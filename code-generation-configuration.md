---
layout: english
title: Code Generation Configuration
---

# Code Generation Configuration

You can fine tune the code generation thanks to a configuration file For example you can change the generated property names, make certain association bidirectional, 
use enums, use joda time, etc... This configuration file comes with 2 xsd files which provide some documentation.

Normally, after running SpringFuse quickstart, you end up with 2 projects:

* The first one, `yourproject`, reverses your database and calls springfuse server to perform the code generation.
* The second one `yourproject-generated`, is the code generation results, from where you run `mvn jetty:run`

To configure the code generation you must edit the file `yourproject/src/main/config/maven-celerio-plugin/maven-celerio-plugin.xml` and when done, 
re-run the `mvn generate-sources` command from the folder `yourproject`.

Since the online version is a one-shot tool, you should rename or delete the folder `yourproject-generated` before re-runing the `mvn generate-sources`.

The example project comes with a configuration file that declares a one-to-many relationship, an enum, and rename some properties. You should first play around with this file and rerun the code generation.

Please refer to <a href="http://www.springfuse.com/documentation/springfuse.html">SpringFuse reference documentation</a>