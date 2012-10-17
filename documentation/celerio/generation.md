---
layout: english
title: Celerio Guide - Code Generation
---

Code generation
===============

Principle
---------

The code generation step is performed by the `generate` goal of the
`maven-celerio-plugin` provided by Jaxio.

The code generation step is driven by several factors:

-   *The database meta data:* It serves as a main entry model. The
    various column's constraints such as `NOT NULL` , the foreign keys,
    etc. are exploited by Celerio in the code generation process.

-   *Celerio conventions:* Please refer to ?.

-   *Celerio configuration:* Please refer to ?.

-   *Celerio template packs:* Please refer to ?.

-   *Generated code modifications:* Please refer to ?.

![Source code generation is driven by several
factors](images/celerio-generation.png)

As for database schema extraction, the code generation step does not
need to be performed at each build. *To prevent useless generation* ,
the simplest approach is to declare a Maven profile dedicated to code
generation. As an example you can use the `pom.xml` that the Celerio
`bootstrap` goal produces.
