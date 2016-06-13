---
layout: english
title: SpringFuse - Online Java Code Generator
---

## Switching to Celerio 4

We are pleased to announce that Celerio (the code generator that was powering SpringFuse) is now Open Source.

For more information please visit [Jaxio's site](http://www.jaxio.com/en/)

### Bootstrapping

If you already have Maven 3.3.3 (or above) and Java 1.8 installed, to generate a sample project, simply run:

	mvn com.jaxio.celerio:bootstrap-maven-plugin:4.0.5:bootstrap

You will be asked by our `bootstrap-maven-plugin` to choose between 3 options:
    
     1) pack-javaee7-wildfly
        https://github.com/jaxio/javaee-lab
        Pure Java EE 7 web application (no Spring inside) running on WildFly 10.
        Uses JPA, Hibernate, Hibernate Search, Lucene, JSF and PrimeFaces.
    
     2) pack-jsf2-spring-conversation
        https://github.com/jaxio/pack-jsf2-spring-conversation
        PrimeFaces 5.2, JSF 2.2, JPA 2.1/Hibernate 5, Spring 4.2
        Advanced CRUD web application with conversation support in Java.
    
     3) pack-backend-jpa
        https://github.com/jaxio/pack-backend-jpa
        Backend only: almost pure JPA 2.1 with Hibernate 5, Spring 4.2
        Generates entities, meta model and repositories. Used by front-end packs.

### Angular 2 / TypeScript / PrimeNG / Spring Boot option...

This option is not yet bundled in the `bootstrap-maven-plugin`.

You may try it here directly from the source:

[https://github.com/jaxio/celerio-angular-quickstart](https://github.com/jaxio/celerio-angular-quickstart)

Simply follow the instructions...

Feedbacks are welcome.

Happy coding with Celerio!

The Jaxio team.

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