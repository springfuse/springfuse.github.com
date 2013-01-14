---
layout: english
title: Celerio Guide - Writing templates
---

Writing Celerio Templates
=========================

Templates source folder
-----------------------

In celerio-templates-packs.xml declare your celerio template source folder using the template pack element.
For example:

{% highlight xml %}
<packs>
	<!-- ... other packs skipped... -->
	<pack name="pack-custom" path="src/main/celerio" enable="true" />
</packs>
{% endhighlight %}

In the above example, Celerio considers any file present under 'src/main/celerio' and its subfolder as a template.

Template name convention
------------------------

There are several kinds of template:

### Per entity template

A 'per entity template' is interpreted for each entity.
Its name must have this form: `TemplateName.e.vm.ext` where:

* TemplateName is a logical name for your template. It is not used by Celerio.
* e stands for entity.
* vm means the templates is written in Velocity.
* ext is your file extension. It is used by Celerio.

Example: `Controller.e.vm.java`

### Per projet template

A 'per project template' is interpreted one time per projet.
Its name must have this form: `TemplateName.p.vm.ext` where:

* p stands for project.

### Per enum template

A 'per enum template' is interpreted for each enum.
Its name must have this form: `TemplateName.enum.vm.ext`

### Per composite primary key template

A 'per composite primary key template' is interpreted for each composite primary key.
Its name must have this form: `TemplateName.cpk.vm.ext` where:

* cpk stands for composite primary key

### Static files

Static files are not interpreted, they are just copied as is by Celerio.

Exemple: `afolder/img.gif` would be copied to `yourProjectRootFolder/afolder/img.gif` 


Writing a new Template
----------------------

### Writing a new 'per entity' Java template

**Let's assume that:**

* you want to create for each entity an Access Control List class.
* each ACL class should be named EntityNameAcl
* each class should be located under the security sub package

**Here is the template code:**

{% highlight java %}
$output.java($entity.acl)##

package $entity.acl.packageName;

public class $output.currentClass {
    // var: $entity.acl.var
    // type: $entity.acl.type
    // fullType: $entity.acl.fullType
    // package: $entity.acl.packageName
	// type: $entity.acl.type
	// path: $entity.acl.path
	// packageName: $entity.acl.packageName
	// fullType: $entity.acl.fullType
	// var: $entity.acl.var
	// varUp: $entity.acl.varUp
	// vars: $entity.acl.vars
	// varsUp: $entity.acl.varsUp
	// adder: $entity.acl.adder
	// adders: $entity.acl.adders
	// contains: $entity.acl.contains
	// getter: $entity.acl.getter
	// getters: $entity.acl.getters
	// remover: $entity.acl.remover
	// removers: $entity.acl.removers
	// setter: $entity.acl.setter
	// setters: $entity.acl.setters
	// editer: $entity.acl.editer
}
{% endhighlight %}

The 'acl' entity's property implements Celerio's `Namer` Interface.
The `Namer` interface exposes simple getter methods to access var name, getter name, etc...

Before running Celerio with the above template, you must first create the 'acl' Namer.
To do so, open the celerio-templates-packs.xml file and add the following `celerioTemplateContext` element:

{% highlight xml %}
<packs>
	<celerioTemplateContext>
		<entityContextProperties>
			<entityContextProperty property="acl" subPackage="security" suffix="Acl"/>
		</entityContextProperties>			
	</celerioTemplateContext>

	<!-- ... other packs skipped... -->
	<pack name="pack-custom" path="src/main/celerio" enable="true" />
</packs>
{% endhighlight %}

### Existing entity's namer properties

By default Celerio has some built-in namers. Theses can be used from your entity templates:

<table class="table">
	<tfoot>
		<tr>
			<td colspan="4">Entity's namer properties</td>
		</tr>
	</tfoot>
	<tbody>	
	<tr>
		<th>property name</th>
		<th>description</th>
	</tr>
	<tr>
		<td>dao</td>
		<td>Namer for the entity Dao Interface</td>
	</tr>
	<tr>
		<td>dao</td>
		<td>Namer for the entity Dao Implementation</td>
	</tr>
	<tr>
		<td>repository</td>
		<td>Namer for the entity Repository Implementation</td>
	</tr>
	<tr>
		<td>controller</td>
		<td>Namer for the entity Controller Implementation</td>
	</tr>
		<td>...</td>
		<td>...</td>
	</tr>
	</tbody>
</table>	

 



