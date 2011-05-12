---
layout: main
title: Code Generation Configuration
---

# Code Generation Configuration

You can fine tune the code generation thanks to a configuration file For example you can change the generated property names, make certain association bidirectional, 
use enums, use joda time, etc... This configuration file comes with 2 xsd files which provide some documentation.

Normally, after running SpringFuse quickstart, you end up with 2 projects:

* The first one, <code>yourproject</code>, reverses your database and calls springfuse server to perform the code generation.
* The second one <code>yourproject-generated</code>, is the code generation results, from where you run <code>mvn jetty:run</code>

To configure the code generation you must edit the file <code>yourproject/src/main/config/maven-celerio-plugin/maven-celerio-plugin.xml</code> and when done, 
re-run the <code>mvn generate-sources</code> command from the folder <code>yourproject</code>.

Since the online version is a one-shot tool, you should rename or delete the folder <code>yourproject-generated</code> before re-runing the <code>mvn generate-sources</code>.

The example project comes with a configuration file that declares a one-to-many relationship, an enum, and rename some properties. You should first play around with this file and rerun the code generation.

Please refer to <a href="http://www.springfuse.com/static/documentation/html/springfuse.html">SpringFuse reference documentation</a>