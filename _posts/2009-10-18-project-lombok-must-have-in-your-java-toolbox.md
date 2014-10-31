---
layout: english
title: Project lombok - a must have in your java toolbox !
comments: true
---

# Project lombok - a must have in your java toolbox !

What you'll read in this post:

* using eclipse to write POJO
* using eclise and commons-lang to write POJO
* using lombok to write POJO
* a maven project with working examples

Get the code directly <a href="https://github.com/springfuse/project-lombok-example">on github</a> ! 

## ProjectLombok is my new technical friend

Today I would like to share with you my new technical companion: <a href="http://projectlombok.org/">projectlombok</a>.

## What is lombok

ProjectLombok like <a href="http://www.springfuse.com">Springfuse</a> is a code generator, and I very much like code generators as they make my life easier. 
Where springfuse is producing working knowledge spanning many technologies, project lombok produces simple code to bypass java excessive verbosity. 
Project lombok is generating : 

* <a href="http://projectlombok.org/features/GetterSetter.html">setter</a>
* <a href="http://projectlombok.org/features/GetterSetter.html">getter</a>
* <a href="http://projectlombok.org/features/ToString.html">toString</a>
* <a href="http://projectlombok.org/features/EqualsAndHashCode.html">equals</a>
* <a href="http://projectlombok.org/features/EqualsAndHashCode.html">hashcode</a>
* see the <a href="http://projectlombok.org/features/index.html">other features</a>
 
While reading this you should think that eclipse does it for you already since... for ever.

<div id="screen"> 
<a href="/images/blog/2009-10-18/toString.png" class="screen" title="toString" rel="group"><img src="/images/blog/2009-10-18/toString-min.png" /></a>
<a href="/images/blog/2009-10-18/hashcode.png" class="screen" title="Hashcode" rel="group"><img src="/images/blog/2009-10-18/hashcode-min.png" /></a>
<a href="/images/blog/2009-10-18/getter-setter.png" class="screen" title="Getters and setters" rel="group"><img src="/images/blog/2009-10-18/getter-setter-min.png" /></a>
</div>
  
You could also tell me that I should use a real language like <a href="http://www.scala-lang.org/">scala</a> or a dynamic language like <a href="http://groovy.codehaus.org/">groovy</a>.


## The problem

Well they could be ideal solutions, but like so many I have no choice but to stick with java.

* Should we really rely on our IDE to generate this kind of code ?
* Should we really have to see all these methods clutter our code ?
* Should we really need to loose time and focus to manually verify that our hashcode, equals, toString methods are in sync ?
* Come on, our time is precious, and this really totally dumb, and error prone ! 

<u>But there should not be this problem to solve in the first place !</u>

## WRITING ALL THESE METHODS MANUALLY

I used to write them manually while using emacs back in the 2000 days, let's skip these painful memories...

## A LITTLE HELP FROM ECLIPSE

We all know how to generate all these methods using eclipse, but I had the curiosity for this post to count the number of steps to generate them:

1. click Source 
2. click generate getter & setter 
3. click Select all
4. click Ok
5. click Source
6. click generate to String
7. click Ok
8. Click Source
9. click generate hashcode and equals
10. click Ok
11. I tidy up things


That’s 11 steps ! 


Ok, now it’s time to do some eclipse magic and bind "generate setter/getter" to a shortcut. 

That’s right, <a hred="http://wiki.eclipse.org/FAQ_How_do_I_provide_a_keyboard_shortcut_for_my_action%3F">no big deal</a>. 
But sounds like an ugly solution isn’t it?
 
<i>And I insist, this problem should not exist in the first place !</i> 

So you end up with :

{% highlight java %}
	package com.springfuse.blog.projectlombok;
	
	public class UsingEclipse {
		private String not;
		private String really;
		private String fun;
	
		@Override
		public int hashCode() {
			final int prime = 31;
			int result = 1;
			result = prime * result + ((fun == null) ? 0 : fun.hashCode());
			result = prime * result + ((not == null) ? 0 : not.hashCode());
			result = prime * result + ((really == null) ? 0 : really.hashCode());
			return result;
		}
	
		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			UsingEclipse other = (UsingEclipse) obj;
			if (fun == null) {
				if (other.fun != null)
					return false;
			} else if (!fun.equals(other.fun))
				return false;
			if (not == null) {
				if (other.not != null)
					return false;
			} else if (!not.equals(other.not))
				return false;
			if (really == null) {
				if (other.really != null)
					return false;
			} else if (!really.equals(other.really))
				return false;
			return true;
		}
	
		@Override
		public String toString() {
			return "UsingEclipse [fun=" + fun + ", not=" + not + ", really=" + really + "]";
		}
	
		public String getNot() {
			return not;
		}
	
		public void setNot(String not) {
			this.not = not;
		}
	
		public String getReally() {
			return really;
		}
	
		public void setReally(String really) {
			this.really = really;
		}
	
		public String getFun() {
			return fun;
		}
	
		public void setFun(String fun) {
			this.fun = fun;
		}
	
	}
{% endhighlight %}

Basically the usual pojo suspect you see everywhere ...


## Some help from commons-lang

<a href="http://commons.apache.org/lang">Commons-lang</a> is giving simple and effective solutions to reduce the boilerplate code with 

* <a href="http://commons.apache.org/lang/api/org/apache/commons/lang/builder/EqualsBuilder.html">EqualsBuilder</a>
* <a href="http://commons.apache.org/lang/api/org/apache/commons/lang/builder/ToStringBuilder.html">ToStringBuilder</a>
* <a href="http://commons.apache.org/lang/api/org/apache/commons/lang/builder/HashCodeBuilder.html">HashCodeBuilder</a>
 
