## Spring and Spring Boot
> Spring 5.x, Spring Boot 2.x，所有管理的事情Spring Boot用一个很简单的包来帮你管理所有别的包，二者是一回事，Spring Boot相比原生的Spring主要有3个优点：
>* Simplify dependencies
>* Simplify all bean configurations
>* Spring Boot has built-in servers like Tomcat and Jetty

> Spring从四方面来掌握 ：
>* IoC Container
>* Spring how to manages all beans
>* Spring Proxy
>* Spring is an Integrator

1.       Scope in Spring IoC

Scope: singleton, prototype, request, session. globalSession

prototype is a shallow copy.

2.       Autowire in Spring IoC

Autowire: no, byname, byType, constructor, autodetect

3.       How to inject a singleton in Spring IoC?

Set factory-method=”getInstance”. Otherwise, it will create more than one object.

4.       Difference between BeanFactory and ApplicationContext?

ApplicationContext is more powerful than BeanFactory. Each bean in BeanFactory is lazy-loaded by default, but not lazy-loaded in ApplicationContext. To make a bean lazy-loaded in ApplicationContext, we can set lazy-init=”true”.

5.       Difference advices in Spring AOP

Intercept around, before, after returning, after throwing, after

6.       Workflow of Spring MVC.

7.       Three mappings in Spring MVC

SimpleUrlHandlerMapping, BeanNameUrlHandlerMapping, CommonsHandlerMapping

8.       How to handle multiple submit buttons in Spring MVC?

Use MultiActionController

9.       How does Spring integrate with Struts?

Three ways:

(1)    Use ActionSupport instead of Action

(2)    Add a controller in struts-config.xml file and the controller is DelegatingRequestProcessor

(3)    Change the type of each action to DeletaingActionProxy

10.   Spring Transaction Management.

Spring framework provides a generic abstraction layer for transaction management. This allowing the developer to add the pluggable transaction managers, and making it easy to demarcate transactions without dealing with low-level issues. Spring's transaction support is not tied to J2EE environments and it can be also used in container less environments.

11.   Spring Application Contexts

There are three well known Application Context in Spring used to Bean wiring.

Types of Application Contexts:
•ClassPathXmlApplicationContext
Loads a context definition from an XML file located in the classpath, treating context definition files as classpath resources.
• FileSystemXmlApplicationContext
Loads a context definition from an XML file in the file system.

• XmlWebApplicationContext
Loads context definitions from an XML file contained within a web application.



Hibernate

1.       Hibernate caching

·         Hibernate has two levels of caching. First-level caching is on Session; second-level caching is on SessionFactory. Caching on Session is by default; Caching on SessionFactory needs to be configured.

·         Each object has three status in a session: attached(persist), detached, transient. It can be converted from attached to detached status by calling evict() method or clear() method; it can be converted from detached to attached status by calling save(), update() or merge() method. If an object is in transient status, it lost its id and cannot come back to attached status.

·         Use update() if you are sure that the session does not contain an already persistent instance with the same identifier, and merge() if you want to merge your modifications at any time without consideration of the state of the session.

·         Caching is a good mechanism to improve the performance of Hibernate and save memory. However, it results problem for batch processing, in which case Hibernate saves big amount of data to the database. In this case, we have two ways to solve it.

(1)    We set a counter. Everytime it reaches 100, we call session.clear() method to clear the session.

(2)    We use StatelessSession to do the transaction

2.       Mapping for class hierarchy.

There are three ways.

(1)    Table per class hierarchy. In this way, we only create one table and use discriminator to identify different subclasses.

(2)    Table per subclass. In this way, we build a table for each class and use join-subclass block in the mapping file.

(3)    Table per concrete class. In this way, we only build tables for each subclass and use union-subclass in the mapping file.

3.        Hibernate call native SQL.

Two ways:

(1)    Write a sql-query block in the mapping file and write the native SQL in the block, then call session.getNamedQuery to invoke the query.

(2)    Call method session.createSQLQuery directly to run the query. It might use addEntity method to guarantee that the query returns objects.

4.       Hibernate call stored procedure.

Two ways:

(1)    Write a sql-query block in the mapping file, set callable=”true” and write the stored procedure in the block. This only works for Oracle because it returns a cursor.

(2)    Call session.connection() method to return a JDBC connection, then use CallableStatement to call the stored procedure. In this way, Hibernate is downgraded to JDBC.

5.       Difference between load and get methods

The method load uses proxy pattern. It returns a proxy object instead of a real object. When the user accesses the field of the object, then load method will run the query to get the real object. So load method lazy-loads the object. However, the method get will run the query directly and returns a real object. So when an object does not exist, get method will return null and load method will throw a runtime exception.

6.       Criteria in Hibernate

Hibernate provides Criteria to connect to database. The Criteria can use builder pattern to defines different restrictions of the data to search. It does not need the primary key of the object and thus is more flexible than load and get method.

7.       Lazy loading and LazyIntializationException

Say you have a parent and that parent has a collection of children. Hibernate now can "lazy-load" the children, which means that it does not actually load all the children when loading the parent. Instead, it loads them when requested to do so. You can either request this explicitly or, and this is far more common, hibernate will load them automatically when you try to access a child.

Lazy-loading can help improve the performance significantly since often you won't need the children and so they will not be loaded.

Also beware of the n+1-problem. Hibernate will not actually load all children when you access the collection. Instead, it will load each child individually. When iterating over the collection, this causes a query for every child. In order to avoid this, you can trick hibernate into loading all children simultaneously, e.g. by calling parent.getChildren().size().

 

8.       Difference between HQL and SQL

HQL is object-oriented and everything is related to class, object and field. SQL is relational and everything is related to table, alias and column.

9.       What if an HQL returns partial fields of a class?

It will get the list of object arrays.