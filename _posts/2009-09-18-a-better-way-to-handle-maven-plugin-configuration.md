---
layout: english
title: A better way to handle maven plugin configuration
comments: true
---

# A better way to handle maven plugin configuration

## When times were simple
Celerio the code generation engine behind <a href="http://www.springfuse.com/">springfuse.com</a> is a maven plugin.

It can be configured extensively via xml.

Only a small subset can be configured directly in maven relying on mojo's source level annotations described <a href="http://maven.apache.org/developers/mojo-api-specification.html#The_Descriptor_and_Annotations">here</a>.
 
You can get variables directly like this :
{% highlight java %}
	  /**
	   * jdbc user
	   * @parameter expression="${jdbc.user}"
	   * @parameter required
	   */
	  protected String jdbcUser;
{% endhighlight %}

Or relying on simple nested structures like this :

{% highlight java %}
    /**
 * list of enabled modules
 * @parameter
 */
   protected String[] enabledModules = new String[0];
{% endhighlight %}

So you could configure your plugin like that

{% highlight xml %}
    <plugin>
      <groupId>sample.plugin</groupId>
      <artifactId>maven-hello-plugin</artifactId>
      <version>1.0-SNAPSHOT</version>
      <configuration>
        <jdbcUser>me</jdbcUser>
        <enabledModules>
            <enabledModule>module1</enabledModule>
            <enabledModule>module2</enabledModule>
        </enabledModules>
      </configuration>
    </plugin>
{% endhighlight %}

When we first wrote the maven plugin we were happy and life was simple.

## When the storm came

But in fact it was a pain, because of the limitation of the maven plugin configuration mapping support we had 2 representations of our configuration, 
one for the maven plugin, and the other one for the xml file backed by an XSD.
Therefore it meant for us to merge manually both configuration, duplication of code was involved, documentation was a pain, twice the testing, and worst : questions from our customers.

## Weather is changing
While navigating in the <a href="http://maven.apache.org/maven-v4_0_0.xsd">maven xsd</a> I stumbled on the plugin configuration tag definition which is

{% highlight xml %}
    <xs:element name="configuration" minOccurs="0">
        <xs:annotation>
            <xs:documentation source="version">0.0.0+</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:any minOccurs="0" maxOccurs="unbounded" processContents="skip"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
{% endhighlight %}

Notice the processContents="skip". I never paid attention to it but when you set your maven plugin configuration it is not known by the maven xsd 
therefore it makes perfect sense to skip the maven.xsd validation of the enclosed xml tags ... and let maven's magic appear.

{% highlight xml %}
    <plugin>
      <groupId>sample.plugin</groupId>
      <artifactId>maven-hello-plugin</artifactId>
      <version>1.0-SNAPSHOT</version>
      <configuration>
        <jdbcUser>me</jdbcUser>  <!-- not part of maven xsd -->
        <enabledModules> <!-- not part of maven xsd -->
            <enabledModule>module1</enabledModule> <!-- still not part of maven xsd -->
            <enabledModule>module2</enabledModule> <!-- and your editor does not complain -->
        </enabledModules>
      </configuration>
    </plugin>
{% endhighlight %}

This made me realize that maven must handle the content of the tag as plain xml string or some kind of DOM. Of course, how could it be otherwise?
And if there was a way of getting from the plugin the xml, I could use it too and sent it to our configuration service!

## And the sun shines again
I fired Eclipse and went on navigating in maven source code to find code related to configuration.

It was not long before I found <a href="http://maven.apache.org/ref/2.0.8/maven-model/apidocs/org/apache/maven/model/Plugin.html">http://maven.apache.org/ref/2.0.8/maven-model/apidocs/org/apache/maven/model/Plugin.html</a>

Then <a href="http://maven.apache.org/ref/2.0.8/maven-model/apidocs/org/apache/maven/model/ConfigurationContainer.html#getConfiguration()"> http://maven.apache.org/ref/2.0.8/maven-model/apidocs/org/apache/maven/model/ConfigurationContainer.html#getConfiguration()</a> 

{% highlight java %}
    /**
 * Get The configuration as DOM object.
 */
    public Object getConfiguration() {
     ...
     }
{% endhighlight %}

... I was on the right track.
Turns out this Object is an Xpp3Dom object <a href="http://plexus.codehaus.org/plexus-utils/apidocs/org/codehaus/plexus/util/xml/class-use/Xpp3Dom.html">http://plexus.codehaus.org/plexus-utils/apidocs/org/codehaus/plexus/util/xml/class-use/Xpp3Dom.html</a>
And the good story is that its toString method returns directly the DOM as a String xml representaton.
Perfect, I could give that to my configuration service, and voilà.

## Back to cloudy times
The maven plugins typically extends the <a href="http://maven.apache.org/ref/2.0.4/maven-plugin-api/apidocs/org/apache/maven/plugin/AbstractMojo.html">AbstractMojo</a> to get facilities. But you cannot get the desired plugin instance directly! Yes that's really strange. 
Turns out, I found the solution <a href="http://stackoverflow.com/questions/125389/best-way-to-access-the-runtime-configuration-of-a-maven-plugin-from-a-custom-mojo">here</a>
There must some way to get it more easily, maybe by implementing some interface or what not. But I could stop there with maven as I had what I wanted.

## And the XSD sun shines again
Adding our xsd in the pom project header
{% highlight xml %}
	<project xmlns="http://maven.apache.org/POM/4.0.0" 
	             xmlns:celerio="http://www.jaxio.com/schema/celerio" 
	             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd
	                                             http://www.jaxio.com/schema/celerio http://www.jaxio.com/schema/prototype/celerio-2.6.xsd">
	    ...
{% endhighlight %}

We could now have 

{% highlight xml %}
    <plugin>
     <groupId>com.jaxio.prototype</groupId>
     <artifactId>maven-celerio-plugin</artifactId>
     <configuration>
      <celerio:celerio>
       <celerio:database jdbcUser="myJdbcUser"/>
      </celerio:celerio>
     </configuration>
        <executions>
            ...
        </executions>
    </plugin>
{% endhighlight %}

Our customers will now be guided by their editors when configuring our maven plugin.
They will use the same knowledge they used when using our xml configuration file.
Oh yes, and when you get your maven pluging configuration, all the substitutions has been made.
Therefore it is not the "raw" configuration.

{% highlight xml %}
    <plugin>
     <groupId>com.jaxio.prototype</groupId>
     <artifactId>maven-celerio-plugin</artifactId>
     <configuration>
      <celerio:celerio>
       <celerio:my>
           <celerio:really>
               <celerio:deep>
                   <celerio:nested-structure>
                       <celerio:that>makes sense to you</celerio:that>
                   </celerio:nested-structure>
               </celerio:deep>
           </celerio:really>
       </celerio:my>
      </celerio:celerio>
     </configuration>
        <executions>
            ...
        </executions>
    </plugin>
{% endhighlight %}


## Then the rainbow :)
So by noticing the attribute in the maven xsd, and following its logic I went on adding real value to our product that is:

* auto-documented configuration via xsd in both pom.xml and xml configuration file
* a single configuration
* a single documentation
* and no more (valid) questions from our customer
