---
layout: english
title: Why we switched from jaxb to jibx
comments: true
---

# Why we switched from jaxb to jibx
Here is what you will find in this post :

* xsd to java generation using jaxb2 with an <a href="https://github.com/springfuse/xsd-to-java-with-jaxb2">maven project example</a>
* java to xsd generation using jaxb2
* jaxb2 cannot generate an xsd with documentation
* xsd from java generation using jibx with a <a href="https://github.com/springfuse/xsd-to-java-with-jibx">maven project example</a>
* jibx customization is easy
* add jibx xsd generation in maven with customization
* how to use jibx using spring oxm


## XSD authored manually

Continuing on my previous post on how to <a href="http://blog.springfuse.com/2009/09/better-way-to-handle-maven-plugin.html">integrate your own xsd to ease your plugin configuration</a>, 
I will talk today on something that really bugged me for a while.

Some of our xsd are pretty large; we created them using xsd authoring tool, then continued by hand.
We used <a href="https://jaxb.dev.java.net/">jaxb</a> to produce the java code to map the xsd, but the generated code was not that great.
There are some ways to tweak the <a href="https://jaxb.dev.java.net/jaxb-maven2-plugin">xjc plugin</a> to bend the produced code the way you like. But this was way too awkward for us.

## Jaxb generates XSD from java annotations
Then we thought that it was time to use the java code and annotate it with <a href="http://java.sun.com/javaee/5/docs/api/javax/xml/bind/annotation/package-tree.html">jaxb annotation</a> so we could produce the xsd for our users to use.

You annotate with the same few annotations here and there, and after this very tedious task you can add <a href="https://jaxb.dev.java.net/maven-jaxb-schemagen">maven-jaxb-schemagen-plugin</a> plugin to your pom and voilà you have a fresh xsd ready for production generated directly from your classes.

But something is missing, looks like the generated xsd is very small compared to the manually authored one: <b>jaxb did not insert any documentation</b> !

Of course I thought that I did a silly mistake, and was ready to add something like @XmlDocumentation annotations.
And here starts the story: there is no way to add documentation information to schemagen !

## Jaxb cannot generate an XSD with configuration
This really surprised me, because the xsd are also here to help the users when they author an xml by showing documentation while they type etc.

I really searched to find a way to use the tool; I even tried to dive into the schemagen source-code to see if there would be an existing annotation not present in the documentation.

By the way, let me give a big thumb down to <a href="https://www.dev.java.net/servlets/ProjectList">java.net</a> for beeing <a href="http://twitter.com/framiere/status/4325130844">so slow</a> ! 
It was <b>hell</b> to navigate through the documentation on a site that is <b>that</b> slow. 

Wrong path: I was stuck. But there was no way I wanted to continue maintaining both the java and the xsd ! 

# Enter jibx
Then I looked at the alternatives to jaxb, and quickly found out jibx <a href="http://jibx.sourceforge.net/">http://jibx.sourceforge.net/</a> was the tool I was looking for!

<a href="http://jibx.sourceforge.net/fromcode/index.html">Bindgen</a> is for jibx what maven-jaxb-schemagen-plugin is for jaxb. But instead of relying on annotation, 
bindgen rely solely on the class attributes and on the javadocs for producing the xsd and its documentation.
Here is an example :

{% highlight java %}
	public class XSD {
	 
	 /** please define your complex object */
	 private ComplexObject complexObject;
	 /** you are allowed to set many simple objects */
	 private List<SimpleObject> simpleObject = new ArrayList<SimpleObject>();
	}
{% endhighlight %}

{% highlight java %}
	public class ComplexObject {
	 /**
	  * only string are allowed
	  */
	 private String stringAttribute;
	 /**
	  * This should be a date
	  */
	 private Date dateAttribute;
	 /**
	  * boolean are so over
	  */
	 private boolean thisIsABool = false;
	 /**
	  * enums are much better than booleans
	  */
	 private MyEnum myEnum;
	}
{% endhighlight %}

Would generate the following xsd : 

