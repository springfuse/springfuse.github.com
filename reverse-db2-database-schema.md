---
layout: english
title: Generate Spring MVC3, JQuery, JPA2 CRUD Application
comments: true
---

# Generate a project from an IBM DB2 database schema

Reversing a DB2 database with springfuse requires few additional steps that we describe here.


## Install the JDBC Driver

The DB2 jdbc driver is not available on maven central repository. You must download it from <a href="http://www-01.ibm.com/software/data/db2/express/download.html">IBM site</a>
and install it manually. 

In addition to the driver, you must also install a license for the driver to function normally.

Assuming you have found your way on IBM site, you should have the 2 following jars handy:

* db2jcc4.jar
* db2jcc_license_cu.jar

Let's assume the driver version your downloaded is "9.7.0.4"

Open a console, go to the folder containing these 2 jar files, and run the following commands to deploy them in your local maven repository:


mvn install:install-file -Dfile=db2jcc4.jar -DgroupId=com.ibm.db2 -DartifactId=db2jcc4 -Dversion=9.7.0.4 -Dpackaging=jar -DgeneratePom=true

mvn install:install-file -Dfile=db2jcc_license_cu.jar -DgroupId=com.ibm.db2 -DartifactId=db2jcc_license_cu -Dversion=9.7.0.4 -Dpackaging=jar -DgeneratePom=true

## Fill SpringFuse form

On SpringFuse generation form simply select DB2 as your database and fill the appropriate informations.

Copy paste the resulting command and run it. 

It will fail as by default SpringFuse does not depend on the DB2 licence jar.

So, please edit the springfuse.xml file that was created and add the following dependency:

{% highlight xml %}
	<dependency>
    	<groupId>com.ibm.db2</groupId>
        <artifactId>db2jcc_license_cu</artifactId>
        <version>9.7.0.4</version>
	</dependency>                  
{% endhighlight %}

From your console, try again to reverse the database by running:
mvn -f springfuse.xml generate-sources

Now it should work. 

Once the generation is complete, edit the newly created pom.xml file and add the driver and license dependency to it so the generated project can access the DB2 database too.

Then run mvn jetty:run or mvn test
