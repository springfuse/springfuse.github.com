---
layout: english
title: Conversation using JPA 2, JSF 2, PrimeFaces and the Spring Framework
comments: true
---

## Important update (2015-11-12)

We have 2 ways to try the JSF Conversation solution detailed in this post:

#### 1/ Mix Spring + JSF 2 + home-made conversation support

The full implementation is available in all projets generated by Celerio.

Follow our doc to ** generate in a few minutes ** your [first project with Celerio](http://www.jaxio.com/documentation/celerio/installation.html)

#### 2/ Pure Java EE 7 + home-made conversation support

Check out the project [https://github.com/jaxio/javaee-lab](https://github.com/jaxio/javaee-lab)
and follow the instructions.


## Conversation with JSF2

In this article we give you a bird eye view on how we implement **custom Conversations for data-driven applications** 
using JPA 2, JSF 2, PrimeFaces and the Spring Framework.

Our solution is using neither CDI nor Spring Web Flow, but a home-made API. We believe our solution has several advantages:

* It is XML free, thus refactorable, debuggable.
* It uses callbacks, which allows us to use a JSF views as black boxes. Spring Web Flow has a similar feature, but it is in XML.
* The core API comprises 15 classes, it is understandable in one day and can be improved to fit your custom needs.
* It does not require any Java EE application server, a bare Jetty or Tomcat is enough.

### Conversation

A conversation is a kind of inner web session. It has a start and an end. 
In between it enforces a strict navigation between pages (like spring webflow or up coming Faces Flow do)

For our case, data-driven applications, a conversation is created each time the user wants to edit a JPA Entity.
It starts with a search page, continue with an edit page and when the user is done editing, he goes back to the search page. 
From there, he can click from the menu a quit button which terminates the conversation.

From the main edit page the user can of course edit the entity's properties but he can also **manage the entity's associations** (if any). 

For example, if the entity has a many-to-many association, the user can add a new entity to this many-to-many association. 
To do so the user can navigate to the target entity's edit page.

But when should the entity be added to the collection ?

* before navigating to the target entity's edit page? 
* after navigating to the target entity's edit page? 

If we choose the first approach we have to handle the case when the user changes his mind and finally prefer not to add the entity.

The second approach is more natural, we add it only if the user clicks a 'Submit' button in the target entity's edit page.

But wait a second. Other entities could also have a many-to-many association to the same target entity.
The target entity edit page should therefore be reusable, that is it should not 'know' from which page the user is coming from.
For this reason we introduce callback. Thus, when the user clicks the 'Submit' button on the target entity page, we invoke a method
on the callback. This approach is extremely powerful. 

### Here is a concrete example

An `Account` entity has a many-to-many association with a `Role` entity.
From the `Account` edit page, when the user clicks on the <img src="/images/blog/2013-03-05/add.png"/>
icon, it invokes the `addRole` method which ultimately sets a callback and return the target entity's edit page (we rely on JSF implicit navigation).

**Here is an extract of the `Account` entity edit page:**

<img src="/images/blog/2013-03-05/conversation-role-tab.png"/>

**Here is an extract of the `AccountEditForm` class, which is a statefull controller:**

{% highlight java %}
public String addRole() {
    ConversationContext<Role> ctx = RoleController.newEditContext(new Role());
    ctx.setLabelWithKey("account_roles");
    ctx.setCallBack(addRoleCallBack);
    getCurrentConversation().setNextContextSub(ctx);
    return ctx.view();
}

protected ConversationCallBack<Role> addRoleCallBack = new ConversationCallBack<Role>() {
    private static final long serialVersionUID = 1L;

    @Override
    protected void onOk(Role role) {
        getAccount().addRole(role);
        messageUtil.infoEntity("status_added_new_ok", role);
    }
};
{% endhighlight %}

**Here is an extract of the target Role edit page:**

<img src="/images/blog/2013-03-05/conversation-role-edit.png"/>

As you have guessed, when the user clicks the "Submit" button above, the `onOk(Role role)` callback is invoked.
In this case it adds the Role to the account's role collection.

Great, but how do we know we should go back to the account's edit page once the role is added?

For each page we create a new ConversationContext, each context has a view property which holds an uri.

**Here is the code that created the ConversationContext to edit the Role entity above:** 

{% highlight java %}
public final static String editUri = "/domain/roleEdit.faces";

/**
 * Helper to construct a new ConversationContext to edit an Role.
 * @param role the entity to edit.
 */
public static ConversationContext<Role> newEditContext(final Role role) {
    ConversationContext<Role> ctx = new ConversationContext<Role>();
    ctx.setEntity(role); // used by GenericEditForm.init()
    ctx.setViewUri(editUri);
    return ctx;
}
{% endhighlight %}

Like for the role edit page, the account edit page also has a ConversationContext (not shown here).

As the user goes forward in the conversation, we stack up (push) conversation contextes. 
Going backward is just a matter of returning the previous ConversationContext's view property after the callback invocation. 
Of course, when going backward, the current ConversationContext is popped from the stack.

For each association we have a similar mechanism, for example, if the user wants to add some existing roles to the account entity,
it clicks on the <img src="/images/blog/2013-03-05/find.png"/> icon. This time, the destination page is not the role edit page but
the role search page, which allows the user to select one or more existing roles.

** Here is the callback for existing roles selection:** 

{% highlight java %}
public String selectRole() {
    ConversationContext<Role> ctx = RoleController.newSearchContext();
    ctx.setLabelWithKey("account_roles");
    ctx.setCallBack(selectRoleCallBack);
    ctx.setVar("multiCheckboxSelection", true);
    getCurrentConversation().setNextContextSub(ctx);
    return ctx.view();
}

protected ConversationCallBack<Role> selectRoleCallBack = new ConversationCallBack<Role>() {
    private static final long serialVersionUID = 1L;

    @Override
    protected void onSelected(List<Role> roles) {
        for (Role role : roles) {
            Role mergedRole = getCurrentConversation().getEntityManager().merge(role);
            if (!getAccount().containsRole(mergedRole)) {
                getAccount().addRole(mergedRole);
                messageUtil.infoEntity("status_added_existing_ok", mergedRole);
            }
        }
    }
};
{% endhighlight %}

**And here is an extract of the target search role page:**

<img src="/images/blog/2013-03-05/conversation-role-search.png"/>

When the user clicks on the <img src="/images/blog/2013-03-05/accept.png"/> icon, the callback `onSelected(List<Role> roles)` is invoked.
This callback is more interesting, as you can see we keep an EntityManager instance in the Conversation.

The conversation allows you to move forward/backward through the entity graph, the changes you make are retained in this conversation's entityManager. 
Nothing is committed until you invoke a service method annotated with a read-write @Transactional
This means you can have a long conversation to prepare all the desired changes and commit them in a short transaction.

**This works great, however, there is one drawback:**
If you use the conversation's entityManager in search pages, you may not see changes made by others as the entityManager guaranties you repeatable reads. 
For this reason, we do not use the conversation's entityManager in search page.
This way we are sure to display the most up to date data to the user. You should now better understand why we need 
to merge the selected roles back in the conversation's entity manager.

Note that both the role search page and the role edit page that are used in the Account's conversation are also used in the Role conversation... reusability we said.

### Conversation Scope

Our Conversation API defines a custom Spring Scope, named `conversation`.

Beans in the conversation scope reside in a ConversationContext. They are visible only when the conversation is bound to the current 
Thread of execution and their hosting ConversationContext is on top of the conversation's contextes stack.
This allows a conversation to have 2 'conversation scoped' beans with the same name (they just have to reside in 2 different ConversationContext).
This prevents bean name clash in complex navigation scenario within the same conversation.

### Misc

* The user can have several conversations in parallel, we provide a menu Conversations menu to switch from one conversation to another
* We limit the number of Conversation per user. In case the max number of conversations is reached a warning page is displayed.
* etc.

### Conclusion

This simple API:

* enforces navigation
* supports extended persitence context (i.e. we reuse the same entityManager in conversation's edit pages) 
* allows page reuse thanks to callbacks
* is strongly typed
* is easy to understand (assuming you are not a beginner). 

What else would you want? Your answer is probably: we want CDI!

And we agree with you, if someone send us the source code to do the same thing using CDI we would be delighted to propose it in the code we generate :-)

If you want to know more, the best is to study the source code and run it on your computer.

**We encourage you to ** follow our doc to ** generate in a few minutes ** your [first project with Celerio](http://www.jaxio.com/documentation/celerio/installation.html)

Have fun !

The Jaxio/SpringFuse team.
