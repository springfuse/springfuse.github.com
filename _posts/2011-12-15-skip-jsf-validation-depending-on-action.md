---
layout: english
title: How to skip JSF BeanValidation conditionally
comments: true
---

# How to skip JSF BeanValidation conditionally 

Here is a trick that allows you to perform JSF-based BeanValidation depending on the action.

## The challenge

The challenge when developing JSF applications involving multi-page form is to provide a usable navigation between the pages.

By usable navigation we mean:

* a user should be able to navigate freely from one page to another without loosing the data entered in the input fields, even if the entered data is invalid, so that the user can come back to it later.

* for certain actions, for example a 'save' action, the validation should be enforced.

## Requirements

* The solution should be easy to develop and maintain. For example, we have tried to implement the <a href="http://www.coderanch.com/t/481100/JSF/java/Saving-form-without-validation"> a trick that Mr Ed Burns suggests</a>, without any success.

* JSF 2.0 supports BeanValidation, which is extremely convenient. We should leverage it.

## The trick

We leverage the `binding` attribute of the JSF `<f:validateBean/>` tag.

As the documentation says, this attribute value is a <cite>ValueExpression that evaluates to an object that implements javax.faces.validate.BeanValidator</cite>

Unsurprisingly BeanValidator implements the `validate` method below from the `Validator` interface: 

{% highlight java %}
    public void validate(FacesContext context,
                         UIComponent component,
                         Object value) throws ValidatorException;
{% endhighlight %}

We just have to extend `BeanValidator` and override the `validate` method, here is the code:

{% highlight java %}
package com.jaxio.demo.web.component;

import javax.faces.component.UIComponent;
import javax.faces.context.FacesContext;
import javax.faces.validator.BeanValidator;

import org.springframework.beans.factory.config.BeanDefinition;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;

/**
 * Lenient bean validator which disable validation in certain cases 
 * in order to let the user navigate to sub view without loosing the 
 * data entered in input field.  
 */
@Component
@Scope(BeanDefinition.SCOPE_PROTOTYPE)
public class LenientBeanValidator extends BeanValidator {
    @Override
    public void validate(FacesContext context, UIComponent component, Object value) {
        if (doValidation(context)) {
            super.validate(context, component, value);
        }
        // simply skip it...
    }

    private boolean doValidation(FacesContext context) {
        // main page (action that saves the main entity) 
        if (context.getExternalContext().getRequestParameterValuesMap().containsKey("form:save")) {
            return true;
        }

        // sub page (action that binds the entered data to an associated entity)
        if (context.getExternalContext().getRequestParameterValuesMap().containsKey("form:ok")) {
            return true;
        }

        return false;
    }
}
{% endhighlight %}
 
Of course the code above may be improved to fit your need and your security requirements.

## How to use it

Then, to use it from your view, you simply do as follow:

{% highlight html %}
  <h:form id="form">
  	<f:validateBean disabled="true"> 
  	
    	<!-- ... skip for clarity ... -->
    	
		<p:inputText id="email" label="${msg.account_email}" value="#{account.email}" maxlength="80" >
    		<f:validateBean binding="#{lenientBeanValidator}"/>
    	</p:inputText>
    
        <!-- 'save' (validation is enforced) -->
		<p:commandButton id="save" action="save" ajax="true" update="messages" process="@form"
			styleClass="aria-save-button default"
			image="ui-icon-disk"
			value="#{msg.menu_save}"
			rendered="#{not subPage}" />

        <!-- 'ok' (validation is enforced) -->
   		<p:commandButton id="ok" action="ok" process="@form" ajax="true" update="messages" 
   			styleClass="default"
   			image="ui-icon-check"
   			value="${msg.submit}"
   			rendered="#{subPage}" />    

        <!-- 'otherCase' (validation is NOT enforced) -->
   		<p:commandButton id="navigateInSubPage" action="navigateInSubPage" process="@form" ajax="false" 
   			styleClass="default"
   			image="ui-icon-check"
   			value="${msg.submit}"
   		 />    
  	</f:validateBean>
  </h:form>
{% endhighlight %}

If you have any remark on this solution, please share :)

Enjoy!

The SpringFuse/Jaxio team.