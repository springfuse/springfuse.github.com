---
layout: main
title: Generate Spring MVC3, JQuery, JPA2 CRUD Application
comments: true
---
<link rel="stylesheet" href="http://tom.preston-werner.com/css/syntax.css" type="text/css" />
# 5 may 2011 - Generate Spring MVC3, JQuery, JPA2 CRUD Application

We are pleased to announce some major improvements in the Spring MVC application that SpringFuse generates.

As usual, you can generate the application from <a href="/">SpringFuse quickstart page</a>.

One of the top 40 company in France is already running an application generated with this version. Their application's database schema has over 50 tables.

# Look & Feel

Instead of using our home grown stylesheets, the generated application now uses <a href="http://www.blueprintcss.org/">Blue Print CSS</a>.

It also uses <a href="http://jqueryui.com/">jQuery UI</a> 1.8.11

The generated application look'n' feel is much easier to maintain.

# Navigation

We now provide navigation for all JPA associations. It allows you to easily browse though the entity graph and update the associated entities. 
Here is a screenshot of the 'Account' entity page from the sample application:

You can follow the 5 different associations:

* many-to-many for the Roles
* many-to-one for the Address
* inverse one-to-one for the Contact Info
* one-to-many for the books
* one-to-many for the documents, mostly here to illustrate file upload/download

<a href="/images/blog/2011-05-04/mvc-account-ajax.png" class="screen" title="New navigation" rel="group"><img src="/images/blog/2011-05-04/mvc-account-ajax-min.png" /></a>

# Auto complete instead of select box

To set a many to one association, you can configure Celerio to use auto-complete (ajax) instead of displaying all the possible target in a select list box. 
In the screenshot below, we set the linked address using auto-complete:

<a href="/images/blog/2011-05-04/mvc-account-ajax.png" class="screen" title="New navigation" rel="group"><img src="/images/blog/2011-05-04/mvc-account-ajax-min.png" /></a>

# Joda Time

You can configure Celerio to use Jodatime instead of java.util.Date. Here is an example of generated java code and a screen shot:

{% highlight %}
	@Column(name = "date_joda", length = 8)
	@Type(type = "org.joda.time.contrib.hibernate.PersistentLocalDate")
	@DateTimeFormat(iso = ISO.DATE)
	public LocalDate getDateJoda() {
	    return dateJoda;
	}
	
	public void setDateJoda(LocalDate dateJoda) {
	    this.dateJoda = dateJoda;
	}
	
	@Column(name = "date_time_joda", length = 23)
	@Type(type = "org.joda.time.contrib.hibernate.PersistentLocalDateTime")
	@DateTimeFormat(iso = ISO.DATE)
	public LocalDateTime getDateTimeJoda() {
	    return dateTimeJoda;
	}
	
	public void setDateTimeJoda(LocalDateTime dateTimeJoda) {
	    this.dateTimeJoda = dateTimeJoda;
	}{% endhighlight %}

<a href="/images/blog/2011-05-04/mvc-joda.png" class="screen" title="Joda time integration" rel="group"><img src="/images/blog/2011-05-04/mvc-joda-min.png" /></a>

