---
layout: english
title: Springfuse approach to code generation
comments: true
---

# Springfuse approach to code generation

One of the most interesting objections I ever received about code generation came from a woman who told me: 
	« Code generators are great, but only their creator can really use them. So at the end, they are useless ». 
That’s a point!

I think she is right, it is pretty hard to write a code generator that can be used by other people without having them to understand the ins and outs of the code generator itself.

You probably cannot create an easy to use code generator that produces exactly what you have in mind. 
It is a bit like the Heisenberg’s principle, you cannot get the exact position and speed of a particle at the same time… you have to choose your camp.

With SpringFuse, we made a clear choice. We choose the camp of simplicity. 
We sacrifice the possibility to configure extensively the generator to produce exactly what you want.

For example, we do not try to generate business code out of complex rules that tend to resemble to code! 
Instead SpringFuse uses existing database schema as an entry point.

The range of applications that could benefit from SpringFuse is therefore limited to database-oriented applications having a data model that fit roughly the business model. 
There are still many of them.

This bottom-up approach has an advantage: it leaves the developer in charge of the business layer. 
The generated code is just here to support the developer in his day to day job.
The developer keeps the control of the code that creates the real value for the end user.
Thanks to the generated code, the developer can spend more time on creating real value.

Of course the developer should understand the generated code to use it. 
There is no magical stuff here. 
But at least the code that SpringFuse generates is clean, well organized, with no cyclic dependencies. 
It uses many popular frameworks such as:
 
* Spring Framework, 
* Spring Security, 
* Spring MVC, 
* Hibernate, 
* etc… 

so understanding how this code works, is clearly an investment as all the technologies used are demanded by the industry.

That’s it for today!