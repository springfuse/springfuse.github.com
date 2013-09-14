---
layout: english
title: What is Springfuse? 
---

* [What is Springfuse](#what)
* [How Springfuse works](#how)
* [When to use Springfuse](#when)

<a name="what"></a>
## What is SpringFuse?

Springfuse is a free online service dedicated to generating solid data-oriented application written in Java.

SpringFuse is the online version of <a href="http://www.jaxio.com/en/celerio.html">Celerio</a>,
a professional code generator for Java developed by <a href="http://www.jaxio.com/en/">JAXIO</a>.

Springfuse relies on Celerio to generate __in a few seconds__ web applications that leverage various open source technologies/standards,
such as Hibernate/JPA, Spring Framework, JSF2, etc.

<a name="how"></a>
<br/><br/>
## How does Springfuse work ?

Springfuse uses the structure of __your database as an entry point__.

The generation process is done in __4 automated steps__.

<img src="/images/springfuse/how-springfuse-works-2.png"/>

<span class="badge badge-info">1</span> You run locally on your computer our Springfuse Maven plugin.
It <strong>extracts</strong> the meta-data information from your database. Meta-data includes the table names, 
the column names, indexes and the various integrity constraints.

<span class="badge badge-info">2</span> Springfuse plugin <strong>uploads</strong> the result of this extraction to the Springfuse server. It also uploads
the `maven-celerio-plugin.xml` configuration file present in the folder `src/main/config`. This configuration file allows you to fine tune the generation.

<span class="badge badge-info">3</span> Once uploaded on Springfuse server, <a href="http://www.jaxio.com/en/celerio.html" target="_new">Celerio</a>
code generator generates your project and zip it.

<span class="badge badge-info">4</span> Springfuse plugin then <strong>downloads</strong> your project source code on your computer.
Here you go : you have your first release!

With Springfuse you <strong>save weeks of developments</strong> and you <strong>learn
faster</strong> the Open Source technologies that Springfuses leverages.

<a name="when"></a>
<br/><br/>
## When to use Springfuse?

### Eliminate repetitive tasks

When you identify a repetitive task, your duty is to automate it.
Springfuse automates the tedious and repetitive task of writing the first piece of code of a new Java project.

Actually this first piece of code that Springfuse generates constitute the backbone of your application. It goes way beyond a simple copy paste.
It covers subject such as persistence, 2d level cache, security, dependency injection, distribution, localization, unit tests, etc.

In just a few seconds, Springfuse relieves you from the burden of coding all this not-so-funny part of your application.

Therefore

* You save weeks.
* You reduce your risks.
* You learn from the generated code.
* You can focus on developing real features.
* You deliver on time.

### Learn faster technologies

There are so many Java technologies around! It is moving so fast!
Which ones to choose ? And then, what are the associated best practices ?
You do not always have the time to answer these questions.

Springfuse's mission is to deliver world-class project built on standard or de facto standard technologies following industry best practices

Therefore

* You reduce your maintenance costs.
* Developers learn faster and better with concrete code.
* You improve the overall quality of your project.

### Make it possible !

Cost cuttings, lack of resources, lack of training, impossible dead lines, you name it.

When the wall in front of you is too high, you just cannot climb it without help.
Springfuse can be a precious ladder. Here are two use cases:

### Prototyping

Writing a prototype for free is a common practice in the industry.
You have to work fast, for free, and deliver top notch quality to get the deal.

__Springfuse increases drastically your chances to succeed.__

### Application rewriting

Deciding to rewrite an application is a tough decision. 
There are often many risks.
However, when your customer ask for patches and features that you cannot deliver in time because of some some old code that nobody understand anymore, you do not have many choices. 
But it is too much work, you would need a second team, but there is no budget for that.

__Springfuse helps your existing team make the first move toward your application rewriting.__

