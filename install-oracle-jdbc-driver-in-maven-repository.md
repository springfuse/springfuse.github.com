---
layout: english
title: Install Oracle Jdbc driver in your Maven local repository
---

#### Celerio and Oracle

Before [using Celerio to reverse your Oracle database and generate a projet](http://www.jaxio.com/en/) you must first follow these 3 steps.

### Install Oracle Jdbc driver in your Maven local repository

If you are using Oracle, you must first install your Oracle JDBC driver in your local Maven repository.

Here is how to proceed:

#### Step 1 - Download the Oracle JDBC driver

Please download manually the Oracle JDBC driver <a href="http://www.oracle.com/technetwork/database/features/jdbc/index-091264.html">from Oracle web site</a>.

#### Step 2 - install your Oracle JDBC driver in your local Maven repository

We follow the instructions from this Maven FAQ <a href="http://maven.apache.org/general.html#importing-jars" target="_new">I have a jar that I want to put into my local repository. How can I copy it in?</a>

In this example, we assume that your Oracle JDBC driver is in a file called <strong>classes12_g.jar</strong>

Open a console and go to the folder containing the classes12_g.jar file.

<pre class="screen">
c:\oracle\jdbc>dir
23/06/2008  13:02		 2 044 594 classes12_g.jar
</pre>

Let's assume you want to register your driver under the group id 'com.oracle', use 'oracle' as the name of the artifact id and that you want the version to be '10.2.0.2.0'.

You can now run the following command:

<pre class="screen">
c:\oracle\jdbc>mvn install:install-file -Dfile=classes12_g.jar -DgroupId=com.oracle \
-DartifactId=oracle -Dversion=10.2.0.2.0 -Dpackaging=jar -DgeneratePom=true

[INFO] Scanning for projects...
[INFO] Searching repository for plugin with prefix: 'install'.
[INFO] ------------------------------------------------------------------------
[INFO] Building Maven Default Project
[INFO]	task-segment: [install:install-file] (aggregator-style)
[INFO] ------------------------------------------------------------------------
[INFO] [install:install-file]
[INFO] Installing c:\oracle\jdbc\classes12_g.jar to C:\Users\Nicolas\.m2\repository\com\oracle\oracle
\10.2.0.2.0\oracle-10.2.0.2.0.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESSFUL
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 1 second
[INFO] Finished at: Tue Feb 03 12:58:23 CET 2009
[INFO] Final Memory: 3M/5M
[INFO] ------------------------------------------------------------------------
</pre>

#### Step 3 - Ready!

You can now add the driver dependency in your pom.xml
<pre class="screen">
&lt;dependency&gt;
	&lt;groupId&gt;com.oracle&lt;/groupId&gt;
	&lt;artifactId&gt;oracle&lt;/artifactId&gt;
	&lt;version&gt;10.2.0.2.0&lt;/version&gt;
&lt;/dependency&gt;
</pre>


<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>






 