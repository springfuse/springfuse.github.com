---
layout: english
title: Celerio Guide - Troubleshooting
---

Troubleshooting
===============

Generated code does not compile
-------------------------------

You may encounter a situation where the generated Java code does not
compile. This could be due to a Celerio's bug. To avoid loosing too much
time on this issue, if you know how to fix the compilation error, you
should take totally control over the generated file that does not
compile (please refer to ?) and fix the compilation error manually.

Make sure you also report the issue to <support@jaxio.com> so it get
fixed in a next release of Celerio. As soon as the issue is fixed in
Celerio, you may give the control back to Celerio by simply removing the
file so Celerio can generate it as usual.

Tomcat converts request parameters to 0, "" or true
---------------------------------------------------

By default Tomcat coerces null values of types such as java.lang.String
or java.lang.Boolean to `""` or `false`.

Please edit your `catalina.properties` file and add the following
property:

	org.apache.el.parser.COERCE_TO_ZERO=false

Please refer to [Tomcat System
properties](http://tomcat.apache.org/tomcat-6.0-doc/config/systemprops.html)
for more information.

PermGen when running Jetty
--------------------------

Increase the memory:

	export MAVEN_OPTS="-Xmx2048m -XX:MaxPermSize=128m"
 