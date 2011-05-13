---
layout: english
title: Testing various equals and hashCode strategies
comments: true
---

# Testing various equals and hashCode strategies

Equality in Java and in particular when working with Hibernate/JPA is a tricky subject. 
You will find in this post a simple Java project with some unit tests that illustrate the importance of overriding the equals() and hashCode() methods.
The project has a User entity with pluggable equals/hashCode implementations. 
Of course this design is only meant for testing different equals/hashCode implementations against the same unit tests.
Running the tests and seeing them fail or succeed depending on the equals/hashCode strategy used is a fun and easy way to learn and remember the importance of overriding equals/hashCode.
Note that the subject of identity is extensively covered 

* in "Item 9" of <a href="http://java.sun.com/docs/books/effective/">Effective Java second Edition</a> 
* and in chapter 9 of <a href="http://www.manning.com/bauer2/">Java Persistence with Hibernate</a>. 

Both books are must read.


Here is a preview of the kind of equals/hashCode tests you are going to find in the project:

{% highlight java %}
	 @Test
	 public void reflexive() {
	  User x = newUser(1, "x");
	  assertTrue(x.equals(x));
	 }
	
	 @Test
	 public void logicalEquality() {
	  User x1 = newUser(1, "x", "yellow");
	  User x2 = newUser(1, "x", "yellow");
	
	  assertTrue(x1.equals(x2) && x2.equals(x1));
	
	  // consistent
	  x1.setFavoriteColor("red");
	  x2.setFavoriteColor("blue");
	  assertTrue(x1.equals(x2) && x2.equals(x1));
	
	  x2.setId(2);
	  x2.setUsername("x2");
	  assertFalse(x1.equals(x2));
	 }
	
	 @Test
	 public void entityInSet() {
	  Set<User> set = new HashSet<User>();
	  set.add(newUser(1, "x"));
	  set.add(newUser(1, "x"));
	  assertEquals(1, set.size());
	 }
	
	
	 @Test
	 public void differentManagersReturnSameEntity() {
	  UserManager um1 = new UserManager(this);
	  UserManager um2 = new UserManager(this);
	
	  Set<User> set = new HashSet<User>();
	  set.add(um1.getUser(1));
	  set.add(um2.getUser(1));
	
	  assertEquals(1, set.size());
	 }
{% endhighlight %}
	 
Etc..

You can download the simple equal/hashCode project <a href="https://github.com/springfuse/java-identity-strategies">on github</a>. 
Clone itlocally and import it in your IDE as a Maven project. You may also run directly the unit tests from a command line (mvn test).
Once imported, for example in Eclipse, you can run the Junit tests.


# RUNNING THE TESTS WITH THE DEFAULT EQUALS/HASHCODE IMPLEMENTATION

Run as a junit test the DefaultUserIdentityTest class. You should have the following result :

<img src="/images/blog/2009-10-11/default.png">

As you can see most of the tests fail. The following logical identity test is not satisfied as you can expect.

{% highlight java %}
	 @Test
	 public void logicalEquality() {
	  User x1 = newUser(1, "x", "yellow");
	  User x2 = newUser(1, "x", "yellow");
	
	  assertTrue(x1.equals(x2) && x2.equals(x1));
	
	  // consistent
	  x1.setFavoriteColor("red");
	  x2.setFavoriteColor("blue");
	  assertTrue(x1.equals(x2) && x2.equals(x1));
	
	  x2.setId(2);
	  x2.setUsername("x2");
	  assertFalse(x1.equals(x2));
	 }
{% endhighlight %}

The default equals implementation is not sufficient. Let’s use a strategy based on the primary key that is the id property and see what happens.
RUNNING THE TESTS WITH AN EQUALS/HASHCODE STRATEGY USING THE PRIMARY KEY

Run as a junit test the IdUserIdentityTest class.
package com.springfuse.blog.identity;

