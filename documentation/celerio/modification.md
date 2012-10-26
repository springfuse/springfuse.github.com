---
layout: english
title: Celerio Guide - Code modification, regeneration and collisions
---

Code modification, regeneration and collisions
==============================================

Introduction
------------

One of the most important feature of a code generator is its ability to
preserve manual code modifications across re-generations. To solve this
challenge, Celerio proposes various pragmatic solutions depending on the
nature of the generated file.

Manual Modification Detection
-----------------------------

Celerio keeps track of all the file it generates in the file `.celerio/generated.xml`.
Do not commit this file to your Source Control System as it is different for each developer.

Each time Celerio regenerates a file it checks first if the file has been modified since the last generation.
`If yes`, Celerio takes no risk, it generates the file in the collision folder (details are provided further).
`If no`,   Celerio replaces the file with the new generated content.

Note that if the generated file has the same content as the old one, Celerio does not regenerate it in order to preserve the file's timestamp.

> ** Important **
> 
> If you delete the `.celerio/generated.xml file` Celerio has no way to determine if a file has been manually modified or not and you may loose 
> your modifications unless the file has been committed to your Source Control System.


Java files
----------

By default, Celerio generates the main Java file under the directory
`${maven-celerio-plugin.outputDir}/src/main/generated-java` or `${maven-celerio-plugin.outputDir}/src/main/java`
depending on Celerio's outputDir [Please refer to Code Generation chapter](generation.html)

In this section you will learn how to modify a generated Java file
without loosing your modifications. The first approach consists 
simply in moving the file to ${baseDir}/src/main/java. 

The second approach involves inheritance of a base class. Both approaches have pros and cons.

> **Important**
>
> In any case, you should avoid to modify directly the generated Java file
> as you may loose your changes as soon as you regenerate the code.

### Moving the file to ${baseDir}/src/main/java

Before modifying the generated Java file, move it to the `${baseDir}/src/main/java`
folder. For example, if you want to edit the generated
`BankAccount.java` file, move it from

__if outputDir equals baseDir__
`src/main/generated-java/<package path>/BankAccount.java` to
`src/main/java/<package path>/BankAccount.java`

__if outputDir different from baseDir__
`${maven-celerio-plugin.outputDir}/src/main/java/<package path>/BankAccount.java` to
`${baseDir}/src/main/java/<package path>/BankAccount.java`

> **Note**
>
> When copying the file you must use the same relative path.

Since all the files under the `${baseDir}/src/main/java` are considered as user
reserved files, Celerio will not interfere with them. Next time you run
Celerio, Celerio will detect the presence of BankAccount.java under
`${baseDir}/src/main/java/<package path>`, leave it untouched, and will not
generate it here.

The `main advantage` of this approach is that, you now can do whatever you
want with the file, in particular you can modify any method's body etc.

