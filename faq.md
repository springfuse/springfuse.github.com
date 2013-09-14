---
layout: english
title: Frequently asked questions 
---

## SpringFuse FAQ

### How can I install the oracle JDBC Driver ?
Oracle jdbc driver is not available on the global public maven repository, you will need to install it manually. 

To do so, please <a href="/install-oracle-jdbc-driver-in-maven-repository.html">follow the following instructions</a>.

### Why are some of my tables ignored ?
Tables having no primary key defined are ignored by Springfuse.

### Why does the remote generation fail ?
Most likely the remote generation failure is due to a specificity in your database schema that we are not able to handle properly. 

Here are few examples that we have encountered:

* A table with no primary key constraint defined
* A column with an esoteric <a href="http://download.oracle.com/javase/6/docs/api/java/sql/Types.html">jdbc type</a> such as (NULL, OTHER, etc.)
* A table having a Foreign key constraint to a table that was not reversed
* The maven-celerio-plugin.xml is referencing a table or a column that does not exist
* A stupid bug on our side. For example 3.0.43 may fail if the JDBC type is DOUBLE (was fixed in 3.0.44)
* If you can fix your schema, please do so and try again! 
* If you cannot change the schema, we are curious to know more about its specificity and determine how we could handle it, so do not hesitate to <a href="/contact-us.html">contact us</a> to tell us more.


### How can I see what is uploaded online ?
We send both generation logs and extracted metadata to the email address provided in springfuse generation form.

### How can I tell maven that I use a proxy ?
If you are behind an http proxy, in order to download properly the dependencies, you must configure maven with a settings.xml file (usually `${user.home}/.m2/settings.xml`). 

Please follow these <a href="http://maven.apache.org/guides/mini/guide-proxies.html">instructions</a> to create this file.

Note that you also need to provide this information to the springfuse maven plugin.

### How can I use previous versions of springfuse ?
Springfuse uses only the latest version of Celerio.
If you rely on a specific Celerio's version, you may be interested in [purchasing Celerio](http://www.jaxio.com/en/pricing.html).

### I am still using jdk 1.5, will it work for me ?
Yes, update the pom.xml accordingly

{% highlight xml %}
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-compiler-plugin</artifactId>
	<version>2.0.2</version>
	<configuration>
		<source>1.6</source>
		<target>1.5</target>
	</configuration>
{% endhighlight %}

###  My answer is not here...
Just <a href="/contact-us.html">contact us</a>, drop us an email at <support@springfuse.com> we will be glad to help you.
