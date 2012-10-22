---
layout: english
title: Celerio Guide - Installation
---

Installation
============

Requirements
------------

### JDK 6 or above

Celerio and the generated code require at least JDK 1.6.0_24 to compile and run.
*Download and install the latest JDK from [](http://java.oracle.com)*

Once installed, make sure you can run `javac` from the command line.
Open a command line and run:

	javac –version

You should get a result similar to this:

    javac 1.6.0_37

### Maven 2

Celerio and the generated code require Maven 2.

*Download and install Maven 2 from [](http://maven.apache.org)*

Once installed, make sure you can run Maven 2 from the command line.
Open a command line and run:

	mvn –v

You should get a result similar to this:

    Maven version: 2.0.9
    Java version: 1.6.0_18
    OS name: "windows xp" version: "5.1" arch: "x86" Family: "windows"

### Source control system

Celerio leverages source control (SVN and CVS) usage to provide features
allowing the user to take control over certain generated file.

Before generating such file, Celerio always check if a file of the same
name exists on disk and is present under source control.

Celerio assumes that files under source control should not be
overwritten arbitrarily.

To really take advantage of Celerio's collision features, you must use a
source-control system for the project you intent to generate with
Celerio.

Celerio
-------

Celerio is distributed as a Maven 2 plugin. Celerio plugin is hosted on
Jaxio Maven 2 repository. You can either directly uses it if your
organization allows access to Jaxio's repository or deploy it on your
organization Maven's repository. Please contact Jaxio's for further
details.


