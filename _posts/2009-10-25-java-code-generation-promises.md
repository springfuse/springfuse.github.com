---
layout: main
title: Java Code Generation Promises
comments: true
---

# Java Code Generation Promises

In the last months there has been some increasing interest for <a href="http://www.infoq.com/news/2009/09/codegen-java-development">Java code generation</a>.

However, code generation may be source of a great disappointment if you expect too much out of it.

In France, a politician said something like: “promises commit only those who believe in it” (I am unsure about the translation). 
Applied to code generation it becomes: if you believe all promises of code generation, it is your responsibility.
If you consider using code generation on your next project, you may be interested in checking the various points that drive us in the development of Celerio, the code generator that powers SpringFuse.


# The model

SQL is still predominant in this world. Many web applications are data-oriented and the database schema is the only model that is always up to date.
We have created Celerio especially for this kind of applications. So, it is natural for us to use the database schema as an entry model for the code generation. 
When the schema is not enough, for example to describe entity inheritance, we rely on a configuration file.
We could have taken a different path, starting from UML or Java Entities; but for the application we target, SQL + some configuration remain the most pragmatic model.

# Maintenance

In some many cases, an application is maintained by developers that were not part of the initial core team. 
To ease the maintenance, the code generation tool should be pragmatic, easy to learn, with as fewer bells and whistles as possible.

# Self training

The generated code should help the most junior developers to train themselves. The code should be clean, well organized, and documented. 
The generated code should not be considered as a black-box. 
At the end of a project, the developer should understand the ins and outs of the generated code and the underlying technologies it uses.
We have received many feedbacks from users who used SpringFuse to learn JPA, Spring MVC, Spring Security, Spring Web Flows, etc.

# Code generation templates

Developers should focus on the business code, not on writing the code generation templates.
Moreover the underlying technology is moving fast: one year you use hibernate, the next you support JPA, the next you move to JPA 2. 
Spring is out in 2.5, but version 3 is coming etc… Java ecosystem has not landed yet, it may never.
We write templates for the latest stable technologies as they are released and we support them. 
For example our next move will be supporting Spring 3.0 and part of EE6.

# Speed

Code generation phase should be almost transparent to the developers that generate-compile-deploy-debug often, even on large models.

# Over generating

The most difficult thing is to resist to the temptation of generating some code. As we progress with Celerio, we tend to generate less and less code. 
We also warn our users that parts of the code that Celerio generates are just meant for training/tutorial purposes (i.e. web UI code) or should be used as a copy-paste source.

# IDE

A code generation tool is just a tool. I believe it should not force you to use a specific IDE. 
Celerio is just a Maven2 plugin; it can run in a console mode, in Eclipse etc.

# Lock-in

The generated code should run without the code generation tool itself. 
Of course Celerio is not required at runtime and the generated code depends only on well known Open Source projects.

# Code generation round trip

The generated code manual modification should not be lost when regenerating. 
Celerio uses different techniques to preserve the user code (this could be the subject of a separated post).

# Conclusion

Code generation can be of great helps if you select the right tool for the right project, for the right team and if you know in advance what to expect from it.
Keep in mind that at the end, one of the most important features is simply the result, which is the generated code. So take the time to review it before selecting a tool. 
Make sure the generated code complies with your highest expectations in term of quality. 
Try to put yourself in a position where you would have to maintain this code manually or explain it to another team.
To ease the process of reviewing the code that Celerio generates, we have created <a href="http://www.springfuse.com/">SpringFuse</a>. Developers can use this service to generate a project in less than 15 minutes. 
The result is a zip file that contains the generated source code organized into a Maven2 project. 

Have fun!