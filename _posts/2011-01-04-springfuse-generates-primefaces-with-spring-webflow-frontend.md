---
layout: main
title: Springfuse generates Primefaces with Spring Web Flow front end
comments: true
---

# Springfuse generates Primefaces with Spring Web Flow front end

We are pleased to announce that SpringFuse (v 3.0.43), our online Java Code Generation service, is now able to generate advanced CRUD web applications leveraging:

* JSF2
* PrimeFaces 2.2
* SpringWebFlow 2.2.1,
* JPA2
* Bean Validation,
* Spring 3.0.5
* SpringSecurity 3.0.5

Thanks to <a href="http://www.primefaces.org/showcase">PrimeFaces</a>, the generated front-end looks great, comes with some nice cool Ajax effects, is easy to understand and modify.
The CRUD navigation is entirely driven by <a href="http://static.springsource.org/spring-webflow/docs/2.2.x/reference/htmlsingle/spring-webflow-reference.html">Spring Web Flow</a>.

# Reusable flows

For each entity SpringFuse generates 2 reusable flows:

* one to search for existing entity instances
* one to create/read/update/delete the entity

Whenever an entity has an association (many-to-one, one-to-one, one-to-many, many-to many), you can navigate to it until you reach leaves. 
This advanced navigation is achieved thanks to flows composition.

# Advances navigation

Here is how look for example a 'search' view for the Account entity (example provided by SpringFuse)

<a href="/images/blog/2011-02-04/springfuse-primefaces-webflow-search.png" class="screen" title="Ajax navigation" rel="group"><img src="/images/blog/2011-02-04/springfuse-primefaces-webflow-search-min.png" /></a>

And below, here is how look the 'edit' view for the Account entity

<a href="/images/blog/2011-02-04/springfuse-primefaces-webflow-edit.png" class="screen" title="Ajax navigation" rel="group"><img src="/images/blog/2011-02-04/springfuse-primefaces-webflow-edit-min.png" /></a>

# Extended persistence context

As you walk through the entity graph, the changes you make are retained in an extended persistence context bound to the conversation. 
Nothing is committed until you invoke a service method annotated with a read-write @Transactional
This means you can have a long conversation to prepare all the desired changes and commit them in a short transaction. 

A nice side-effect of using extended persistence context is that you no longer have to spend your time merging entities as the user navigates from one view to an other. Indeed, the entities remain by definition in the same persitence context.
The back-end is the same as before, JPA2, Bean Validation, Spring, etc. 

# Building upon great technologies

Thanks to PrimeFaces and Spring Web Flow, it becomes a real pleasure to work with JSF and real enterprise applications can be written without spending months on re-inventing the wheel... specially when you use SpringFuse ;-) 

# Springfuse

We hope this contribution will make you realize the potential of such architecture for enterprise applications. 

We won't go further in the details of all the generated code. 

# Your turn

The best is to generate a project, play with it and study the source code. 

Have fun !