So you have now only the getter and setter to generate with eclipse and no more need to worry about your equals/hashcode methods. 

You should now have this:

{% highlight java %}
	package com.springfuse.blog.projectlombok;
	
	import org.apache.commons.lang.builder.EqualsBuilder;
	import org.apache.commons.lang.builder.HashCodeBuilder;
	import org.apache.commons.lang.builder.ToStringBuilder;
	
	public class UsingCommonsLang {
		private String not;
		private String really;
		private String fun;
	
		public String getNot() {
			return not;
		}
	
		public void setNot(String not) {
			this.not = not;
		}
	
		public String getReally() {
			return really;
		}
	
		public void setReally(String really) {
			this.really = really;
		}
	
		public String getFun() {
			return fun;
		}
	
		public void setFun(String fun) {
			this.fun = fun;
		}
	
		@Override
		public int hashCode() {
			return HashCodeBuilder.reflectionHashCode(this);
		}
	
		@Override
		public boolean equals(Object obj) {
			return EqualsBuilder.reflectionEquals(this, obj);
		}
	
		@Override
		public String toString() {
			return ToStringBuilder.reflectionToString(this);
		}
	}
{% endhighlight %}

This is better, less error prone, but we still still have so many getter/setters that we can’t stand.


## Lombok comes and wins

Now look how we do it using lombok:

{% highlight java %}
	package com.springfuse.blog.projectlombok;
	
	import lombok.Data;
	
	@Data
	public class UsingProjectLombok {
		private String get;
		private String fun;
		private String back;
	}
{% endhighlight %}

Isn't it elegant ? 

<div id="screen"> 
<a href="/images/blog/2009-10-18/outline-simple.png" class="screen" title="outline" rel="group"><img src="/images/blog/2009-10-18/outline-simple-min.png" /></a>
</div>


The <a href="http://projectlombok.org/features/Data.html">@Data</a> does express my intention nicely ... and completely as the code is also generated. 
After the shock of such a concise POJO, the next though you have is for configuration ... 
Projectlombok gives you this freedom.

{% highlight java %}
	package com.springfuse.blog.projectlombok;
	
	import lombok.EqualsAndHashCode;
	import lombok.Getter;
	import lombok.Setter;
	import lombok.ToString;
	
	@EqualsAndHashCode(exclude = { "get" })
	@ToString(exclude = { "get" })
	public class UsingProjectLombokWithConfiguration {
		protected String get;
		@Getter
		private String fun;
		@Getter
		@Setter
		private String back;
	
		public UsingProjectLombokWithConfiguration(String get, String fun, String back) {
			this.get = get;
			this.fun = fun;
			this.back = back;
		}
	}
{% endhighlight %}


Please note that Lombok is a good citizen as it gives you clear warnings.

<div id="screen"> 
<a href="/images/blog/2009-10-18/outline-configured.png" class="screen" title="outline configured" rel="group"><img src="/images/blog/2009-10-18/outline-configured-min.png" /></a>
<a href="/images/blog/2009-10-18/smart.png" class="screen" title="Smart messages" rel="group"><img src="/images/blog/2009-10-18/smart-min.png" /></a>
</div>

## How does it work ?

Project lombok is a javac plugin that will use the javac 6 annotation processor. 
That means that the generation of the methods is part of the compilation, and no runtime nor java agent is required ! 
It's almost like adding behavior with aspectj but with plain java !

## Lombok and maven

Using lombok and maven is straightforward:
 
{% highlight xml %}
	<dependency> <!-- Will be picked by javac -->
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>0.8.5</version>
		<scope>provided</scope>
	</dependency>
	...	
 	<repositories>
		<repository> <!-- project lombok is not yet in public maven repo -->
			<id>projectlombok.org</id>
			<url>http://projectlombok.org/mavenrepo</url>
		</repository>
	</repositories>
	...	
	<plugins>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>2.3.2</version>
			<configuration>
				<compilerVersion>1.6</compilerVersion>
				<source>1.6</source>
				<target>1.6</target>
			</configuration>
		</plugin>
	</plugins>
{% endhighlight %}
 
 
## Lombok and eclipse

Execute the lombok.jar and specify your eclipse folder it will add itself or add manually in eclipse.ini the botclasspath and javaagent like this

	-javaagent:lombok.jar
	-Xbootclasspath/a:lombok.jar

	
## Constraints

### javac 1.6

Lombok does work only under javac 1.6, but if you want to target 1.5 just configure it in your pom. 
But JDK 1.5 has 10 more days before it is no more supported by sun ! 
It is time to give this info to your boss and make the switch.

### Eclipse refactoring

The current version 0.8.5 does not work great in this regard, however they fixed it in the trunk. 
If you do build your own, you'll be fine

	git clone git://github.com/rzwitserloot/lombok.git
	ant
... or wait for the next binary release ! 

Edit: the 0.9 release is out

### Netbean support
It's in the way


### Do not abuse
Lombok generates other methods like @Cleanup, @Synchronized, @SneakyThrows or @Logger. 
I am not sure what to think about these, maybe it could go too far but as the intent is clearly described via the annotation, why not... 
Anyway I'll stick with the simple features for now and see how it goes.

## I love this tool !

I have to say, that the combination of google collections and project lombok gave me a fresh view of what you can accomplish with java. 
It feels like the gap between the language "du jour" and my plain old java has been dramatically reduced. 
And you know what ? 

It feels good !