{% highlight xml %}
	<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:tns="http://jaxio.com" elementFormDefault="qualified" targetNamespace="http://jaxio.com">
	  <xs:element type="tns:XSD" name="XSD"></xs:element>
	  <xs:complexType name="XSD">
	    <xs:annotation>
	      <xs:documentation>this is my annotated xsd</xs:documentation>
	    </xs:annotation>
	    <xs:sequence>
	      <xs:element name="complexObject" minOccurs="0">
	        <xs:annotation>
	          <xs:documentation>please define your complex object</xs:documentation>
	        </xs:annotation>
	        <xs:complexType>
	          <xs:sequence>
	            <xs:element type="xs:string" name="stringAttribute" minOccurs="0">
	              <xs:annotation>
	                <xs:documentation>only string are allowed</xs:documentation>
	              </xs:annotation>
	            </xs:element>
	            <xs:element name="myEnum" minOccurs="0">
	              <xs:annotation>
	                <xs:documentation>enums are much better than booleans</xs:documentation>
	              </xs:annotation>
	              <xs:simpleType>
	                <xs:annotation>
	                  <xs:documentation>this is a enum, you need to choose between the values</xs:documentation>
	                </xs:annotation>
	                <xs:restriction base="xs:string">
	                  <xs:enumeration value="A"></xs:enumeration>
	                  <xs:enumeration value="B"></xs:enumeration>
	                  <xs:enumeration value="C"></xs:enumeration>
	                  <xs:enumeration value="D"></xs:enumeration>
	                </xs:restriction>
	              </xs:simpleType>
	            </xs:element>
	          </xs:sequence>
	          <xs:attribute type="xs:dateTime" name="dateAttribute">
	            <xs:annotation>
	              <xs:documentation>This should be a date</xs:documentation>
	            </xs:annotation>
	          </xs:attribute>
	          <xs:attribute type="xs:boolean" use="required" name="thisIsABool">
	            <xs:annotation>
	              <xs:documentation>boolean are so over</xs:documentation>
	            </xs:annotation>
	          </xs:attribute>
	        </xs:complexType>
	      </xs:element>
	      <xs:element name="simpleObject" minOccurs="0" maxOccurs="unbounded">
	        <xs:complexType>
	          <xs:sequence>
	            <xs:element type="xs:string" name="simpleString" minOccurs="0">
	              <xs:annotation>
	                <xs:documentation>trivial string</xs:documentation>
	              </xs:annotation>
	            </xs:element>
	          </xs:sequence>
	          <xs:attribute type="xs:int" use="required" name="simpleNumeric">
	            <xs:annotation>
	              <xs:documentation>trivial numeric</xs:documentation>
	            </xs:annotation>
	          </xs:attribute>
	        </xs:complexType>
	      </xs:element>
	    </xs:sequence>
	  </xs:complexType>
	</xs:schema>
{% endhighlight %}

Perfect: all the documentation is present, it is taken directly from the javadoc!

But if you follow closely the xsd, the stringAttribute and myEnum are not properties, they are defined as element.

An xml would look like

{% highlight xml %}
	<complexObject thisIsABool="true" dateAttribute="2009-10-01T20:36:39.515Z">
	    <stringAttribute>my string attribute</stringAttribute>
	    <myEnum>B</ myEnum>
	</complexObject>
{% endhighlight %}

You could also see that there is no mention on required, default values etc.

## Jibx customization is easier than jaxb's
Bindgen is not that magic, we have to give it hints using customization, fortunately it is pretty straightforward thanks to a <a href="http://jibx.sourceforge.net/fromcode/bindgen-customs.html">good documentation</a> along with <a href="http://jibx.sourceforge.net/fromcode/bindgen-example1.html">examples</a>.

{% highlight xml %}
	<custom>
	    <class name="com.jaxio.ComplexObject" optionals="myEnum">
	        <value attribute="myEnum" property-name="myEnum"></value>
	        <value attribute="stringAttribute" property-name="stringAttribute"></value>
	    </class>
	</custom>
{% endhighlight %}

The only major pain was to make everything work in maven, in particular:

* The BindGen setup using the ant task maven plugin and the correct dependencies
* maven-jibx-plugin can use only relative path for its directory configuration point.
 
You can download and execute a <a href="http://www.springfuse.com/blog/jibx-jaxb/jibx-java-to-xsd-0.0.1-src.zip">working example here</a>.

## Jibx and spring OXM
And now jibx and <a href="http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/">Spring 3.0</a> <a href="http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/ch14.html">oxm project</a>!
Oxm will help you to have a nice <a href="http://static.springsource.org/spring/docs/3.0.x/javadoc-api/org/springframework/oxm/MarshallingException.html">hierarchy of exception</a> that wraps your underlying xml provider so you do not have to deal with it.

{% highlight java %}

	JibxMarshaller marshaller = new JibxMarshaller();
	marshaller.setTargetClass(XSD.class);
	marshaller.afterPropertiesSet();
	
	// write
	StringWriter writer = new StringWriter();
	marshaller.marshal(xsd, new StreamResult(writer));
	System.out.println(writer.toString());
	
	// load 
	(XSD) marshaller.unmarshal(new StreamSource(new FileInputStream(filename))
{% endhighlight %}

You have a unit test ready to be executed in the <a href="http://www.springfuse.com/blog/jibx-jaxb/jibx-java-to-xsd-0.0.1-src.zip">sample project</a>

Have fun with jibx !