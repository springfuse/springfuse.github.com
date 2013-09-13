---
layout: english
title: Query by example with Spring Data JPA
comments: true
---

> ** Update (2013-09-13) **: we no longer support Spring Data, instead we provide Query By Example using only JPA 2, without Spring Data.
> Please refer to [JPA2 Query By Example blog post](/2012/09/05/jpa-query-by-example.html) for more information.

# Query by Example with Spring Data JPA

We are pleased to announce that SpringFuse now leverages <a href="http://www.springsource.org/spring-data/jpa">Spring Data JPA</a> in the code it generates.

It simplifies dramatically the generated data access layer.

The most challenging part was to offer a **Query By Example** feature, as we did when using Hibernate `Example` support.

This small blog entry is about it.

## Query By Example

The idea is to use an entity as a parameter holder when doing query on an entity.
For example, assuming we have an `Account` entity with a `lastname` property. Here is how to do a simple query by example:

{% highlight java %}

	Account account = new Account();
	account.setLastname("agger"); // will apply LIKE %agger%
	
	Page<Account> accountRepository.findWithExample(account, new PageRequest(0, 100)); // we get first 100 result

{% endhighlight %}

This codes leads in fine to following SQL query (to be accurate, there is also a count query, for pagination):

{% highlight sql %}

	select
        account0_.id as id6_,
        account0_.address_id as address2_6_,
        account0_.BIRTH_DATE as BIRTH3_6_,
        account0_.civility as civility6_,
        account0_.email as email6_,
        account0_.FIRST_NAME as FIRST6_6_,
        account0_.is_enabled as is7_6_,
        account0_.LAST_NAME as LAST8_6_,
        account0_."PASSWORD" as PASSWORD9_6_,
        account0_.login as login6_,
        account0_.version as version6_ 
    from
        Account account0_ 
    where
        account0_.LAST_NAME like ? limit ?
 
{% endhighlight %}

## Mixing Query by Example and Range Query.

Now, let's imagine that you also want to restrict the query above to all accounts having their date of birth between 1940 and 1945 included.
Of course, the entity does not have the appropriate property (from & to). 
For this reason, we introduce some additional parameters. Here is an example:

{% highlight java %}

	Calendar from = Calendar.getInstance();
	from.set(1940, 0, 1);
	
	Calendar to = Calendar.getInstance();
	to.set(1945, 11, 31);
	Account account = new Account();
	
	// like
	account.setLastName("Jagger");        
	
	// between from and to
	RangeDate<Account> birthDateRange = new RangeDate<Account>(Account_.birthDate);
	birthDateRange.setFrom(from.getTime());
	birthDateRange.setTo(to.getTime());
	
	// prepare ranges arg
	List<Range<Account, ?>> ranges = new ArrayList<Range<Account, ?>>();
	ranges.add(birthDateRange);
	
	accountRepository.findWithExample(account, ranges, new PageRequest(0, 100));
{% endhighlight %}

Note that you can add ranges of any type: Integer, Long, LocalDate (joda time), BigDecimal, etc...

This codes leads in fine to following SQL query (to be accurate, there is also a count query, for pagination):

{% highlight sql %}
	select
        account0_.id as id1_,
        account0_.address_id as address2_1_,
        account0_.BIRTH_DATE as BIRTH3_1_,
        account0_.civility as civility1_,
        account0_.email as email1_,
        account0_.FIRST_NAME as FIRST6_1_,
        account0_.is_enabled as is7_1_,
        account0_.LAST_NAME as LAST8_1_,
        account0_."PASSWORD" as PASSWORD9_1_,
        account0_.login as login1_,
        account0_.version as version1_ 
    from
        Account account0_ 
    where
        (
            account0_.LAST_NAME like ?
        ) 
        and (
            account0_.BIRTH_DATE between ? and ?
        ) limit ? 
{% endhighlight %}

## How it works

The repository implementation is rather simple as we provide a custom Spring Data repository common to all entities. 
Here is the implementation of the `findWithExample` method:

{% highlight java %}

    @Override
    public Page<E> findWithExample(E example, List<Range<E, ?>> ranges, Pageable pageable) {
        Specifications<E> spec = Specifications.where(byExampleSpecification.byExample(example));
        spec = RangeSpecification.andRangeIfSet(spec, ranges);
        return findAll(spec, pageable);
    }

{% endhighlight %}

Pretty simple, isn't it?

The tricky and beautiful part is of course the implementation of the **reusable** `ByExampleSpecification` and `RangeSpecification`.

To know more you can either <a href="/">generate a project yourself</a> or browse the code of some already <a href="https://github.com/jaxio/generated-projects">generated projects on github</a>.

Enjoy!

The SpringFuse/Jaxio team.