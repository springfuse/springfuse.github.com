---
layout: english
title: Celerio Guide - Conventions 
---

Conventions and integration
===========================

Celerio has some built-in conventions. When these conventions are
followed, Celerio generates cleaner Java code and some specific
features. For example, by simply following some columns naming
convention, you can rely on Celerio to generate all the infrastructure
code and configuration that will allow you to handle file upload and
download in your web application, in an optimal way.

Camel case conventions
----------------------

### Underscore '\_' Enables Java Camel Case Syntax

'Camel Case' syntax is standard Java code convention. When Celerio
encounters the character underscore '\_' in a table’s name or a column’s
name, it skips it and converts to upper case the next character when
generating classes, variables or methods related to this table, or
column.

For example, if your table name is BOOK\_COMMENT , the generated entity
class will be named BookComment ; a variable holding BookComment
instance will be named `bookComment` and a setter will be named
setBookComment , etc.

### Native camel case support

If your table's and/or column's name use a camelCase syntax AND if the
JDBC driver preserves this syntax, then Celerio takes it into account
when generating classes, variables or methods related to this table, or
column.

For example, if your table name is bankAccount , the generated entity
class will be named BankAccount ; a variable holding BankAccount
instance will be named `bankAccount` and a setter will be named
setBankAccount , etc.

Choosing explicit names for your tables and columns is thus very
important as it improves your source code readability without the burden
of relying on configuration.

Primary key conventions
-----------------------

### Numerical Primary Keys

Each numerical primary key column is mapped with `@GeneratedValue` and
`@Id` annotations.

> **Important**
>
> If your database does not support identity columns, you should create
> the sequence 'hibernate\_sequence'. Please refer to Hibernate
> reference documentation for more advanced alternatives.

### Primary Keys with 32 characters

By convention, for all primary keys that are char(32), Celerio maps the
column with the following annotations

{% highlight java %}
@GeneratedValue(generator = "strategy-uuid")
@GenericGenerator(name = "strategy-uuid", strategy = "uuid")
@Id
{% endhighlight %}

annotations. so it uses Hibernate's UUIDHexGenerator. Therefore no
sequence is needed for these primary keys.

### Other Primary Keys

For primary key that are char(x) where x is different from 32, Celerio
map the column with an "assigned" generator, which means you must
provide manually the primary key value.

The 'Account' table
-------------------

The Account table is a special table that contains the user's login and
password columns and eventually the email and enabled columns. It has an
important role during the login phase. It is also used by the
AccountContext generated class which store the current `account`
information in the current thread.

Celerio detects automatically your 'Account' table. An account table
candidate is expected to have at least the following columns:

  Column's name                                                         Mapped Java Type   Description
  --------------------------------------------------------------------- ------------------ ----------------------------------------------------------------------------------
  "username" OR "login" OR "user\_name" OR "identifiant"                String             Login used by the end user to authenticate to this web application
  "password" OR "pwd" OR "passwd" OR "mot\_de\_passe" OR "motdepasse"   String             Password (in clear) used by the end user to authenticate to this web application

  : Account table conditions

If no Account table candidate is found, Celerio will do as if it had
found one and will generate a mock Account DAO implementation that
returns 2 dummy users (user/user and admin/admin) instead of generating
a real JPA DAO implementation. It is up to you to replace this DAO
implementation with your own implementation.

> **Note**
>
> You may also elect the account table by configuration.

The 'Role' table
----------------

The Role table is a special table that contains the account's roles. To
be detected by Celerio, it must have a many-to-many or a many-to-one
relationship with the found 'Account' table and contain the following
mandatory column:

  Column's name                                             Mapped Java Type   Description
  --------------------------------------------------------- ------------------ ------------------------------------------------------------------------------------------
  "authority" OR "role\_name" OR "role" OR "name\_locale"   String             The generated code relies on the following authority's values: `ROLE_USER`, `ROLE_ADMIN`

  : Role table conditions

Here is a sample SQL script (H2 Database) that complies to Celerio
conventions

    CREATE TABLE ACCOUNT (
        account_id char(32) not null, login
        varchar(255) not null,
        password varchar(255) not null,
        email varchar(255) not null,

        constraint account_unique_1 unique (login),
        constraint account_unique_2 unique (email),
        primary key (account_id)
    );
    CREATE TABLE ROLE (
        role_id smallint generated by default as identity,
        name_locale varchar(255) not null,

        constraint role_unique_1 unique (name_locale),
        primary key (role_id) 
    );
    CREATE TABLE ACCOUNT_ROLE (
        account_id char(32) not null,
        role_id smallint not null,

        constraint account_role_fk_1 foreign key (account_id) references ACCOUNT,
        constraint account_role_fk_2 foreign key (role_id) references ROLE,
        primary key (account_id, role_id) 
    );

Other optional account's columns
--------------------------------

### The Email column

If the detected Account table has an email column, it is used by the
generated code in few places, mostly as an illustration of the
EmailService usage.

  Column's name                                       Mapped Java Type   Description
  --------------------------------------------------- ------------------ -------------------
  "email", "email\_address", "emailAddress", "mail"   String             The user's email.

  : Account's table email column conditions

### The Enabled column

If the detected Account table has an enabled column, it is used by the
generated code related to Spring Security integration.

  Column's name                               Mapped Java Type   Description
  ------------------------------------------- ------------------ -------------------------------------------------
  "enabled" OR "is\_enabled" OR "isenabled"   Boolean            Only enabled users (enabled == true) can login.

  : Account's table enabled column conditions

Special columns for file handling support
-----------------------------------------

When the following columns are present simultaneously in a table,
Celerio generates various helper methods to ease file manipulation from
the web tier to the persistence layer.

-   'prefix'\_FILE\_NAME (String)

-   'prefix'\_CONTENT\_TYPE (String)

-   'prefix\_SIZE or 'prefix'\_LENGTH (int)

-   'prefix'\_BINARY (blob)

<!-- -->

    mydoc_content_type       varchar(255)    not null,
    mydoc_size               integer         not null,
    mydoc_file_name          varchar(255)    not null,
    mydoc_binary             bytea,

This convention will allow you to upload a file transparently, save it
to the corresponding table, then download it using a simple URL.

ACCOUNT\_ID column & Hibernate Filter
-------------------------------------

When a table contains a foreign key pointing to the Account table,
Celerio assumes that the content of this table belongs to the user
represented by the account\_id foreign key.

An hibernate filter is configured to make sure that this table is loaded
only by the current user.

The filter is enabled by the `HibernateFilterInterceptor`. Of course
this default behavior may not always suit your needs. There are two ways
of disabling it:

1.  Remove the `@Filter` annotation from the Entity. This imply taking
    control over the entity.

2.  Disable the filter programmatically using the HibernateFilterContext
    generated helper.

3.  Disable globally this convention in Celerio's configuration file.

Version column and Optimistic Locking
-------------------------------------

If your table has a column named VERSION whose type is an int, Celerio
assumes by convention that you want to enable an optimistic locking
strategy. As a result, the property is annotated with `@Version` .

Many to many and inverse attribute
----------------------------------

Which side of the relation is marked as inverse="true" ? By convention,
the side whose corresponding column's order is the highest on the
"Middle table".