The `main drawback` may show up if your database schema changes. You may
have to reflect those changes manually in the file that you now own as a regular
file. Hopefully, to help you in this task, Celerio generates the file in
a dedicated collision folder under the `target` folder. Please refer to
[Collisions and merging](#collisions-merging) section.

### Code modifications through 'Base' inheritance

Celerio enables you to extend a generated Java class without modifying
the generated Java code.

Let’s take an example with the `Account` entity which maps the `Account`
table of our database schema example.

Let's assume the generated `Account` source file is located at
`${maven-celerio-plugin.outputDir}/src/main/(generated-)java/com/example/demo/domain/Account.java` 

It looks
like this:

{% highlight java %}
package com.example.demo.domain;
@Entity
@Table(name = "ACCOUNT")
public class Account implements Serializable {
    //...   
    private String firstName;
    private String lastName;
    //... skipped for clarity
}
{% endhighlight %}

Let’s assume you want to use a single method call to get
the full name of the user. One solution would be to add the following
method to the Account class:

{% highlight java %}
public String getFullName() {
	return getFirstName()+ " " + getLastName();
}
{% endhighlight %}

Instead of adding this method in the generated file, where it would be
mixed with generated code and potentially overwritten, Celerio supports another solution that
enables you to extend the generated class of you choice and at the same
time preserve the same class name.

This technique has three major benefits:

* No need to modify the existing files (Java, xml, etc.) that reference the 
  Java class that you want to extend.
* The hand written code is isolated in a separated class, in a separated 
  file, which greatly improves the clarity of your code.
* The generated files can be overwritten by Celerio to take into account your most recent Database schema changes. 

Best way to understand how it works is to try it:

Create a new `Account.java` file and save it in the folder:
`${baseDir}/src/main/java/com/example/demo/domain`

> **Note**
>
> Note that the new Account.java must be in the same package as the old one.

At this stage, we have exactly 2 Account classes, which is forbidden by Java.
Let's continue, you will see how Celerio fixes this.
 
Open the newly created `Account.java` file and copy paste the following
code:

{% highlight java %}
package com.example.demo.domain;

@Entity
@Table(name = "ACCOUNT")
public class Account extends AccountBase implements Serializable {
    public String getFullName() {
        return getFirstName()+ " " + getLastName();
    }
}
{% endhighlight %}

This `Account` class now extends a class that does not exist yet!

Next time you run Celerio, it will detect your new `Account.java` file
and will also detect that the `Account` class extends a class that has
the same name plus the `Base` suffix.

This is enough for Celerio to assume that you want to impersonate the
class and that it should generate the code corresponding to the Account
table in a class called `AccountBase` instead of a class called
`Account` .

The source code of `AccountBase` is generated in the file
`${maven-celerio-plugin.outputDir}/src/main/(generated-)java/com/example/demo/domain/AccountBase.java` .
Since this class is an entity, the class level annotations that were
present on the original Account class must copied to your own Account
class. Hopefully if you read the source code of the 'Base' class, you
will find these annotations in the comments. Here is how a snapshot of the generated
AccountBase code.

{% highlight java %}
@MappedSuperclass
/* Copy paste these annotations as is in your subclass
@Entity
@Table(name = "ACCOUNT")
*/
public abstract class AccountBase implements Serializable {
    // code skipped for concision
}
{% endhighlight %}

As you can notice the `@MappedSuperclass` is properly generated and the
other annotations are commented. Also the base class is made abstract to
prevent you from instanciating it .

> **Note**
>
> Always check the source code of the 'Base' class, you may find some
> instructions related to some annotations that must be added to your
> class.

During the generation process, if Celerio encounters the old 
`${maven-celerio-plugin.outputDir}/src/main/(generated-)java/com/example/demo/domain/Account.java` 
file, it deletes it to prevent class duplication.

You can proceed by analogy to override other Java classes.

Other files (non-Java) when baseDir equals Celerio's outputDir
-----------------------------------------------------------------

Ideally all generated files should be under a `generated` folder. In
practice, this is not really convenient or possible as certain files are
expected to be in a well known location (ex: `web.xml` )

If possible and pertinent, we keep the generated files under a
generated folder. This is specially useful for entity bound files as
there could be a lot of them.

This strategy is currently used for generated Spring Web Flow xhtml files, they are
generated under `src/main/webapp/WEB-INF/flows-generated`. 
Do not modify the generated flows, instead simply copy the files you need under
`src/main/webapp/WEB-INF/flows` and then modify the copied version.
By configuration, Spring Web Flow will first look up a flow by id in the
`src/main/webapp/WEB-INF/flows` user's reserved folder.

### Take ownership of a generated file

In order to tell Celerio to do not overwrite a generated file, you must add this file to your source control system.

Next time Celerio runs, it will detect that your file is under source
control and will not overwrite it.

In a sense, the code generation is frozen for this file: Celerio does not
control it anymore, it is under your control.

Since you may be interested in the file Celerio would have generated if you had not added your file to your Source Control System, Celerio generates it under the `target`
folder. Please refer to [Collisions and merging](#collisions-merging) section.

If you change your mind and want Celerio to generate the file again,
simply remove the file from your source control and regenerate your
code.

#### Generation rule summary for non-java file (baseDir == outputDir)

Before generating a non-java file, Celerio applies the following rules:

<table class="table">
	<tfoot>
		<tr>
			<td colspan="4">Generations rule summary for non-java file (baseDir same as Celerio's outputDir)</td>
		</tr>
	</tfoot>	
	<tr>
		<th>File is already present on disk</th>
		<th>File is under source control</th>
		<th>Generated file would be the same </th>
		<th>Celerio action</th>
	</tr>
	<tr>
		<td>No</td>
		<td>n/a</td>
		<td>n/a</td>
		<td>File is generated</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>Yes</td>
		<td>No</td>
		<td>File is generated in the collision folder</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>No</td>
		<td>No</td>
		<td>File is overwritten if it was not manually modified. Otherwise, it is generated in the collision folder</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>Yes</td>
		<td>Yes</td>
		<td>File is not generated</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>No</td>
		<td>Yes</td>
		<td>File is not generated</td>
	</tr>
</table>


Other files (non-Java) when baseDir is different from Celerio's outputDir
-------------------------------------------------------------------------

In the case when baseDir is different from Celerio's outputDir, all is much simpler as
by definition all the files present under the ${baseDir} folder cannot be overwritten by Celerio.

If you want to take ownership of a file, let's say the web.xml file, you should simply move the file from
the ${maven-celerio-plugin.outputDir} to the ${baseDir}. In this process you should preserve the file's relative path.

For example move:

* ${maven-celerio-plugin.outputDir}/src/main/webapp/WEB-INF/web.xml to
* ${baseDir}/src/main/webapp/WEB-INF/web.xml

Once you re-run Celerio, it will detect the file under ${baseDir} and therefore will no longer generate it in the ${maven-celerio-plugin.outputDir}.
Instead, it will generate it in the collision folder.  Please refer to [Collisions and merging](#collisions-merging) section.

#### Generation rule summary for non-java file (baseDir =/= outputDir)

Before generating a non-java file, Celerio applies the following rules:

<table class="table">
	<tfoot>
		<tr>
			<td colspan="4">Generations rule summary for non-java file (baseDir different from Celerio's outputDir)</td>
		</tr>
	</tfoot>	
	<tr>
		<th>File is present under baseDir</th>
		<th>Generated file would be the same </th>
		<th>Celerio action</th>
	</tr>
	<tr>
		<td>No</td>
		<td>n/a</td>
		<td>File is generated under outputDir</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>No</td>
		<td>File is generated in the collision folder</td>
	</tr>
	<tr>
		<td>Yes</td>
		<td>Yes</td>
		<td>File is not generated</td>
	</tr>
</table>


<a name="collisions-merging"></a>

Collisions and Merging
----------------------

### Collision folder

When Celerio detects that a file which should be generated is already
present and under source control or manually modified, it does not overwrite your file. 
Instead, Celerio generates the files in conflict in the *collision folder*: `target/maven-celerio-plugin/collisions`

All files generated in that folder have the same path as if they had
been generated normally, except for the
`target/maven-celerio-plugin/collisions` path prefix.

So, whenever appropriate, Celerio generates the original file, under the
expected path, in the collision folder
`target/maven-celerio-plugin/collisions`

### Merging manually the files

To merge the files in conflict, you can use a tool such as WinMerge.

Since, the files that led to some conflict are located in the collision
folder under the same relative path, you can use the recursive directory
comparison feature.

To do so, you just have to specify in WinMerge, your project root
directory and the collision directory

Then, you can keep track of changes you made and eventually merge some
of the newly generated code into your existing file.

#### Merging Tools

* [WinMerge](http://winmerge.org/)
* [Araxis Merge](http://www.araxis.com/merge/)
