---
layout: english
title: Springfuse change log 
---

## SpringFuse/Celerio Change Logs


### 3.0.101-SNAPSHOT 

##### Database reverse 
* We now extract enums definitions from mysql
* We support mysql year(4) type

##### Configuration 
* fieldNaming element replaced and extended by tableRenamer and columnRenamer.
  Please refer to [documentation](http://www.jaxio.com/documentation/celerio/configuration.html#name_rule)
* fix: the columnConfig's displayOrder attribute is not always taken into account.
 
#####  Convention

* When your table/column name uses camelCase syntax we will use the table/column name as entity/field name.

##### pack backend-jpa
* support many-to-one and one-to-many associations with an intermediate table (as many-to-many).
* it is no longer required to set the associationDirection attribute to BIDIRECTIONAL when configuring inverse association.
* fix default var name of @OneToMany and inverse @OneToOne association (thanks to Shahzad Munir for reporting it)
* rename "isIdSet" method in composite primary key to "areFieldsSet" to avoid duplicate method name when one of the composite pk column name is "id".
* add getType method to GenericDao and GenericRepository.
* fix hashCode when using a fk as a business key
* fix ordinalPosition override in xml (works only for simple properties)
* you can now configure if a field is lazy
* do not log sql queries when using perf profile

##### pack jsf2-spring-conversation
* extract jsf breadcrumb and menu handling from conversation manager
* add print action (opens all tabs, remove layout, add css media print)
* set immediate="true" to quit command button in search panel
* in excel reports use labels for enum values
* in excel reports use printers for many to one values
* add better orderBy defaults to autocompletes
* add sensible default labels on conversations
* simplify iconsXXX usage by relying on jsf scopes
* simplify localization
* localize hardcoded string in GenericController
* use autocomplete maxResults property in completeProperty and completeFuzzy
* force UTF-8 encoding, needed when uploading a file
* fix download link in select page
* fix pagignation in xToMany in edit page
* use the controller defaultOrder from the GenericLazyDataModel 

##### pack jsf2-spring-webflow
* fix regression introduced in 3.0.100: language switch no longer works
* fix regression introduced in 3.0.100: edition of entity with composite pk no longer work


### 3.0.100 (2013-05-01)

[Sample generated app diff 3.0.99-3.0.100](https://github.com/jaxio/generated-projects/commit/9b82e77f4c4b7e6bca495c20bc925f2c7c9170fa) 

##### pack backend-jpa
* better support for composite fk and fk in composite pk
* remove repository interfaces
* instrument domain object which contains blobs to support lazy loading
* use logback instead of log4j
* custom enum types are back
* logs are produced in target/
* replaced dbcp by tomcat-jdbc
* simplify the graphLoader
* refactored hibernate search integration with SearchParameters
* jpa by example now supports annotation on fields
* use @Configuration to replace some xml definitions
* use mockitoRunner instead of creating manually the mocks
* full text indexer is no more blocking
* rename DaoTest to DaoIT, they will be executed at integration-test phase
* upgrade hibernate from 4.1.9.Final to 4.2.0.Final 
* upgrade usertype.core from 3.0.0.CR3 to 3.0.0.GA
* upgrade commons-fileupload from 1.2.2 to 1.3
* upgrade jxls-core from 1.0 to 1.0.1
* upgrade jsoup from 1.6.3 to 1.7.2

##### pack jsf2-spring-conversation
* start conversation programmatically
* introduce GenericToManyAssociation and GenericToOneAssociation to reduce code
* move code from LazyDataModel to controller
* use more the jpa metamodel 
* handle optimistic lock exception, warns the user and propose reloading data
* rename MultiPageMessagesSupport to MultiPageMessagesListener
* in views use generic printer instead of the typed one
* in view remove where possible the usage of $msg.KEY
* jetty stars now with web-development.xml in development mode
* componentarize fileUpload and outputFile
* show labels when using enums
* split service.UserContext in LocaleService and UserContextService
* use navigator in calendars
* use @Configuration to replace some xml definitions
* upgrade primefaces from 3.4.2 to 3.5
* add jacoco support for sonar


### 3.0.99 (2013-03-26)

[Sample generated app diff 3.0.98-3.0.99](https://github.com/jaxio/generated-projects/commit/238324b1fb721f42b83ed1b83ed865391d9ba848) 

##### pack jsf2-spring-conversation
* move code to generics
* separate XxxGraphLoader in a dedicated file.

##### pack jsf2-spring-simple
* move code to generics
* separate XxxGraphLoader in a dedicated file.

##### pack jsf2-spring-webflow
* no changes

##### pack backend-jpa
* no changes

### 3.0.98 (2013-03-25)

[Sample generated app diff 3.0.97-3.0.98](https://github.com/jaxio/generated-projects/commit/84f2996f621b10ca249e1009d547ede6d3dd0147) 

##### pack jsf2-spring-simple
New front end option, without conversation, just plain JSF2/Spring/Primefaces.

##### pack jsf2-spring-conversation

Major change: we no longer keep an entityManager instance in the Conversation, instead we work with detached entities.

* update jsf-api from 2.1.17 to 2.1.20
* fix compilation in SearchEditForm when JPA inheritance is used
* byEntitySelector now relies on real xToOne field, not the fk
* make jsf page non cacheable see http://stackoverflow.com/questions/49547/making-sure-a-web-page-is-not-cached-across-all-browsers
* handle browser back button (pop context accordingly)
* remove harcoded ':' at the end of labels
* remove jquery notif (was used by selenium tests)
* introduce XxxPermission and use them
* search form is now toggleable
* introduce inputMultiAutoComplete for search forms (disjunction on a specific field)
* saved search feature
* introduce GenericController
* move a lot of code to generic level
* export to excel feature
* upgrade to spring security 3.1
* update login button
* better look'n'feel (no more white on white issues)
* merge multiple info/error messages in one panel
* use home made @Conversation annotation
* Use FIFO policy to terminate conversation when the max number of conversations is reached
* handle natural conversation ending (when all contextes are popped)
* 'create' conversation link on homepage
* move the term handling in the GenericSearchForm
* better auto-complete with many to one
* some changes to make sonar happy
* handle all cases in primeresource handler
* make more sens about subpackages, and move around files to prevent cyclic dependencies
* simplify conditionnalValidatorUtil

##### pack jsf2-spring-webflow
No significant changes

##### pack backend-jpa
* SearchParameters cache is now false by default
* no longer map FK columns. Only rely on many-to-one association.
* string based property selectors now make use of the SearchParameters searchMode
* fix oracle date precision
* XxxPrinter refactoring
* replace junit asserts for fest-assert in model unit tests
* extract methods to JpaUtil
* rename searchParameters.propertySelectors() and entitySelectors() to properties() and entities()
* introduce genericDao.getVersion(entity) so it can be used in GenericController auto complete decision helper
* Update spring version to 3.2.2, cleanup xsd reference, add task executor to handle the lucene IndexerService
* use meta model instead of hardcoded values in entity.toString()
* update joda-time from 2.1 to 2.2
* update hibernate-search and hibernate-search-analyzers from 4.1.1.Final to 4.2.0.Final
* update guava from 12.0 to 14.0.1
* update commons-codec from 1.6 to 1.7
* update aspectj from 1.6.12 to 1.7.2
* update junit from 4.10 to 4.11
* update mockito from 1.9.0 to 1.9.5
* update jackson-mapper-asl from 1.9.2 to 1.9.12

##### Celerio config
* mark entity as indexed in case it has one columConfig indexed

### 3.0.97 (2013-03-04)

[Sample generated app diff 3.0.96-3.0.97](https://github.com/jaxio/generated-projects/commit/dfaf72437db6b4da9c6c0c21aeb58d0bbf983d9a) 

##### Front End (without spring web flow)
* Audit information, when present, is displayed only if not null

##### JPA2 Backend
* query By Example using Many to Many uses 'AND' by default, but it is configurable using useANDInManyToMany in SearchParameters.
* introduce useDistinct in SearchParameters
* in SearchParameters rename getLeftJoinAttributes to getLeftJoins
* fix isNull handling in ByRangeUtil
* make Range.setIncludeNull java bean complient

##### Selenium (pro users only)
* remove jquery notification as we will be using primefaces growl (for selenium tests)
* upgrade selenium from 2.24.1 to 2.29.1

##### Celerio reverse engine
* fix duplicate column reverse ( http://stackoverflow.com/questions/1601203/jdbc-databasemetadata-getcolumns-returns-duplicate-columns )

##### Celerio configuration
* 2d level cache is now fully configurable. It is disabled by default.
* fetch type is now configurable globally
* cascade type is now configurable globally
* orphanRemoval is now configurable globally

Here is an example extracted from the default maven-celerio-plugin.xml configuration file:
{% highlight xml %}
<configuration>
	<!-- ... skip stuff ... -->
        <defaultEntityCacheConfig usage="NONE" />
        
        <defaultManyToOneConfig fetch="LAZY">
            <cascades>
                <cascade type="PERSIST"/>
                <cascade type="MERGE"/>
            </cascades>
            <cacheConfig usage="NONE" />
        </defaultManyToOneConfig>
        
        <defaultOneToManyConfig orphanRemoval="true">
            <cascades>
                <cascade type="ALL"/>
            </cascades>
            <cacheConfig usage="NONE" />
        </defaultOneToManyConfig>
        
        <defaultOneToOneConfig fetch="LAZY">
            <cascades>
                <cascade type="NONE"/>
            </cascades>
            <cacheConfig usage="NONE" />
        </defaultOneToOneConfig>
        
        <defaultInverseOneToOneConfig fetch="LAZY">
            <cascades>
                <cascade type="ALL"/>
            </cascades>
            <cacheConfig usage="NONE" />        
        </defaultInverseOneToOneConfig>
        
        <defaultManyToManyConfig>
            <cascades>
                <cascade type="PERSIST"/>
                <cascade type="MERGE"/>
            </cascades>
            <cacheConfig usage="NONE" />        
        </defaultManyToManyConfig>
        
        <defaultInverseManyToManyConfig>
            <cascades>
                <cascade type="ALL"/>
            </cascades>
            <cacheConfig usage="NONE" />
        </defaultInverseManyToManyConfig>
	<!-- ... skip stuff ... -->
	</configuration>
{% endhighlight %}



### 3.0.96 (2013-02-14)

[Sample generated app diff 3.0.95-3.0.96](https://github.com/jaxio/generated-projects/commit/b839b156fa7e9143efd20a72bffaac5a481394aa) 

Many thanks to Brice Leporini, Jean-Louis Boudart, Pierre-Henri Dezanneau and Vincent Beretti for their ideas, feedbacks and patches.

##### Front End (without spring web flow)
* do not use conversation's entity manager for search pages
* skip entityManager binding for ajax request coming from x-to-one auto-complete source
* rename PersistenceContextConversationListener to EntityManagerConversationListener and other renamings
* leverage org.springframework.web.filter.DelegatingFilterProxy so we can inject beans in our filter
* Introduce ConversationHolder to store the current Conversation in a static ThreadLocal field.
* Leverage @PostConstruct in XxxEditForm and no longer create XxxEditForm manually. It simplifies ConversationScope class.
* fix onSelected callback of bidirectional many-to-many
* popCurrentContextOnNextPause is now an int to count the number of contextes to pop. New name is popContextOnNextPauseCounter. You can pop more than 1 context during a request process.
* ConversationContext.getVar is now public
* make GenericLazyDataModel.edit(E selectedRow) and select(E selectedRow) protected
* downgrade primefaces from 3.5 to 3.4.2
* remove 'send' action and button as it confuses people

##### Front End (with spring web flow)
* no changes

##### JPA2 Backend
* upgrade from hibernate 4.1.4.Final to 4.1.9.Final
* use hibernate.connection.release_mode=after_transaction to prevent connection leak
* default jdbc pool size set to 1 to detect upfront any jdbc leak
* derby profile uses derby version 10.9.1.0

### 3.0.95 (2013-02-06)

[Sample generated app diff 3.0.94-3.0.95](https://github.com/jaxio/generated-projects/commit/2cb13258e2a137cae3b12dcf1fb4aa49d6bef3cf) 

##### Front End (without spring web flow)
* upgrade from primefaces 3.4.2. to primefaces 3.5
* rename the various public pushXxx to setNextContextXxx for better clarity
* no longer lazy load xToMany list data model (to please jrebel)
* defer pop until we pause conversation to avoid bean recreation
* remove the contextPopped from conversation listener as we cannot fully guess the future functional need
* remove isDirtyCheck as it leads to freaky insert
* provide a conversationDebug tag for debug/learning purposes
* no longer create entityManager during conversation creation => instead let conversation resuming handle it
* prevent npe during potential ajax race condition

##### Front End (with spring web flow)
* no changes

##### JPA2 Backend
* no changes

### 3.0.94 (2013-02-02)

[Sample generated app diff 3.0.93-3.0.94](https://github.com/jaxio/generated-projects/commit/ad9dbb6350a5af601b9798638d46149a37c71637) 

##### Front End (without spring web flow)
* use omnifaces gzip filter instead of ehcache one
* fix: release Jdbc connection when pausing the conversation, see PersistenceContextConversationListener
* fix: selectOneMenu is now referencing p:selectOneRadio + css fix
* upgrade schema version in faces-config.xml
* use proper JSTL path in panel/search.xhtml (bug found using my faces which is less tolerant than mojarra...)
* fix little details to make it work nicely with MyFaces

##### Front End (with spring web flow)
* fix: introduce AvoidLeakJpaFlowExecutionListener to circumvent https://jira.springsource.org/browse/SWF-1525
* fix: selectOneMenu is now referencing p:selectOneRadio + css fix

##### JPA2 Backend
* leverage QueryParser.escape in HibernateSearchUtil
* add extraParameters in SearchParameters + typo fix


### 3.0.93 (2013-01-29)

[Sample generated app diff 3.0.92-3.0.93](https://github.com/jaxio/generated-projects/commit/dcb20404903ed585d65510b9e952138ebc0577c9) 

##### Front End (without spring web flow)
* minor refactoring (no longer use preRenderView event)
* log context info are now set properly
* uses Primefaces datatable multi selection for many to many association
* fix: selectOneMenu is referencing selectOneRadio
* fix: configuring an enum as ordinal breaks compilation

##### Front End (with spring web flow)
* fix: selectOneMenu is referencing selectOneRadio
* fix: configuring an enum as ordinal breaks compilation


### 3.0.92 (2013-01-22)

[Sample generated app diff 3.0.91-3.0.92](https://github.com/jaxio/generated-projects/commit/b61febe3b9d8e7f87a4a2f75271bda44326ea5d6) 

##### Front End (without spring web flow)
* important code refactoring

### 3.0.91 (2013-01-14)

[Sample generated app diff](https://github.com/jaxio/generated-projects/commit/5d46df4459c73250c1e6da43c95fe668bb27f1aa) 

##### Front End (without spring web flow)
* use breadCrumb in conversation
* align label with css (not js)

##### Front End (with spring web flow)
* align label with css (not js) 

##### JPA2 Backend
* no changes

##### Core Celerio
* introduce celerioTemplateContext (pro user only)

### 3.0.90 (2013-01-10)

##### Front End (without spring web flow)
* upgrade mojarra from 2.1.10 to 2.1.17 (this was helpful http://forum.primefaces.org/viewtopic.php?f=3&t=25822)
* upgrade omnifaces from 1.2 to 1.3 
* refactor the web.conversation package for the better

##### Front End (with spring web flow)
* upgrade mojarra from 2.1.10 to 2.1.17 (this was helpful http://forum.primefaces.org/viewtopic.php?f=3&t=25822)

##### JPA2 Backend
* no changes

### 3.0.89 (2012-12-20)

##### NEW!
* introduce a new option without spring web flow. We encourage you to switch to it and report us feedbacks.

##### Back end
* Possibility to configure left Join in search by example
* composite pk var name changed to 'id'.
* provide oracle script for sample db and create-db-user profile
* rename persistence.xml to cope with jboss
* remove contains method in entity

##### Front end
* all remove/delete dialogs are now contextual
* rename SearchFormBase to GenericSearchForm
* cache resources ( com.sun.faces.defaultResourceMaxAge context-param in web.xml)
* remove before/after placeholder in tags (was a bad idea)
* fix component not found error due to invalid for attribute in label component
* better ask for delete dialog placement (no longer present in layout)
* upgrade to theme 1.0.9
 
### 3.0.88 (2012-11-14)

* fix jpauniquevalidator when a proxy is used
* when composite unique keys names are available, use them
* validate simple and composite unique constraints in the controller
* add search mass indexer
* no longer need to override getByCompositePkPredicate when you have a composite pk

### 3.0.87 (2012-10-22)

* remove erroneous legend for edit form
* fix spring application context hierarchy,
* fix converters when pk is a date
* restore row selection (onclick)


### 3.0.86 (2012-10-17)

* fix cache names!
* fix invalid orm xsd url
* facelet tag refactoring
* when closing edit form, now go back to the select view instead of homepage.
* rename PersistableHashBuilder to IdentifiableHashBuilder
* when using app:selectManyBoolean and app:selectManyEnum display the null values only if the attribute is not required
* use printers (replace formatters)
* move JpaUniqueSupport to backend and rename it to JpaUniqueUtil


### 3.0.85 (2012-10-09)

* no longer use c:if and c:forEach in messages component. Instead use rendered and ui:repeat
* use div instead of span to please html checker
* keep track of flow even in sub flows
* remove useless css settings
* change font size from 11 to 12
* use primefaces tag for selectOneRadio
* for better code factorization : introduce toSearchParameters in XxxForm
* save search feature (relies on conventions)
* maxResults simplification: -1 means no limit
* use facelet tag instead of composite component for outputLabel as it insert an intermediate id in certain cases.
* cleanup flowsMenuHandler, reuse Entityconverters in a TypeAwarePrinter
* introduce getPluralableProperty in PropertyUtils. Use it to localize searchResultsRegion. Use it to localize form error intro
* enable by default pre-post-annotations security
* work on audit log using hibernate listener
* add audit panel to see the last modification date/author
* do not try to be smart with @Column(name), always set the name as found  
  in the metadata, as oracle is case sensitive when using collision column names
* In default database example, add audit info in account entity.
* sort search result by many-to-one property  
* search on many-to-one field

### 3.0.84 (2012-09-26)

* Upgrade jibx from 1.2.1 to 1.2.3. Only Eclipse elements (related to code formatting) are namespaceless.
* No longer generate Primefaces code related to file upload/download in entity. 
  Instead we rely on the controller + a dedicated class XxxUploadHandler
* fix flow: from the same flow, doing 0/ search 1/select 2/close 3/new was 
  loading the item selected during step 1 instead of proposing a fresh empty bean.
* fix charset encoding for non-ajax request!
* provide our own form reset as default one is not complete.
* remove find(String) methods from repository.
* add complete(String) method in controller
* remove flowExecutionContext from flows, use instead RequestContextHolder from java
* order by business key when relevant in XxxLazyDataModel and XxxController
* upgrade to PrimeFaces 3.4.1
* automatically create the Xxx_.java file (in regular user folder src/main/java) in case the corresponding entity Xxx.java is taken over.
* remove a System.out.println in maven-celerio-plugin
* rename Entity_.e.vm.java to EntityMeta_.e.vm.java to make sure it is executed after Entity.e.vm.java
 
### 3.0.83 (2012-09-20)

##### JPA2 backend
* add byNamedQuery in namedQueryUtil
* prevent var clash when self referencing entity
* support for localization in db schema. Ex: columns such as text_fr, text_en are detected by celerio 
which generate a getText() method which invoke the getter corresponding to the current locale.
* fix backend-jpa pom
* HTML content detection based on column name: contains '_html' instead of endsWith 'html'. It is also configurable ("html" attribute in columnConfig)
* SafeHtml annotation is now disabled by default. It is configurable (safeHtml element, child of columnConfig)
* entity: in copyTo remove the copy of the relations' ids

##### Hibernate Search support
* generate transverse hibernate search code only if at least one entity is indexed
* generate XxxPkBridge only if needed
* remove tika dependencies and code (too specific)
* FieldBridge is configurable (use the 'brigdeImpl' attribute of the 'indexField' element)
* introduce findTerm in Respository (use full text search). It is not wired in the view, it is up to the developer 
to change it from find to findTerm... easy

##### JSF2 WebFlow Primefaces
* add a reset button: unfortunately does not work with all components
* remove c:if from select page (use rendered instead)
* dynamic layout in selectManyEnum depending on items list size

##### Celerio
* collision is now under target/maven-celerio-plugin/collisions, in any circumstance
* we now generate bootstrap as all regular file (so pom get into collision)


### 3.0.82 (2012-09-17)

##### JPA2 backend
* change the maven resource substitution pattern from ${value} to @value@ so it does not interfer with the spring one
* enforce java 1.6.0-26 and above, as jpa2 utils we use will not compile
* fix domain localization if we do not generate in the same folder

##### JSF2 WebFlow Primefaces
* fix quit navigation (for case where new is pressed from an edit page and then quit is pressed)
* set severity to error for unique validator message

### 3.0.81 (2012-09-14)

##### JPA2 backend
* improve JPA search by example: take many-to-many association into account
* fix NPE on null booleans (regression)

##### JSF2 WebFlow Primefaces
* add jpa unique validator for jsf forms
* introduce XxxController  to do business validation and other conditional checks that are easier to implement in Java than in webflow's xml syntax
* contextual messages for status_saved_ok and status_deleted_ok
* better text for error message (take plural into account): there is one error / there are x errors
* use multiple autoComplete in search form for many-to-many associations.

### 3.0.80 (2012-09-11)

##### JPA2 backend
* Improve JPA search by example: take x-to-one association into account
* you can now add custom annotations on entities using celerio configuration

##### Hibernate Search support
* Hibernate Search is now configurable per entity and per column. In your entity config, 
use the 'indexed' property to index the entity and use the 'field' element to annotate a field.
Here is an example:
{% highlight xml %}
<entityConfig tableName="ACCOUNT" indexed="true">
	<columnConfigs>
        <columnConfig columnName="email">
                <indexedField store="YES" />
        </columnConfig>
	</columnConfigs>        
</entityConfig>
{% endhighlight %}


##### JSF2 WebFlow Primefaces
* upgrade to PrimeFaces 3.4
* changes in webflow navigation: after'close' or 'save' you go back to search page
* make faces message survive multiple redirections
* split EntityConfigConverter (customer demand, to ease overriding)
* outputBoolean component: no longer display cross icon when value is null
* rename xxxAutocomplete component to xxxAutoComplete, by analogy with primefaces.
* use multiple autoComplete in search form for x-to-one associations.
* Boolean are multi selectable in form
* Enums are multi selectable in form
* add icon for environment name depending on 'env_name' var

### 3.0.79 (2012-09-02)

##### JPA2 backend
* Upgrade jadira usertype from 3.0.RC1 to 3.0.RC3
* Fix package-info.java for repository subpackage
* Upgrade to spring security 3.1.2

##### JSF2 WebFlow Primefaces
* Upgrade to primefaces 3.4-SNAPSHOT
* Use primefaces twitter bootstrap theme 1.0.8
* Upgrade to mojara 2.1.10 (as on prime labs demo site)
* Better partial rendering with dataTable when a row is deleted (see prime enhancement http://blog.primefaces.org/?p=2119)

<hr/>

### 3.0.78 (2012-08-31)

We have decided to focus our effort on JPA2 backend and JSF2/PrimeFaces front.
So currently other options (spring data, spring mvc/jquery) are no longer available, if you need these, please contact us.

##### JPA2 backend
* Upgrade to Hibernate 4.1.4.Final
* Upgrade to Spring Framework 3.1.2.RELEASE
* Upgrade to Spring Security 3.1.1.RELEASE
* Search by example using JPA2
* Search by range for all types (BigInteger, Date, Integer, etc.)
* No more Interface for DAOs
* Rename all XxxService classes to XxxRepository
* Generate Entity metamodel (@StaticMetamodel)
* Simplify the use of spring security context
* First basic support of Hibernate Search

##### JSF2 WebFlow Primefaces
* Upgrade to primefaces 3.3.1
* Upgrade to Spring Web Flow 2.3.1.RELEASE
* Use flow inheritance to reduce the amount of webflow code
* Support search by range for all types (BigInteger, Date, Integer, etc.)
* Introduce some facelets components

<hr/>

### 3.0.74 (2012-04-01)

##### backend common to all projects
* upgrade to springframework 3.0.7.RELEASE
* do not specify nullable = false and unique = true in the column specifying a simple PK to please topLink ddl generation
* dos2unix on all resources
* add missing @Override
* better javadocs

##### Spring data
* refactoring of the support classes

##### JSF front
* upgrade to spring webflow 2.3.1
* upgrade to mojarra 2.1.7
* upgrade to Primefaces 3.2 and theme 1.0.4
* changes in exception handling (refer to SimpleExceptionHandler.java)
* better focus managment on home (useful for accessibility)
* fix fileUpload and Ajax (see https://jira.springsource.org/browse/SWF-1526 )
* remove spel from converters
* add caching in ResourcesUtil
* rename ```GenericConverter``` to ```GenericJsfConverter```
* use prod config mode instead of slowly dev mode
* disable webflow snapshoting by default
* fix typo in {TotalPages} in paginator template
* selenium support 
* remove PRIMEFACES_FILE_HANDLER module, use PRIMEFACES instead

##### Other versions updates
* upgrade junit from 4.8.1 to 4.10
* upgrade jackson from 1.5.2 to 1.9.4
* upgrade xstream from 1.2.2 to 1.4.2
* upgrade hibernate-jpa-2.0-api from 1.0.0.Final to 1.0.1.Final
* upgrade commons-lang version from 2.5 to 2.6
* upgrade h2 version from 1.3.157 to 1.3.164
* upgrade commons-fileupload from 1.2.1 to 1.2.2
* upgrade commons-io from 1.4 to 2.1 
* upgrade commons-codec from 1.4 to 1.6
* upgrade commons-digester from 2.0. to 2.1
* upgrade aspectj version from 1.6.8 to to 1.6.12
* upgrade mockito version from 1.8.5 to 1.9.0

##### Maven related update (generated pom)
* upgrade maven-jxr-plugin from 2.1 to 2.3
* upgrade maven-pmd-plugin from 2.4 to 2.7
* upgrade cobertura plugin to 2.5.1
* upgrade findbugs-maven-plugin from 2.3.1 to 2.4.0
* upgrade build-helper-maven-plugin from 1.5 to 1.7
* upgrade maven-antrun-plugin from 1.6 to 1.7
* upgrade maven-enforcer-plugin from 1.0 to 1.0.1
* upgrade maven-surefire-plugin from 2.4.3 to 2.12
* upgrade maven-javadoc-plugin from 2.6.1 to 2.8.1
* upgrade maven-failsafe-plugin from 2.7.2 to 2.12
* upgrade maven-compiler-plugin from 2.0.2 to 2.3.2
* upgrade maven-clean-plugin from 2.3 to 2.4.1
* upgrade maven-install-plugin from 2.3 to 2.3.1
* upgrade maven-resource-plugin from 2.4.1 to 2.5
* upgrade sql-maven-plugin from 1.4 to 1.5
* upgrade maven-war-plugin from 2.1-beta-1 to 2.2
* upgrade maven eclipse plugin from 2.6 to 2.9

<hr/>

### 3.0.73 (2012-02-14)
* fix typo in panelMenu.xml (jsf2 front, without spring data)
* Fix bootstrapring for certain pack.

<hr/>

### 3.0.72 (2012-02-14)

##### jsf2-primefaces webapp (with spring data backend)
* upgrade to Spring Data 1.0.3
* upgrade to PrimeFaces 3.1
* upgrade to PrimeFaces Theme 1.0.3

##### spring mvc webapp (with spring data backend)
* upgrade to Spring Data 1.0.3

##### backend (with spring data)
* upgrade to Spring Data 1.0.3
* fix compilation issue if no 'account' table is found

<hr/>

### 3.0.71 (2012-02-09)

#### Generation workflow update
It is now required to provide a valid email address.
During the first project generation you will be asked to validate your email address.

#### Spring Data support
The generated code is now using Spring Data 1.0.2 for backend, spring mvc and primefaces projects.
For the moment, we still provide some options to generate backend, spring mvc and primefaces projects as before.

#### upgrades

##### backend
* upgrade to hibernate 3.6.9.Final
* upgrade to joda time 2.0
* upgrade to ehcache 2.4.3

##### jsf2-primefaces front:
* Upgrade to mojara 2.1.6
* Upgrade to primefaces 3.0.1

##### spring mvc
* upgrade to urlrewrite 3.2

### 3.0.70 (2012-01-19)

##### jsf2-primefaces front:

* Remove all render fragments from flows as the update attribute on the command button is enough.
* Set "javax.faces.validator.BeanValidator.MESSAGE_detail={0}" in ValidationMessage properties files
* Remove workaround when "yes" is clicked inside askForSaveDialog (proper fix found)
* Remove deprecated "lazy" attribute in dataTable (see primefaces #2993)

##### pom.xml
* Downgrade maven plugin from 2.7 to 2.6

### 3.0.69 (2012-01-02)

##### jsf2-primefaces front:
* Better JSF navigation with possibility to conditionally skip bean validation. Please <a href="/2011/12/15/skip-jsf-validation-depending-on-action.html">read our blog entry</a> related to this major change. 
* Upgrade to PrimeFaces 3.0
* Better readonly view support (use outputText instead of disabled="true")
* Validate not null many to one association (unless inverse is present)

##### backend:
* Use @Size annotation instead of @Length annotation when javax.validation is present

##### maven (pom.xml)
* Use Hibernate validator annotation processor


### 3.0.68 (2011-12-08)

##### jsf2-primefaces front:
* Introduce SimpleExceptionHandler.java to handle exception during webflow event (ajax request) or transition (non ajax request). When the exception occurs during an event, an error message is displayed. When an exception occurs during a transition, we force a transition to the 'error' state which in turn ends the flow and display an error page
* Better general exception handling using ExceptionFilter.java.
* ExceptionFilter also handles gracefully session expiration during ajax request and send a JSF2 partial redirect to the login page.  

### 3.0.67 (2011-12-01)

##### jsf2-primefaces front:
* clean up localization files messages.properties and messages_fr.properties
* set main title depending on context (ie entity name)
* add contextual title to all command button for accessibility concern
* better accessibility and look for messages composite component (voice reading race condition fixed)
* better accessibility for dialogs 'ask for save' and 'ask for delete'.
* give the focus back to delete menu button when user click no inside ask for delete dialog
* better accessibility for datePicker composite component
* login page is now localized 
* fix 'redmond' background (make it white and not kind of pseudo white)
* messages composite component: fix error count (there could be more than 1 error per field...)
* messages composite component: use ordered list for errors
* messages composite component: fix tricky date bug (visible only for days > 28) in DatePickerHelper
* remove pure one-to-one 'contact info' from example

##### jsf2 without webflow (private front)
* support save (using merge)
* add custom spring scope (ViewScope)
 
##### backend:
* rename all 'logger' to 'log', in case we want to leverage lombok
* add 'merge' to generic DAO
* extract DAOHibernate.getCriteria redundant code to HibernateUtil
* add links to javadoc
* fix compilation bug when a column is unique and mapped to an Enum 

##### misc
* normalize Logger initialization
* renamed PaddingConverter.NOTASTRING to PaddingConverter.NOT_A_STRING

##### celerio engine
* better convention for searchResult to avoid listing redundant parent in one to many list


### 3.0.66 (2011-11-25)

##### jsf2-primefaces front:
* Capture 'Enter' keypress and use it to trigger click() on the expected submit button
* Move Save/Submit and Search buttons below input/select fields (introduce saveButton tag)
* Move 'Active Flows' menu to the right
* Aria landmarks revisited (simpler)
* Remove fieldset around x-to-one association
* Remove some useless 'fId' attributes from tags
* On home page, we now omit links to flows that can only be used as subflows.

### 3.0.65 (2011-11-17)

##### jsf2-primefaces front:
* display a contextual info message each time the model is changed but no saved in database
* move language switch to the top right corner
* fix many to one autocomplete (itemValue was removed in 3.0.64, it is now back)

##### backend
* rename GenericEntityService 'autoComplete' method to 'find' for consistency
* generate labels for onetomany relation


### 3.0.64 (2011-11-14)

##### jsf2-primefaces front:
* fix datePicker composite component
* remove useless code related to webflow menus.
* light refactor in entity's root flow


### 3.0.63 (2011-11-10)

##### jsf2-primefaces front:
* upgrade to primefaces 3.0.M4 and themes 1.0.2 
* introduce and use an accessible datePicker composite component. It supports bean validation, joda time, etc.
* introduce and use an accessible messages component
* fix mains.js to make the layout work when chromeshades is used
* reduce dependency on SWF (messageUtil no longer depends on messageContext)
* get rid of all XxxItems class (the 'getLabel' is replaced by 'print' in GenericConverter)
* get rid of XxxConverter class (actually, they are now regrouped in EntityConverterConfig)
* use SPEL to print entity as string (see GenericConverter)
* deleteButton now appear once a new entity is saved (and may be deleted)
* finally found why enable/disable was not working in flow menu
  ==> fix it and refactor it for better clarity => simpler code/logic
* introduce TabBean to track tab activeIndex
* fix tricky issue with bean validation localization message (i.e. need empty english file)

##### backend
* fix compilation bug when pk is an enum (thanks to Stéphane Cros for reporting it)

### 3.0.62 (2011-10-27)

##### jsf2-primefaces front:
* upgrade to bean validation 4.2.0.Final (was 4.1.0.Final)
* use bean validation instead of webflow validation. No longer generate XxxValidator...
* upgrade to mojarra 2.1.3
* fix char encoding for partial ajax response + IE8
* fix aria-live region (we must use 'additions' instead of 'assertive'... took me weeks to realize that!)
* fix validation for sub edition
* use 'separator' instead of 'divider' in toolbar
* use callback param to update searchResultsRegion aria live region
* use tabview and tab for x-to-many relations
* move dialog down so the command button are not used by default by IE
* webflow simplification: no longer need action-state, instead use event handler and js call using primefaces js server api
* remove bottom buttons in sub edit page (less links for accessibility)
* clean up navigation bar for sub edit and sub select
* remove startup listener
* in edit flow: fix removeXxx and ajax update (using tabs)
* better usage of ajaxStatus (no mix between facet and attribute)
* paginator look and feel harmonization
* in pom.xml remove plugins we don't really care of

### 3.0.61 (2011-10-14)

##### jsf2-primefaces front:
* Fix datatable selection for Firefox and Safari (was OK with Chrome) 
* Replace Select subflow in popup (not accessible enough) by regular Select subflow.
* Introduce auto-complete for Select as an alternative to regular Select subflow
* Refactor the view to use only 1 form and avoid the bug https://jira.springsource.org/browse/SWF-1492
* Since we now use 1 form, remove some useless JavaScript code
* Active flow menu is now fully operational
* Refactor askForSaveDialog appearance logic: remove decision-state from XxxEditFlow.xml and use instead
  Primefaces RequestContext.getCurrentInstance().execute("some javascript") to decide if it should 
  be displayed or not. See generated PrimeFacesUtil.java
* Fix menuitem label in main.css (was not displayed!)

##### backend
* Remove @Transactional annotation from DAO methods (redundant with the one on Service methods)

### 3.0.60 (2011-10-07)

##### jsf2-primefaces front:
* remove bunch of facelet to keep things simpler
* some wai-aria integration (search, form error message, etc.) 
* use PrimeFaces 3.0.M4-SNAPSHOT
* server side pagination using LazyDataModel
* tweak p:layout to make it work with ChromeShades plugin
* custom composite component to display boolean value
* re-introduce active flow menu to switch from flow to flow (in progress)
* use ajax for save call
* use p:spinner for integer and long (fixed recently by primefaces)
* no longer need hack under web/el Use instead MessageBundle which is declared in faces-config

##### jsf2-primefaces and spring-mvc-3 front:
* upgrade from jetty 6 to jetty 7 

### 3.0.57 (2011-09-19)

##### jsf2-primefaces front:
* pay special attention to keyboard navigation and focus for accessibility concern
* fix some page and layout to please achecker accessibility tool.
* use p:layout
* make dialogs modal
* do partial rendering when removing item from x-to-many dataTable
* rename various ids for better clarity


### 3.0.56 (2011-09-08)

##### jsf2-primefaces front:
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

### 3.0.55 (2011-07-27)

##### Database reverse:
* Make database reverse work for DB2 on Z/OS system
* Catalog and schema name were ignored (was working most of the time as we provide sensitive default for Oracle and DB2

##### backend pack
* Fix default value for attribute mapped to enum.
  For example assuming the civility colunm is mapped to CivilityEnum and its default valude in the database in "MR",
  instead of generating setCivility("MR"), we now generate setCivility(CivilityEnum.MR). Thanks to Aram Murguía.
* Fix SearchTemplate constructor by copy. List were passed by reference instead of being cloned.
* Fix some var name clashes occurring when a non foreign key attribute var name matches the var name used by convention for an x-to-one relation.  

##### jsf2 primefaces pack
* Fix url-pattern in web.xml ('*' ==> '/*'), thanks to Aram Murguía

### 3.0.52 (2011-07-11)

##### Remote logs:
* Generation logs are now sent by email along with extracted metadata.
* Fix archetype to take into account email entered in springfuse generation form.

### 3.0.51 (2011-07-07)

##### Celerio engine:
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

##### spring mvc 3 front:
* Move up the character encoding filter and apply it to /** (thanks to unibail for tip)


### 3.0.50 (2011-06-16)

##Celerio engine:
* compilation fix for default value when the numeric type maps to BigInteger or BigDecimal
{% highlight java %}
  // we had for example (compilation error)
  setPrice(0.0000);
  // we now generate:
  setPrice(new BigDecimal("0.0000"));
{% endhighlight %}

##### backend:
* jpa: generate @DateTimeFormat(pattern = DATE_FORMAT_PATTERN) instead of @DateTimeFormat(iso = DATE) to ease global modification of the formatted date. The DATE_FORMAT_PATTERN is statically imported from ResourcesUtil.

##### spring mvc 3 front:
* fix auto complete for many to one: in certain case, the binding was not working on the server side
* fix the contact us link in the generated app

##### jsf2-primefaces front:
* fix the contact us link in the generated app


### 3.0.49 (2011-05-24)
##### General

* no longer skip table without pk. Instead, look for:

  1. first non null unique column
  2. or first unique column
  3. or fall back to first column

* better logging message for property name clash and duplicate columns in metadata (Thanks to Lisa from Qualcomm)
* add getPackageNodeUp facility.

##### Improvements

* Specify mime types in web.xml (thanks to Björn Johansson)

##### maven-springfuse-plugin:

* dump reversed metadata to target/reversed-metadata.xml


### 3.0.48 (2011-05-18)
##### Fixes

* Fix file move (see 3.0.47) when a file with the same name is already present in the collision folder. Classes not located in the project root package would not have been picked up


### 3.0.47 (2011-05-11)
##### General
* The springfuse remote generation plugin now streams the generation logs from our server.
* better logging message for property name clash and duplicate columns in metadata (Thanks to Lisa from Qualcomm)
* Fix @Column mapping for reserved column name whose var name is the same as the column name
{% highlight java %}
@Column(name ="`VALUE`")  //
  public String getValue()...
{% endhighlight %}


### 3.0.46 (2011-05-04)
##### General

* Better quickstart example
* Change the save() implementation in HibernateGenericDao to support persist OR update of entities having either  auto generated id, manually assigned or composite pk.
* Fix equality issue when business key is a java.util.Date: use second precision instead of millisec to cope with Oracle which only store second precision.
* Fix delete propagation for one to one (inverse side) using orphanRemoval attribute, as for one to many.
* Fixed an infinite loop in XxxGenerator occurring when a bidirectional one to one relation was present.
* Search by pattern now searches in assigned primary keys (both simple primary key and composite primary keys)


##### Spring MVC 3 front option

* Totally revisited the look'n'feel and the navigation... for the better :-). Many thanks to Frédéric Pernot from Unibail-Rodamco for his precious feedbacks
* upgrade to jquery 1.5 <http://jquery.org/>
* enable ajax history <https://github.com/cowboy/jquery-bbq>
* use blueprint css framework <http://www.blueprintcss.org/>
* use jquery-ui <http://jqueryui.com/>
* upgrade jquery-validate <https://github.com/jzaefferer/jquery-validation>


##### JSF2/Primefaces front option

* Use embedded flow to renderer search flows in primefaces popup dialog
* File download/upload is now supported


### 3.0.43 (2011-02-08)
##### Introducing JSF2/Primefaces/Webflow pack
New Front end option: JSF 2 + PrimeFaces 2.2 + Spring WebFlow 2.2.1. 

Many thanks to <a href="http://www.linkedin.com/profile/view?id=35594474">Bernard Pons</a> (Architect at Banque de France), for sharing his expertise and vision on this front-end stack. 
Without him, you would not benefit from it.

### 3.0.41 (2011-01-06)

##### New
* You can new generate a backend only project...
* New: Possibility to configure 1 sequence per table. Please use sequenceName attribute in entityConfig.
  It will generate the corresponding @SequenceGenerator and @GeneratedValue annotations.
* New: generate validation annotations on simple primary key that are assigned manually.
* New: In XxxDaoImpl, add getByExampleExtraCriterions when the corresponding entity has simple PK and is manually assigned.
  This allows to perform search on pk field as any other field.
* New: Entities are sorted in alphabetical order in generated menus.
* Upgrade to Spring 3.0.5.RELEASE, Spring Security 3.0.5.RELEASE

##### Fixes
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


### 3.0.39 (2010-11-12)
##### New
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


### 3.0.33 (2010-10-14)
##### New
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

##### Fixes
* Fix cyclic package dependency that was due to format annotations
* No longer elect a table as an 'Account' table if it has a composite primary key.
   	

### 3.0.30 (2010-09-03)
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


### 2.8.22 (2010-01-04)

* Spring Web Flow: fix url when using non-root contexts. Thanks to Pierre Boned.


### 2.8.21 (2009-11-25)

* Spring Web Flow: Use the create subflow, in addition to the select subflow, to wire a many to one relation
* Spring Web Flow: display many-to-many relation in the review state
* no longer generate targetEntity attribute in ManyToMany association since we use generics
* fix XxxFormServiceImpl..java when a many to one points to itself.


### 2.8.19 (2009-11-11)

* Support case where @OneToMany's mappedBy attribute refers to an @EmbeddedId (occurs when the id is a composite primary key). 
  Thanks to Olivier Huber from <a href="http://www.zenika.com">Zenika</a> for reporting it.
* Fix a regression bug showing up in composite primary key class when one of the property is a Date. 
  Thanks to Ahmad Sousak from <a href="http://www.steria.com">Steria</a> for reporting it.
* Remove(Roll back) the default-lazy-init="true" that was recently added in applicationContext-scheduling.xml as it prevents the jobs from starting!. 
  Thanks to <a href="http://www.hikage.be/">Gildas Cuisinier</a> for taking the time to analyze it and report it.


### 2.8.18 (2009-09-24)

* New feature: generate flow menu. Please read <a href="http://blog.springfuse.com/2009/09/spring-web-flow-menus.html">our blog entry</a> to know more.
* Support for hibernate filters in flows thanks to a special flow execution listener
* Refactor: 'boolean hasXxx()' on domain's model changed to '@Transient boolean isXxxSet()' for better clarity and compatibility with EL (expression language) in JSP/Flows etc.
* Refactor equals and hashCode


### 2.8.17 (2009-09-21)

* Upgrade from Spring 2.5.6 to Spring 2.5.6.SEC01 and no longer use spring.jar. We use instead spring-orm.jar etc... as for Spring 3.0 which is coming soon :-)
* Upgrade from SpringSecurity 2.0.4 to 2.0.5.RELEASE
* Upgrade from Hibernate 3.2.6.ga to hibernate-core 3.3.2.GA / EntityManager 3.4.0.GA
* Upgrade Hibernate Validator from 3.0.0.ga to 3.1.0.GA
* Upgrade from SpringWebFlow 2.0.7 to 2.0.8.RELEASE
* JPA annotations are now set on getters instead of fields.


### 2.8.16 (2009-08-22)

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
		

### 2.8.15 (2009-07-05)

* Fix a compilation error (regression) in generated unit test when one of the composite primary fields maps to a Java Long (thanks to Stéphane Deraco for reporting it)
* Fix a compilation error occurring when one of the composite primary key fields maps to a date.
* Fix an incorrect redirection url after an update of a model having a composite pk (thanks to David Martin).


### 2.8.14 (2009-06-25)

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


### 2.8.9 (2009-06-18)

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


### 2.7.4 (2009-05-10)

* New! <b>Spring Web Flow</b> support:
 * For each entity, a create flow and a select flow are now generated. The select flow is used as a subflow in create flow whose entity has a many to one relation.
 * Make the MultipartFile property transient to support file upload in Spring Web Flow.
 * Add flow path in applicationContext-security-http.xml. By default only ROLE_ADMIN can access them.
 * Declare flows in spring/springmvc-webapp.xml
* Remove useless interface on SearchTemplate.... keep only impl version which now takes the name of the interface
* Fix a compilation error when a table reference itself (Thanks to Pierre Gaudin. for reporting it)
* Remove CollectionUtils.java as it was no longer used by the generated code.
* When a table has no pk, use the first non null unique index instead (Thanks to Bernard Pons)


### 2.7.3 (2009-04-09)
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


### 2.7.2 (2009-04-03)

* Use URLEncoder.encode(string, "UTF-8") to encode parameters that appears in search results' sort urls in XxxSearchForm.java files.


### 2.7.1 (2009-03-30)

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

### 2.7.0

* Add Springfuse version support in the project generation form (Thanks to Ian H. for requesting it).
  It allows you regenerate a project using an older version of Springfuse.
  Of course, we encourage you to switch to the latest release as soon as you can.
* Package reorganization: (Thanks to Steve T., it really makes more sense). Group domain classes (model, manager, dao, hibernate) that were in
  a dedicated sub package in the parent package. For example, the AccountModel package is now 'domain' instead of 'domain.account', etc.
* Package reorganization: to clearly separate domain related classes from the rest, move
  the classes that were in the 'hibernate' package to 'hibernate.support' or 'hibernate.listener' packages
* Package reorganization: to clearly separate domain related classes from the rest, move
  the classes that were in the 'dao' package to 'dao.support' package.

### 2.6.0

* Fix a compilation error when using a composite key having a date type (Thanks to Steve T. for reporting it)
* Make getQueryStringForSortableHeader method public on all search forms so it can be conveniently used from Freemarker views
  (needed by a user using Freemarker instead of JSP) and provide more getXxxSortStatusKey methods (i.e on primary keys).
* Fix AssertUtil.isFalse(Boolean). Note that it is not used in the generated code.
* Fix location of hibernate hbm files in JavaDoc of all XxxModel.java files.
* Cosmetic comments in Spring's configuration files


### Since 2009-03-13

* Fix a zip issue that was preventing windows to unzip properly the files at the root of the generated project (Thanks to Neil G. for reporting it)
* Add some instructions for tomcat 5.5 and tomcat 6.0 in the generated pom.xml.
* Change in the generated pom.xml concerning mysql users: use the org.hibernate.dialect.MySQLInnoDBDialect instead of the org.hibernate.dialect.MySQL5Dialect
* Minor changes in Spring application context files related to bean description (no impact, just documentation and cosmetic)


### Since 2009-03-06

* Fix hard coded reference to login/password/email setters that were preventing certain generated projects to compile.
* Fix a generation issue when the email column was not present in the auto detected Account table.
* Introduce isAccount method in the AccountContext for fined grained security.


### Since 2009-03-03

* Account table detection: accept the 'user_name' column as a candidate for the username.
* Use directly LocaleContextHolder instead of AccountContext in EmailServiceImpl to prevent NPE when using the EmailService from a cron job.
* Fix potential NPE in Context Interceptor: <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/web/servlet/HandlerInterceptor.html">the ModelAndView that the handler returned (can also be null)</a>
* Checkbox in all createForm.jsp/updateForm.jsp: fix path of default checked value. The bug was visible only in certain cases.
* Cosmetic in xml configuration: move bean descriptions from comments to description tag


### Since 2009-02-28

* Set currentAccountId to a dummy value in HibernateFilterContext


### Since 2009-02-27

* Fix the currentAccountId type in HibernateFilterContext: it was hard coded to String, it has now the same type as the primary key of the 'account' table.
* Circumvent a SpringJavascript bug similar to <a href="http://jira.springframework.org/browse/SJS-21">http://jira.springframework.org/browse/SJS-21</a> (thanks to Ian Hendry for reporting it).
* SearchTemplateImpl setters now return SearchTemplateImpl instead of SearchTemplate so builder pattern can be used.


### Since 2009-02-24

* Remove trailing div tag in show.jsp responsible for poor layout under IE (thanks to Ian Hendry)
* Fix duplication of the searchParameters.searchMode in the show.jsp page for each domain table (thanks to Ian Hendry)
* Fix a typo in the string ROLE_USER in the generated PasswordService interface that was preventing the user from changing his password (thanks to Steve T.)
* Provide two sets of velocity templates under src/main/resources/velocity/emails for email sent upon reset/change password.


### Since 2009-02-12

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


### Since 2009-02-03

* Remove common table prefix before generating variable/method/class name
* Clean primary key variable names
* Clean foreign key variable names
* Ignore foreign key that do not refer to a primary key instead of stopping the generation!
* Fix JSP domain page: There were few tags missmatch such as use a th instead of td in the pages show.jsp, createForm.jsp, updateForm.jsp
* Prevent action caching in urlrewrite.xml
* Ignore specific hibernate hilosequence table

