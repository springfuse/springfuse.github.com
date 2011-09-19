---
layout: english
title: Springfuse change log 
---

#3.0.56 (2011-09-19)

## jsf2-primefaces front:
* pay special attention to keyboard navigation and focus for accessibility concern
* fix some page and layout to please achecker accessibility tool.
* use p:layout
* make dialogs modal
* do partial rendering when removing item from x-to-many dataTable
* rename various ids for better clarity


#3.0.56 (2011-09-08)

## jsf2-primefaces front:
* Upgrade to PrimeFaces 3.0.RC1-SNAPSHOT
* Remove selectionMode="single" from p:dataTable as webflow datamodel does not support it.
* Change the way we display askForUpdateDialog
* Change the way we display the search popup faced this issue: http://forum.primefaces.org/viewtopic.php?f=3&t=14597
* Use p:selectOneMenu in search form
* Use JSF2 resources facility instead of spring one.
* Clean up our CSS (keep it minimal)
* Use new primefaces maven repo & tag lib namespace uri
* Use 'redmond' theme (see pom.xml and web.xml)
* accessibility: add 'for' attribute to label in the inputText component
* accessibility: use hidden commandButton instead of hidden commandLink in panelMenu component

# 3.0.55 (2011-07-27)

## Database reverse:
* Make database reverse work for DB2 on Z/OS system
* Catalog and schema name were ignored (was working most of the time as we provide sensitive default for Oracle and DB2

## backend pack
* Fix default value for attribute mapped to enum.
  For example assuming the civility colunm is mapped to CivilityEnum and its default valude in the database in "MR",
  instead of generating setCivility("MR"), we now generate setCivility(CivilityEnum.MR). Thanks to Aram Murguía.
* Fix SearchTemplate constructor by copy. List were passed by reference instead of being cloned.
* Fix some var name clashes occurring when a non foreign key attribute var name matches the var name used by convention for an x-to-one relation.  

## jsf2 primefaces pack
* Fix url-pattern in web.xml ('*' ==> '/*'), thanks to Aram Murguía

# 3.0.52 (2011-07-11)

## Remote logs:
* Generation logs are now sent by email along with extracted metadata.
* Fix archetype to take into account email entered in springfuse generation form.

# 3.0.51 (2011-07-07)

## Celerio engine:
* Leverage IS_AUTOINCREMENT column metadata when the jdbc driver supports it. 
  It is used to determine if we should annotate simple pk field witn @GeneratedValue or not. 
  If the driver does not support this metadata, we do as before: numeric pk are annotated 
  by default with @GeneratedValue.

* Introduce back support for composite foreign key with the following limitations:
  * Only composite @ManyToOne and its inverse @OneToMany are supported
  * Such composite relations are not yet supported/tested in front-end views

* DB2 support:
  * Fix db reverse when foreign key are duplicated (observed with SAMPLE schema shipped with DB2 distribution)
  * When connecting to the database, force schema name to current username
   
* Fix composite primary key error, when a date is present in the composite PK.
  Was due to missing import of org.springframework.format.annotation.DateTimeFormat

* Upgrade all H2 versions used in the examples or template pack bootstraps to 1.3.157

## spring mvc 3 front:
* Move up the character encoding filter and apply it to /** (thanks to unibail for tip)


# 3.0.50 (2011-06-16)

##Celerio engine:
* compilation fix for default value when the numeric type maps to BigInteger or BigDecimal
{% highlight java %}
  // we had for example (compilation error)
  setPrice(0.0000);
  // we now generate:
  setPrice(new BigDecimal("0.0000"));
{% endhighlight %}

## backend:
* jpa: generate @DateTimeFormat(pattern = DATE_FORMAT_PATTERN) instead of @DateTimeFormat(iso = DATE) to ease global modification of the formatted date. The DATE_FORMAT_PATTERN is statically imported from ResourcesUtil.

## spring mvc 3 front:
* fix auto complete for many to one: in certain case, the binding was not working on the server side
* fix the contact us link in the generated app

## jsf2-primefaces front:
* fix the contact us link in the generated app


# 3.0.49 (2011-05-24)
## General

* no longer skip table without pk. Instead, look for:

  1. first non null unique column
  2. or first unique column
  3. or fall back to first column

* better logging message for property name clash and duplicate columns in metadata (Thanks to Lisa from Qualcomm)
* add getPackageNodeUp facility.

## Improvements

* Specify mime types in web.xml (thanks to Björn Johansson)

## maven-springfuse-plugin:

* dump reversed metadata to target/reversed-metadata.xml


# 3.0.48 (2011-05-18)
## Fixes

* Fix file move (see 3.0.47) when a file with the same name is already present in the collision folder. Classes not located in the project root package would not have been picked up


# 3.0.47 (2011-05-11)
## General
* The springfuse remote generation plugin now streams the generation logs from our server.
* better logging message for property name clash and duplicate columns in metadata (Thanks to Lisa from Qualcomm)
* Fix @Column mapping for reserved column name whose var name is the same as the column name
{% highlight java %}
@Column(name ="`VALUE`")  //
  public String getValue()...
{% endhighlight %}


# 3.0.46 (2011-05-04)
## General

* Better quickstart example
* Change the save() implementation in HibernateGenericDao to support persist OR update of entities having either  auto generated id, manually assigned or composite pk.
* Fix equality issue when business key is a java.util.Date: use second precision instead of millisec to cope with Oracle which only store second precision.
* Fix delete propagation for one to one (inverse side) using orphanRemoval attribute, as for one to many.
* Fixed an infinite loop in XxxGenerator occurring when a bidirectional one to one relation was present.
* Search by pattern now searches in assigned primary keys (both simple primary key and composite primary keys)


## Spring MVC 3 front option

* Totally revisited the look'n'feel and the navigation... for the better :-). Many thanks to Frédéric Pernot from Unibail-Rodamco for his precious feedbacks
* upgrade to jquery 1.5 <http://jquery.org/>
* enable ajax history <https://github.com/cowboy/jquery-bbq>
* use blueprint css framework <http://www.blueprintcss.org/>
* use jquery-ui <http://jqueryui.com/>
* upgrade jquery-validate <https://github.com/jzaefferer/jquery-validation>


## JSF2/Primefaces front option

* Use embedded flow to renderer search flows in primefaces popup dialog
* File download/upload is now supported


# 3.0.43 (2011-02-08)
## Introducing JSF2/Primefaces/Webflow pack
New Front end option: JSF 2 + PrimeFaces 2.2 + Spring WebFlow 2.2.1. 

Many thanks to <a href="http://www.linkedin.com/profile/view?id=35594474">Bernard Pons</a> (Architect at Banque de France), for sharing his expertise and vision on this front-end stack. 
Without him, you would not benefit from it.

# 3.0.41 (2011-01-06)

## New
* You can new generate a backend only project...
* New: Possibility to configure 1 sequence per table. Please use sequenceName attribute in entityConfig.
  It will generate the corresponding @SequenceGenerator and @GeneratedValue annotations.
* New: generate validation annotations on simple primary key that are assigned manually.
* New: In XxxDaoImpl, add getByExampleExtraCriterions when the corresponding entity has simple PK and is manually assigned.
  This allows to perform search on pk field as any other field.
* New: Entities are sorted in alphabetical order in generated menus.
* Upgrade to Spring 3.0.5.RELEASE, Spring Security 3.0.5.RELEASE

## Fixes
* Fix jdbc driver (when oracle is selected) in generated pom
* Fix PrimaryKeyJoinColumn annotation in case of JOINED inheritance (tables having different pk names)
* Fix bidirectional one-to-one generated test (XxxDaoWithRealSessionTest)
* Fix missing import when composite primary keys uses an Enum.
* EnumType is no more mandatory on enumConfig
* Fix enableOneToVirtualOne="true" option on columnConfig representing a foreign key
* Fix getByExampleExtraCriterions on entities with composite pk
* Fix enum2xsd plugin when enum has a varargs argument
* Fix oracle retrieve remarks
* Fix javadoc comments (use '/**' instead of '/*' for entity and attributes)	


# 3.0.39 (2010-11-12)
## New
* springfuse plugin: Support remote generation through http proxy, including proxy using ntlm (please let us know if it works for you)
* DateRange now also support jodatime LocalDate and LocalDateTime
* Activate ManyToManyConfig element to fine tune @ManyToMany relation (var, element var, fetch, cascade)
* Enhancement in search by example: 
   Each DAO constructs additional criteria to leverage the associated entities of the passed entity example. 
   It allows you to perform more complex queries without having to code them. Also it serves as
   example if you need to improve the search by example generated code (please check the code
   of the DAOs, they are no longer empty for entities having one or more associations).
   
# Fixes
* Remove initBinder method in controller (not really useful + was causing compilation bug in certain limit case)
* Fix ehcache configuration filename (was not properly picked up by hibernate)


# 3.0.33 (2010-10-14)
## New
* Increase the max of number of tables you can reverse per schema to 400 (was 100)
* Revisited, for the better, the generated spring mvc 3 controllers
* Fix some "context-less" link on the generated application homepage (was ok without context, but was problematic for example 
  when running the generated app in Tomcat/Eclipse, where by default a context is present)
* Business Key and equals/hashCode: You can now use the businessKey attribute in your configuration. For example

{% highlight java %}
	<entityConfig ...>
		<columnConfig columnName="email" businessKey="true"/>
		<columnConfig columnName="username" businessKey="true"/>
	</entityConfig>
{% endhighlight %}

Celerio will generate the equals/hashCode methods accordingly. If no columnConfig is marked as a business key, convention will apply in this order:
1. use the first unique constraint involving 1 column
1. if none is found, use the first unique constraint involving more than 1 column
1. if none is found, the PK is used.

## Fixes
* Fix cyclic package dependency that was due to format annotations
* No longer elect a table as an 'Account' table if it has a composite primary key.
   	

# 3.0.30 (2010-09-03)
We are happy to release this new version which remotely uses the latest version of Celerio.
The remote generation process has been greatly simplified:
 
* You no longer have to subscribe online
* You no longer have to upload manually the metadata file: Our Springfuse maven plugin does it for you transparently.

And of course this new version comes with new major features:

* You can now configure the generation process: JPA inheritance, types, names, etc... 
* The front-end is now based on Spring @MVC 3 and JQuery. As a result the Java code is drastically simplified.
* Upgrade to Spring 3.0.3.RELEASE
* Upgrade to Spring Security 3.0.3.RELEASE
* Upgrade to Hibernate 3.5.5-Final
* Upgrade to Hibernate Validator 4.1.0-Final

Attention: the Spring Web Flow front-end is no longer generated. It is only provided with Celerio (part of JSF + WebFlow pack)

We would like to thank all the developers that have been using Celerio over the last months. 
Some of their precious feedbacks have helped us to improve the free edition of SpringFuse.
A special thank to Bernard Pons (Architect at Banque de France) for his numerous and constructive feedbacks on 
all the parts of the generated application. Another special thanks to Hervé Le Morvan for sharing his experience on legacy, but pretty impressive, 
ORM technologies and generators. Finally, thanks to the developers using Celerio who took the time to report issues and ways to improve 
both the generated code and the product: Hervé, Tony B., Sébastien P., Lottfi B., Pierre T, Gary ?, Vincent L.


# 2.8.22 (2010-01-04)

* Spring Web Flow: fix url when using non-root contexts. Thanks to Pierre Boned.


# 2.8.21 (2009-11-25)

* Spring Web Flow: Use the create subflow, in addition to the select subflow, to wire a many to one relation
* Spring Web Flow: display many-to-many relation in the review state
* no longer generate targetEntity attribute in ManyToMany association since we use generics
* fix XxxFormServiceImpl..java when a many to one points to itself.


# 2.8.19 (2009-11-11)

* Support case where @OneToMany's mappedBy attribute refers to an @EmbeddedId (occurs when the id is a composite primary key). 
  Thanks to Olivier Huber from <a href="http://www.zenika.com">Zenika</a> for reporting it.
* Fix a regression bug showing up in composite primary key class when one of the property is a Date. 
  Thanks to Ahmad Sousak from <a href="http://www.steria.com">Steria</a> for reporting it.
* Remove(Roll back) the default-lazy-init="true" that was recently added in applicationContext-scheduling.xml as it prevents the jobs from starting!. 
  Thanks to <a href="http://www.hikage.be/">Gildas Cuisinier</a> for taking the time to analyze it and report it.


# 2.8.18 (2009-09-24)

* New feature: generate flow menu. Please read <a href="http://blog.springfuse.com/2009/09/spring-web-flow-menus.html">our blog entry</a> to know more.
* Support for hibernate filters in flows thanks to a special flow execution listener
* Refactor: 'boolean hasXxx()' on domain's model changed to '@Transient boolean isXxxSet()' for better clarity and compatibility with EL (expression language) in JSP/Flows etc.
* Refactor equals and hashCode


# 2.8.17 (2009-09-21)

* Upgrade from Spring 2.5.6 to Spring 2.5.6.SEC01 and no longer use spring.jar. We use instead spring-orm.jar etc... as for Spring 3.0 which is coming soon :-)
* Upgrade from SpringSecurity 2.0.4 to 2.0.5.RELEASE
* Upgrade from Hibernate 3.2.6.ga to hibernate-core 3.3.2.GA / EntityManager 3.4.0.GA
* Upgrade Hibernate Validator from 3.0.0.ga to 3.1.0.GA
* Upgrade from SpringWebFlow 2.0.7 to 2.0.8.RELEASE
* JPA annotations are now set on getters instead of fields.


# 2.8.16 (2009-08-22)

* New feature: Generate annotation for validation (use Hibernate Validators 3.0.0.ga)
* New feature: Handle composite foreign keys
* JPA mapping fixes:
 * Check that the column type is compatible with @Version
 * Fix mapping bug when when both side of a many-to-many are the same model
* Fix Cobertura errors by ignoring beans without interface
* Fix naming clash in managerXxxImpl when unique column name and table name are the same
* Change: Make all associations unidirectional by default. Celerio users can enable bidirectionality thanks to the configuration file.
* Change: Enable Spring lazy loading by default to speed up startup time of very large schemas
* Upgrade log4j dependency to 1.2.15 (from 1.2.11)
* Upgrade Cobertura maven plugin from 2.2 to 2.3
* Upgrade quartz-all from 1.6.0 to 1.6.3 (quartz pom.xml is now alsmost ok)
* Use servlet 2.5, jstl 1.2, jsp 2.1
* Eclipse integration:
 * No longer generate the Eclipses files. Please import the project as a Maven project in Eclipse, it works fine.
 * Set the source/target to 1.5 / 1.5 explicitly with the compiler plugin to keep Eclipse happy
		

# 2.8.15 (2009-07-05)

* Fix a compilation error (regression) in generated unit test when one of the composite primary fields maps to a Java Long (thanks to Stéphane Deraco for reporting it)
* Fix a compilation error occurring when one of the composite primary key fields maps to a date.
* Fix an incorrect redirection url after an update of a model having a composite pk (thanks to David Martin).


# 2.8.14 (2009-06-25)

* No longer set attribute that match the default value in @Column annotation:
 * length = 255 is useless
 * name = colname is useless when colname is same as property
* Set @OneToMany to Cascade.ALL in the case of a 'pseudo' one to one mapping
* Search by example now takes into account pk fields which fix the current navigation consistency (ie search for linked accountRole link on account display page)
* Search by pattern: also include string pk (several people were surprised this was not the case)
* Apply javascript numeric validation for composite pk field when appropriate
* Use Restrictions.disjunction instead of Restrictions.or in HibernateUtil. This lead to better and more readable query in the console
* Preserve ref integrity when deleting a model having a bidirectional relation even in case where the other side is a 'pseudo' one to one
* Instrument only bean model that really require lazy loading (@Lob byte[])
* Remove javascript redundancy for ajax navigation (in table sort column) using dojo selectors
* Fix a runtime exception when no account table is found (no longer set the hibernate filter on mock!)
* Fix a compilation error when no account table is found (due to a wrong import)
* Fix unit test error when no account table is found (Thanks to David Martin)


# 2.8.9 (2009-06-18)

The major feature of this release is the <strong>JPA support</strong>.
It was a long awaited feature demand from our users.
Other important changes are listed below.

* Bidirectional association generation (one to one / one to many) is now optional. This feature is not yet available for the online version. (Thanks to Pierre Gaudin)
* Use generics for DAO and managers when appropriate (Thanks to Bernard Pons)
* SpringSecurity related:
 * Refactor SpringSecurityContext: no longer create a User if it is anonymous (Thanks to Marcel Heemskerk)
 * Refactor AccountContextSupport: remove the "ROLE_USER" dependency
 * Refactor AccountContext: do not use the account.getRoleNames as fallback
* Ease of use related:
 * Some move and renaming to keep things more clear when there are a lot of tables (thanks to Ahmad Sousak)
 * move domain related generated properties to localization/domain-generated
 * move /WEB-INF/domain/* to /WEB-INF/domain-generated/*
* Refactor XxxFormService: no more interface
* Refactor XxxForm: no more dependency on XxxManager or XxxWebSupport.
* Refactor the main pom : filter only .properties (we used to filter also the .xml files)


# 2.7.4 (2009-05-10)

* New! <b>Spring Web Flow</b> support:
 * For each entity, a create flow and a select flow are now generated. The select flow is used as a subflow in create flow whose entity has a many to one relation.
 * Make the MultipartFile property transient to support file upload in Spring Web Flow.
 * Add flow path in applicationContext-security-http.xml. By default only ROLE_ADMIN can access them.
 * Declare flows in spring/springmvc-webapp.xml
* Remove useless interface on SearchTemplate.... keep only impl version which now takes the name of the interface
* Fix a compilation error when a table reference itself (Thanks to Pierre Gaudin. for reporting it)
* Remove CollectionUtils.java as it was no longer used by the generated code.
* When a table has no pk, use the first non null unique index instead (Thanks to Bernard Pons)


# 2.7.3 (2009-04-09)
* Fix a case that was breaking compilation of the generated code: a composite foreign
  key having one of its field also used as a foreign key (non-composite). (Thanks to <a href="http://www.linkedin.com/in/marcelheemskerk">Marcel Heemskerk</a>).
* Isolate the use of URLEncoder.encode(string, "UTF-8") in a dedicated URLEncoderUtil class.
* Cosmetic in XxxFormServiceImpl.java (use @Autowired on properties instead of constructor) and remove some unused dependencies.
* Small changes in spring/springmvc-webapp.xml to make future Spring Web Flow integration smoother.
* Improve doc in generated controllers
* Changes in XxxValidator:
 * change the validator name from XxxValidator to XxxFormValidator to later use Spring Web Flow convention over configuration (invoke validator automatically)
 * annotate each validator with @Component
 * rename <fieldName>Validation method names to validate&lt;FieldName&gt;Field
 * overload validate() so it can also take a XxxForm as argument (Spring Web Flow support)
 * Inject the XxxValidator in XxxFormController using @Autowire


# 2.7.2 (2009-04-03)

* Use URLEncoder.encode(string, "UTF-8") to encode parameters that appears in search results' sort urls in XxxSearchForm.java files.


# 2.7.1 (2009-03-30)

* pom.xml: remove the error prone activeByDefault from H2 profile.
 - No impact as H2 properties are anyway set by default when no database profile is used.
 - Cosmetic changes in versions organization.
* Fix and prevent potential bean name collisions, encountered on tables whose name was either
 'Admin', 'Login' or 'Password' by forcing the name of all generated controllers to a name
 that is less collision-prone. There is no impact because these names are not used anywhere.
 Indeed the controllers sit on top of the rest (Thanks to Laurent P. and Vishal P. for reporting this issue).
* Spring Web Flow compatibility: now the generated XxxForm.java, XxxSearchForm.java, SearchParameters.java and PagerDisplayImpl.java can be used from Spring Web Flow.
* Rename the applicationContext-web.xml to applicationContext-security-http.xml and reflect this renaming in web.xml for better clarity.
* Annotate AccountDetailsServiceImpl.loadByUsername with @Transactional so it works even without Open Session In View (thanks to Pierre Abel for reporting this issue).
* Fix bug when the accountId is Long: distinguish the type in filter (Integer vs Long) both in the Java code and in the hibernate filter definition.
* Use Html entities instead of images to display sort arrows (&uarr; or &darr;) in search results. Impact in XxxSearchForm.java and searchResult.jsp pages.
* Allow search using both a searchPattern and a model example. Change within Xxx.DAOHibernate.addCriterionOnCriteria method.

# 2.7.0

* Add Springfuse version support in the project generation form (Thanks to Ian H. for requesting it).
  It allows you regenerate a project using an older version of Springfuse.
  Of course, we encourage you to switch to the latest release as soon as you can.
* Package reorganization: (Thanks to Steve T., it really makes more sense). Group domain classes (model, manager, dao, hibernate) that were in
  a dedicated sub package in the parent package. For example, the AccountModel package is now 'domain' instead of 'domain.account', etc.
* Package reorganization: to clearly separate domain related classes from the rest, move
  the classes that were in the 'hibernate' package to 'hibernate.support' or 'hibernate.listener' packages
* Package reorganization: to clearly separate domain related classes from the rest, move
  the classes that were in the 'dao' package to 'dao.support' package.

# 2.6.0

* Fix a compilation error when using a composite key having a date type (Thanks to Steve T. for reporting it)
* Make getQueryStringForSortableHeader method public on all search forms so it can be conveniently used from Freemarker views
  (needed by a user using Freemarker instead of JSP) and provide more getXxxSortStatusKey methods (i.e on primary keys).
* Fix AssertUtil.isFalse(Boolean). Note that it is not used in the generated code.
* Fix location of hibernate hbm files in JavaDoc of all XxxModel.java files.
* Cosmetic comments in Spring's configuration files


# Since 2009-03-13

* Fix a zip issue that was preventing windows to unzip properly the files at the root of the generated project (Thanks to Neil G. for reporting it)
* Add some instructions for tomcat 5.5 and tomcat 6.0 in the generated pom.xml.
* Change in the generated pom.xml concerning mysql users: use the org.hibernate.dialect.MySQLInnoDBDialect instead of the org.hibernate.dialect.MySQL5Dialect
* Minor changes in Spring application context files related to bean description (no impact, just documentation and cosmetic)


# Since 2009-03-06

* Fix hard coded reference to login/password/email setters that were preventing certain generated projects to compile.
* Fix a generation issue when the email column was not present in the auto detected Account table.
* Introduce isAccount method in the AccountContext for fined grained security.


# Since 2009-03-03

* Account table detection: accept the 'user_name' column as a candidate for the username.
* Use directly LocaleContextHolder instead of AccountContext in EmailServiceImpl to prevent NPE when using the EmailService from a cron job.
* Fix potential NPE in Context Interceptor: <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/web/servlet/HandlerInterceptor.html">the ModelAndView that the handler returned (can also be null)</a>
* Checkbox in all createForm.jsp/updateForm.jsp: fix path of default checked value. The bug was visible only in certain cases.
* Cosmetic in xml configuration: move bean descriptions from comments to description tag


# Since 2009-02-28

* Set currentAccountId to a dummy value in HibernateFilterContext


# Since 2009-02-27

* Fix the currentAccountId type in HibernateFilterContext: it was hard coded to String, it has now the same type as the primary key of the 'account' table.
* Circumvent a SpringJavascript bug similar to <a href="http://jira.springframework.org/browse/SJS-21">http://jira.springframework.org/browse/SJS-21</a> (thanks to Ian Hendry for reporting it).
* SearchTemplateImpl setters now return SearchTemplateImpl instead of SearchTemplate so builder pattern can be used.


# Since 2009-02-24

* Remove trailing div tag in show.jsp responsible for poor layout under IE (thanks to Ian Hendry)
* Fix duplication of the searchParameters.searchMode in the show.jsp page for each domain table (thanks to Ian Hendry)
* Fix a typo in the string ROLE_USER in the generated PasswordService interface that was preventing the user from changing his password (thanks to Steve T.)
* Provide two sets of velocity templates under src/main/resources/velocity/emails for email sent upon reset/change password.


# Since 2009-02-12

* Collect JDBC driver name/version when reversing the database schema. This information is displayed in the generated project page.
* Improve support for camel case syntax: if your column or table name are camel cased and your jdbc driver preserves your syntax, 
  Springfuse takes it into account to generate clean variable, method and class names following your camel case convention.
* Account table auto detection:  Springfuse now tries to identify your 'account' table. It looks for at least 2 columns login and password. 
  The login column can be named either: 'login', 'username', the password column can be named either: 'password', 'pwd', 'passwd', 'mot_de_passe'
* Email column is no longer mandatory in the account table
* Hibernate Filters on the account PK and foreign key referencing the account PK are no longer hard-coded.
* Role table auto detection: Springfuse now tries to identify your 'role' table. For the moment the role table must be linked through a many-to-many relationship to 
  the account table and contains a column whose name is either: 'authority', 'name_locale', 'role_name' 'role'
* When generated, the mock account table is now named sf_mock_account (thanks to Loic Fournial)
* Databse schema from Julien Dubois's tudulist project can be reversed
* Include the primary key field in search by example when the primary key looks like a natural key: a string type with a size different from 32.
* Fix lazy loading support in the generated pom.xml.
* Fix a bug in the hibernate mapping file that was preventing from inserting columns value having a default value on the database side.
* Better support for name conflict resolutions when column names looks alike, for example roleId and role_id.
* Basic numeric validation on the client side in create and update form
* disable JSP compilation by default in the generated pom.xml
* No longer validate email on the server side if the email field is not required
* Improve generated css so we do not have to use &lt;br/&gt; tags in the generated pages.
* New homepage for the generated project (thanks to Nicolas Martignole for his suggestions)
* In search results, sort arrows are now displayed next to the column label.
* fix search by example parameters propagation when sorting/iterating in search results page.
* Upgrade to velocity 1.6.1
* Upgrade to Spring Javascript 2.0.5


# Since 2009-02-03

* Remove common table prefix before generating variable/method/class name
* Clean primary key variable names
* Clean foreign key variable names
* Ignore foreign key that do not refer to a primary key instead of stopping the generation!
* Fix JSP domain page: There were few tags missmatch such as use a th instead of td in the pages show.jsp, createForm.jsp, updateForm.jsp
* Prevent action caching in urlrewrite.xml
* Ignore specific hibernate hilosequence table