{% highlight java %}
	import java.io.Serializable;
	
	import org.apache.commons.logging.Log;
	import org.apache.commons.logging.LogFactory;
	
	/**
	 * equals/hashCode strategy using the User primary key, the id property.
	 */
	public class IdEqualsStrategy implements EqualsStrategy, Serializable {
	 static private final long serialVersionUID = 1L;
	 static final private Log logger = LogFactory.getLog(IdEqualsStrategy.class);
	
	 private User user;
	
	 public IdEqualsStrategy(User user) {
	  this.user = user;
	 }
	
	 public boolean doEquals(User other) {
	  return user.getId() != null ? user.getId().equals(other.getId()) : false;
	 }
	
	 public int doHashCode() {
	  if (user.getId() != null) {
	   return user.getId().hashCode();
	  } else {
	   logger.warn("TODO: developer your code is not safe regarding hashCode", new Exception("stack trace"));
	   return System.identityHashCode(user);
	  }
	 }
	}
{% endhighlight %}
	
You should have the following result:

<img src="/images/blog/2009-10-11/id.png">

Almost all the tests pass now, except the one below:

{% highlight java %}
	 @Test
	 public void setIdAfterAddingEntityInSetAndTryToRemoveIt() {
	  Set<User> set = new HashSet<User>();
	  User x = newUser("x");
	  set.add(x);
	  x.setId(1);
	  set.remove(x);
	
	  assertEquals(0, set.size());
	 }
{% endhighlight %}

You may not encounter this scenario everyday, but with hibernate you might, for example when using saveOrUpdate(user). 
Imagine, if the user is added a Set before being saved in the database, you fall into this scenario. 
This lead us to use instead a "business key", that is a property or a set of properties that is unique, 
  not null and rarely or never change and known before inserting the entity in the Set and in the database.

RUNNING THE TESTS WITH AN EQUALS/HASHCODE STRATEGY USING A BUSINESS KEY

Run as a junit test the UsernameUserIdentityTest class.

{% highlight java %}
	package com.springfuse.blog.identity;
	
	import java.io.Serializable;
	
	import org.apache.commons.logging.Log;
	import org.apache.commons.logging.LogFactory;
	
	/**
	 * equals/hashCode strategy using a business key, the username property.
	 */
	public class UsernameEqualsStrategy implements EqualsStrategy, Serializable {
	 static private final long serialVersionUID = 1L;
	 static final private Log logger = LogFactory.getLog(UsernameEqualsStrategy.class);
	
	 private User user;
	
	 public UsernameEqualsStrategy(User user) {
	  this.user = user;
	 }
	
	 public boolean doEquals(User other) {
	  return user.getUsername() != null && user.getUsername().length() > 0 ? user.getUsername().equals(other.getUsername()) : false;
	 }
	
	 public int doHashCode() {
	  if (user.getUsername() != null && user.getUsername().length() > 0) {
	   return user.getUsername().hashCode();
	  } else {
	   logger.warn("TODO: developer your code is not safe regarding hashCode", new Exception("stack trace"));
	   return System.identityHashCode(user);
	  }
	 }
	}
{% endhighlight %}

You should have the following result :
	
<img src="/images/blog/2009-10-11/username.png">

All the tests pass now :-)

Note that the doHashCode() methods warns the developer if the username is not set.

{% highlight java %}
	 public int doHashCode() {
	  if (user.getUsername() != null && user.getUsername().length() > 0) {
	   return user.getUsername().hashCode();
	  } else {
	   logger.warn("TODO: developer your code is not safe regarding hashCode", new Exception("stack trace"));
	   return System.identityHashCode(user);
	  }
	 }
{% endhighlight %}

Indeed, the hashCode is most likely called by a Set implementation and if the username is not yet set, you may break the Set contract if you set (sorry for this repetition) the username while the User is in the Set. 
You could be more violent and throw an exception instead to be sure to spot such pratice.

If you want to send us some code modifications, please use a pull request

Happy coding !