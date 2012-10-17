---
layout: english
title: Celerio Guide - Database Schema extraction
---

Database Schema extraction
==========================

Principle
---------

The database schema extraction is performed by
`maven-dbmetadata-plugin`, a Maven 2 plugin provided by Jaxio.

This plugin connects to a relational database using JDBC and reverses 
the database schema meta data. The reverse engineering consists in serializing the
information returned by the JDBC driver into an XML file.

> **Note**
>
> The metadata file produced by the plugin is not meant to be edited
> manually. If you need to change some settings, you should either
> change your database schema or use Celerio's configuration file.

While pretty straightforward the schema extraction may take several minutes on large
database schemas (e.g. more than 200 tables). *To prevent useless
extraction* , the simplest approach is to declare a Maven profile
dedicated to database extraction and activate it only when needed. As an
example you can use the `pom.xml` that Celerio `bootstrap` goal
produces.

The `metadata.xml` file produced by this plugin is used by Celerio's generate goal.

Plugin details
--------------

### Full name

* name: com.jaxio.celerio:maven-dbmetadata-plugin:3.0.86
* goal: extract-metadata

### Attributes

#### skip
* expression: maven-celerio-plugin.skip
* default value: false
* description: Should the database meta data extraction be skipped ? 
This is a common pattern in Maven, where you can skip plugins using profiles to fully adapt your build.

#### jdbcDriver
* expression: jdbc.driver
* description: Set the JDBC driver class
* example: org.postgresql.Driver

#### jdbcUrl
* expression: jdbc.url
* description: Set the JDBC url to connect to your database. Make sure that you connect with enough privileges to access the meta data information.
* example: jdbc:h2:~/.h2/sampledatabase

#### jdbcUser
* expression: jdbc.user
* description: Set the JDBC user, this user needs to have the privilege to access the database metadata.

#### jdbcPassword 
* expression: jdbc.password
* description: Set the JDBC password.

#### jdbcCatalog
* expression: jdbc.catalog
* description: Set the JDBC catalog.

#### jdbcOracleRetrieveRemarks 
* expression: jdbc.oracleRetrieveRemarks
* default value: false
* description: Should the Oracle remarks be retrieved ? Please note that this will impact the speed of the reverse engineering of your database.

#### jdbcOracleRetrieveSynonyms 
* expression: jdbc.oracleRetrieveSynonyms
* default value: true
* description: Should the synonyms be retrieved ?

#### jdbcReverseViews
* expression: jdbc.reverseViews 
* default value: false
* description: Should this plugin also reverse VIEWS?

#### jdbcSchema 
* expression: jdbc.schema
* description: Set the JDBC schema.

#### targetFilename 
* expression: maven-metadata-plugin.targetFilename 
* default value: ${basedir}/src/main/config/maven-celerio-plugin/metadata.xml
* description: The fully qualified name of the XML file created by this plugin.

Simple Usage
------------

In your pom.xml, declare the properties required by the plugin and create a dedicated profile to execute the plugin.

{% highlight xml %}

	<properties>
		<jdbc.groupId>com.h2database</jdbc.groupId>
		<jdbc.artifactId>h2</jdbc.artifactId>
		<jdbc.version>1.3.167</jdbc.version>
		<jdbc.driver>org.h2.Driver</jdbc.driver>
		<jdbc.url>jdbc:h2:~/.h2/mydbname;MVCC=TRUE</jdbc.url>
		<jdbc.user>admin</jdbc.user>
		<jdbc.password></jdbc.password>
	</properties>

<!-- skip -->
	
		<profile>
			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
			<!-- Extract the database metadata -->
			<!-- ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ -->
			<id>metadata</id>
			<build>
				<defaultGoal>generate-sources</defaultGoal>
				<plugins>
					<plugin>
						<groupId>com.jaxio.celerio</groupId>
						<artifactId>maven-dbmetadata-plugin</artifactId>
						<version>${maven-celerio-plugin.version}</version>
						<executions>
							<execution>
								<id>Extract the database schema.</id>
								<goals>
									<goal>extract-metadata</goal>
								</goals>
							</execution>
						</executions>
						<dependencies>
							<dependency>
								<groupId>${jdbc.groupId}</groupId>
								<artifactId>${jdbc.artifactId}</artifactId>
								<version>${jdbc.version}</version>
							</dependency>
						</dependencies>
					</plugin>
				</plugins>
			</build>
			<repositories>
				<repository>
					<id>springfuse-repository</id>
					<url>http://maven2.springfuse.com/</url>
				</repository>
			</repositories>
			<pluginRepositories>
				<pluginRepository>
					<id>springfuse-repository</id>
					<url>http://maven2.springfuse.com/</url>
				</pluginRepository>
			</pluginRepositories>
		</profile>
{% endhighlight %}
		