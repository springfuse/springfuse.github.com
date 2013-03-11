---
layout: english
title: What is Springfuse? 
---

## What is SpringFuse?

SpringFuse is the online version of <a href="http://www.jaxio.com/en/celerio.html">Celerio</a>, a code generation tool for Java developed by <a href="http://www.jaxio.com/en/">JAXIO</a>.

Springfuse relies on Celerio to generate __in a few seconds__ web applications that leverage various open source technologies, such as Spring Framework and Hibernate.

## How Springfuse works

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
