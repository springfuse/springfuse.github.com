---
layout: main
title: Springfuse features 
---

# Springfuse features

We describe here the features of the project that Springfuse generates.
Whenever we can, we try to follow the principle of the least surprise which means
you should not be too surprised by our technological or implementation choices.
Following this principle makes the project easier to maintain and reduces the learning curve.


# Project Build System

The generated project uses Maven 2.

The generated Maven pom.xml is pre-configured with convenient plugins such as
* the Jetty plugin to start your web application without having to package it,
* the Surefire plugin to run the unit tests,
* the Cobertura plugin to perform test coverage reports, etc.

All Jar dependencies have version number set as a properties in the pom.xml.
There is no snapshot version for Jar dependencies.

# Project Best practices
## Generated Source code

The various generated components implement interfaces. There is no cyclic dependencies. We run some audit tools
on the generated code and we try to follow the tools recommendations, when they are relevant.

## Unit tests / Integration tests

Unit tests and integration tests are also generated. They are implemented using Junit 4, Spring test and
Easy mock. Springfuse also generates test helper classes to create dummy domain classes.

## Dependency injection with Spring

The generated components use the <code>@Autowired</code> annotation for dependency injection to
simplify the Spring configuration. Note that you can still override through the Spring XML configuration.

## <a href="/why/annotations">Transactions with Spring</a>

We use the <code>@Transactional</code> annotation for transactions and as
the Spring team recommends we only annotate concrete classes and not interfaces.
We also use the Open Session In View Filter.

## <a href="/why/hibernate">Hibernate</a>

Bidirectional associations such as one-to-many/many-to-one, many-to-many are all supported.
We provide some helper methods to preserve the coherence at the memory level.

## <a href="/why/spring-security">Security</a>

Authorization and authentication is not hard coded in the project.
Instead the generated project uses Spring security filter or/and annotations.


## Logging

Each line of logs is contextual. It contains for example the current HTTP session id and
user login. This is done transparently for the developer thanks to log4j's
<i>Mapped Diagnostic Context</i>, an instrument for distinguishing interleaved log
output from different sources.

## Project Architecture

The application that Springfuse generates has a layered architecture. There is as you would expect,
a web layer, a service layer, an entity manager layer, a domain layer and a data layer.

These layers are well separated and organized into packages without cyclic dependencies.

Springfuse does not re-invent the wheel, the generated source code leverage existing Open source technologies.


# The Web Layer
##<a href="/why/spring-security">Spring Security</a>

Springfuse generates the required Spring Security configuration and an implementation of the
<code>UserDetailsService</code> that loads the account information using the
generated account entity manager. It also generates a login page and some convenient methods to
allow you to auto-login a user.

Spring Security can also be used in your code to prevent certain roles from executing
some methods thanks to the <code>@RolesAllowed</code> annotation.

## <a href="/why/spring-mvc">Spring MVC annotation-based Controllers</a>

The web layer leverage Spring MVC 3.0.2. 
All the generated controllers leverage the new Spring MVC annotation system, they use <code>@Controller</code>,
<code>@InitBinder</code>, <code>@RequestMapping</code>, <code>@ModelAttribute</code>.
For each domain class, Springfuse generates controllers that allow you to:

* Perform CRUD operations with validation
* Search for domain data with pagination
* Upload and download files


CRUD can become tricky to support when you have many-to-many relations, many-to-one relations, boolean, etc.
As you would expect, Springfuse covers all these cases gracefully.


When implementing your own business controllers, you can leverage the generated controller
either by extending them or simply by learning from the generated code. Note that various utility
classes are also generated to support the controller operations and can
be directly used to support your business controller.


## Validators

The domain layer is generated along with Hibernate Bean Validation annotations.
Springfuse also generates some basic Validators that leverage these annotations for each domain class.


## Views

Springfuse generates UTF-8 encoded JSP pages that use Spring tags and JQuery.
These JSP are fully functional.

However, we strongly recommend to do not modify the generated pages but instead create
your new JSP pages based on what
you learn in the generated pages. Generated pages can be used for basic administration purposes but it is
not Springfuse's primary goal.

## Localization

All the JSP pages are localized. We provide generic properties files for 2 locales : English and French.
You can easily switch from one locale to another thanks to some links in the generated page. Note that
we leverage here Spring's <code>LocaleChangeInterceptor</code>.

## Account Context Interceptor

Springfuse generates a <code>ContextInterceptor</code> which is responsible for binding on the
current thread of each incoming http request some contextual information.
For example, when the user is logged in, it binds the User model. This information is also binded
on the Spring MVC <code>Model</code> so it can be easily available from the JSP view.
This interceptor also enable some Hibernate filters, please refer to the main documentation.


## URL Rewrite

Springfuse generates a simple URL rewrite configuration.


# The Service Layer

This is the business layer that you code manually. But you do not start from scratch, you can use
within your service implementation the entity managers that are generated. Note that Springfuse generates
the following services. All service implementation are annotated with <code>@Service</code>.

## Password Service

This is a simple service to allow users to reset or change their password.
Upon password reset an email is sent to the end user.

## Email Service with Javamail and Velocity

Springfuse generates an Email sending interface and implementation that allows you to send
template-based email messages. Email can be sent synchronously or asynchronously.
It leverages JavaMail and Spring's <code>VelocityEngineUtils</code> class. Springfuse generates some velocity
templates for the reset password service, as you would expect the email service supports localization.

By default we provide a Javamail configuration ready to be used with Gmail, it uses SSL.


## Named Query Util Service

Springfuse generates a named query util service which can be used transparently through the entity
manager. You just have to write your named query in an xml file, set its in the SearchTemplate and pass it as
an argument to the corresponding entity manager. Note that this named query util support
dynamic 'order by' clauses as the entity manager.


# The Entity Manager Layer

The entity manager layers allow you to perform CRUD and search operations.
It is independent from the underlying data layer. For each domain classes Springfuse generates
an entity manager interface and implementation. The entity manager implementation uses a DAO
interface to make data call.


At first view, the various managers code looks pretty much alike. In practice, there are few
differences depending on your data model. We believe that having one implementation per
domain class keeps the code easier to maintain and understand.


# The DAO Layer

The implementation of the DAO layer is repository dependent. Springfuse generates generic
DAO interface and their implementation for JPA/Hibernate.
These DAO allow you perform the CRUD and search operations.
These DAOs only throws generic Spring unchecked exceptions.


Springfuse generates the configuration for database connection pooling,
2nd level caching, and distributed 2nd level caching with Ehcache.


# The Domain Layer

For each table in your database Springfuse generates a Domain class, a POJO.

Springfuse generates the corresponding JPA annotations including for Blob support, lazy loading and cache.


The following mapping are supported: one-to-many, many-to-one, many-to-many.
For each mapping Springfuse generates some
additional helper methods to preserve referential integrity.


Springfuse also supports one-to-one, but instead of using Hibernate one-to-one mapping, we use a one-to-many mapping and some
helper methods to prevent from adding more than one element in the collection. This simple trick allows you to leverage lazy loading.

Helper methods to manipulate files (i.e BLOB) are also generated.

