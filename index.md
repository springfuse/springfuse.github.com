---
layout: english
title: SpringFuse - Java Code Generator
---
## SpringFuse no longer operates but... :-)

Celerio the code generator that was powering SpringFuse is now Open Source. Celerio can reverse 
a database schema and generate advanced CRUD-based applications.

* [Celerio Documentation](http://www.jaxio.com/documentation/celerio)
* [Celerio Source Code](https://github.com/jaxio/celerio)

## Related projects

### Code generation templates

 * *IN PROGRESS*: [Web App Angular 2 + PrimeNG + Spring Boot](https://github.com/jaxio/celerio-angular-quickstart)
 * [Java EE 7 Web App frontend and backend: No Spring Inside](https://github.com/jaxio/javaee-lab)
 * [backend: JPA 2 / Hibernate + Lucene + Spring](https://github.com/jaxio/pack-backend-jpa)
 * [frontend: JSF 2 + Spring](https://github.com/jaxio/pack-jsf2-spring-conversation)

### JPA Query By Example API

 * [JPA Query By Example API](https://github.com/jaxio/jpa-query-by-example)

### Bootstrapping a project with Celerio

If you already have Maven 3.3.3 (or above) and Java 1.8 installed, to generate a sample project, simply run:

	mvn com.jaxio.celerio:bootstrap-maven-plugin:4.0.7:bootstrap

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

> **Note** Angular 2 is not yet part of the options yet as it is [under development](https://github.com/jaxio/celerio-angular-quickstart).

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