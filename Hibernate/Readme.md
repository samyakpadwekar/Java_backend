### 1. What is ORM in Hibernate?
- Hibernate ORM stands for Object Relational Mapping.
- This is a mapping tool pattern mainly used for converting data stored in a relational database to an object used in object-oriented programming constructs.
- This tool also helps greatly in simplifying data retrieval, creation, and manipulation.
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/042/original/Object_Relational_Mapping.png" width="500">

### 2. What are the advantages of Hibernate over JDBC?
- The advantages of Hibernate over JDBC are listed below:
1. *Clean Readable Code*: Using hibernate, helps in eliminating a lot of JDBC API-based boiler-plate codes, thereby making the code look cleaner and readable.
2. *HQL (Hibernate Query Language)*: Hibernate provides HQL which is closer to Java and is object-oriented in nature.This helps in reducing the burden on developers for writing database independent queries. In JDBC, this is not the case.A developer has to know the database-specific codes.
3. *Transaction Management*: JDBC doesn't support implicit transaction management. It is upon the developer to write transaction management code using commit and rollback methods. Whereas, Hibernate implicity provides this feature.
4. *Exception Handling*: Hibernate wraps the JDBC exceptions and throws unchecked exceptions like JDBCException or HibernateException. This along with the built-in transaction management system helps developers to avoid writing multiple try-catch blocks to handle exceptions. In the case of JDBC, it throws a checked exception called SQLException thereby mandating the developer to write try-catch blocks to handle this exception at compile time.
5. *Special Features*: Hibernate supports OOPs features like inheritance, associations and also supports collections. These are not available in JDBC.

### 3. What are some of the important interfaces of Hibernate framework?
Hibernate core interfaces are:
1. Configuration
2. SessionFactory
3. Session
4. Criteria
5. Query
6. Transaction

### 4. What is a Session in Hibernate?
- A session is an object that maintains the connection between Java object application and database.
- Session also has methods for storing, retrieving, modifying or deleting data from database using methods like persist(), load(), get(), update(), delete(), etc.
- Additionally, It has factory methods to return Query, Criteria, and Transaction objects.

### 5. What is a SessionFactory?
- SessionFactory provides an instance of Session.
- It is a factory class that gives the Session objects based on the configuration parameters in order to establish the connection to the database.
- As a good practice, the application generally has a single instance of SessionFactory.
- The internal state of a SessionFactory which includes metadata about ORM is immutable, i.e once the instance is created, it cannot be changed.
- This also provides the facility to get information like statistics and metadata related to a class, query executions, etc.
- It also holds second-level cache data if enabled.

### 6. What do you think about the statement - “session being a thread-safe object”?
- No, Session is not a thread-safe object which means that any number of threads can access data from it simultaneously.

### 7. Can you explain what is lazy loading in hibernate?
- Lazy loading is mainly used for improving the application performance by helping to load the child objects on demand.
- It is to be noted that, since Hibernate 3 version, this feature has been enabled by default.
- This signifies that child objects are not loaded until the parent gets loaded.

### 8. What is the difference between first level cache and second level cache?
Hibernate has 2 cache types. First level and second level cache for which the difference is given below:
1. First Level Cache
- This is local to the Session object and cannot be shared between multiple sessions.
- This cache is enabled by default and there is no way to disable it.
- The first level cache is available only until the session is open, once the session is closed, the first level cache is destroyed.
2. Second Level Cache
- This cache is maintained at the SessionFactory level and shared among all sessions in Hibernate.
- This is disabled by default, but we can enable it through configuration.
- The second-level cache is available through the application’s life cycle, it is only destroyed and recreated when an application is restarted.
->If an entity or object is loaded by calling the get() method then Hibernate first checked the first level cache, if it doesn’t find the object then it goes to the second level cache if configured. If the object is not found then it finally goes to the database and returns the object, if there is no corresponding row in the table then it returns null.

### 9. What can you tell about Hibernate Configuration File?
- Hibernate Configuration File or hibernate.cfg.xml is one of the most required configuration files in Hibernate.
- By default, this file is placed under the src/main/resource folder.
- The file contains database related configurations and session-related configurations.
- Hibernate facilitates providing the configuration either in an XML file (like hibernate.cfg.xml) or a properties file (like hibernate.properties).
This file is used to define the below information:
- *Database connection details*: Driver class, URL, username, and password.
- There must be one configuration file for each database used in the application, suppose if we want to connect with 2 databases, then we must create 2 configuration files with different names.
- Hibernate properties: Dialect, show_sql, second_level_cache, and mapping file names.

### 10. How do you create an immutable class in hibernate?
Immutable class in hibernate creation could be in the following way.
- If we are using the XML form of configuration, then a class can be made immutable by markingmutable=false. The default value is true there which indicating that the class was not created by default.
- In the case of using annotations, immutable classes in hibernate can also be created by using @Immutable annotation.

### 11. Can you explain the concept behind Hibernate Inheritance Mapping?
- Java is an Object-Oriented Programming Language and Inheritance is one of the most important pillars of object-oriented principles.
- To represent any models in Java, inheritance is most commonly used to the relationship.
- But, there is a catch. Relational databases do not support inheritance. They have a flat structure.
- Hibernate’s Inheritance Mapping strategies deal with solving how hibernate being an ORM tries to map this problem between the inheritance of Java and flat structure of Databases.
- Consider the example where we have to divide InterviewBitEmployee into Contract and Permanent Employees represented by IBContractEmployee and IBPermanentEmployee classes respectively.  \
  Now the task of hibernate is to represent these 2 employee types by considering the below restrictions:
  1. The general employee details are defined in the parent InterviewBitEmployee class. 
  2. Contract and Permanent employee-specific details are stored in IBContractEmployee and IBPermanentEmployee classes respectively
- The class diagram of this system is as shown below:
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/043/original/Hibernate%E2%80%99s_Inheritance_Mapping.png" width="500">
  
### 12. Is hibernate prone to SQL injection attack?
- SQL injection attack is a serious vulnerability in terms of web security wherein an attacker can interfere with the queries made by an application/website to its database thereby allowing the attacker to view sensitive data which are generally irretrievable.
- It can also give the attacker to modify/ remove the data resulting in damages to the application behavior.
- Hibernate does not provide immunity to SQL Injection. However, following good practices avoids SQL injection attacks. It is always advisable to follow any of the below options:
  1. Incorporate Prepared Statements that use Parameterized Queries.
  2. Use Stored Procedures.
  3. Ensure data sanity by doing input validation.

### 13. Explain hibernate mapping file
- Hibernate mapping file is an XML file that is used for defining the entity bean fields and corresponding database column mappings.
- These files are useful when the project uses third-party classes where JPA annotations provided by hibernating cannot be used.
- In the previous example, we have defined the mapping resource as “InterviewBitEmployee.hbm.xml” in the config file. Let us see what that sample hbm.xml file looks like:
```
<?xml version = "1.0" encoding = "utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
"-//Hibernate/Hibernate Mapping DTD//EN"
"http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">

<hibernate-mapping>
   <!-- What class is mapped to what database table-->
  <class name = "InterviewBitEmployee" table = "InterviewBitEmployee">

     <meta attribute = "class-description">
        This class contains the details of employees of InterviewBit. 
     </meta>

     <id name = "id" type = "int" column = "employee_id">
        <generator class="native"/>
     </id>

     <property name = "fullName" column = "full_name" type = "string"/>
     <property name = "email" column = "email" type = "string"/>

  </class>
</hibernate-mapping>
```

### 13. What are the most commonly used annotations available to support hibernate mapping?
- Hibernate framework provides support to JPA annotations and other useful annotations in the org.hibernate.annotations package. Some of them are as follows:
1. javax.persistence.Entity: This annotation is used on the model classes by using “@Entity” and tells that the classes are entity beans.
2. javax.persistence.Table: This annotation is used on the model classes by using “@Table” and tells that the class maps to the table name in the database.
3. javax.persistence.Access: This is used as “@Access” and is used for defining the access type of either field or property. When nothing is specified, the default value taken is “field”.
4. javax.persistence.Id: This is used as “@Id” and is used on the attribute in a class to indicate that attribute is the primary key in the bean entity.
5. javax.persistence.EmbeddedId: Used as “@EmbeddedId” upon the attribute and indicates it is a composite primary key of the bean entity.
6. javax.persistence.Column: “@Column” is used for defining the column name in the database table.
7. javax.persistence.GeneratedValue: “@GeneratedValue” is used for defining the strategy used for primary key generation. This annotation is used along with javax.persistence.GenerationType enum.
8. javax.persistence.OneToOne: “@OneToOne” is used for defining the one-to-one mapping between two bean entities. Similarly, hibernate provides OneToMany, ManyToOne and ManyToMany annotations for defining different mapping types.
9. org.hibernate.annotations.Cascade: “@Cascade” annotation is used for defining the cascading action between two bean entities. It is used with org.hibernate.annotations.CascadeType enum to define the type of cascading.
- Following is a sample class where we have used the above listed annotations:
```
package com.dev.interviewbit.model;
import javax.persistence.Access;
import javax.persistence.AccessType;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.OneToOne;
import javax.persistence.Table;

import org.hibernate.annotations.Cascade;

@Entity
@Table(name = "InterviewBitEmployee")
@Access(value=AccessType.FIELD)
public class InterviewBitEmployee {

   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   @Column(name = "employee_id")
   private long id;

   @Column(name = "full_name")
   private String fullName;

   @Column(name = "email")
   private String email;
   
   @OneToOne(mappedBy = "employee")
   @Cascade(value = org.hibernate.annotations.CascadeType.ALL)
   private Address address;

   //getters and setters methods
}
```

### 15. Explain Hibernate architecture
- The Hibernate architecture consists of many objects such as a persistent object, session factory, session, query, transaction, etc.
- Applications developed using Hibernate is mainly categorized into 4 parts:
1. Java Application
2. Hibernate framework - Configuration and Mapping Files
3. Internal API -
  a. JDBC (Java Database Connectivity)
  b. JTA (Java Transaction API)
  c. JNDI (Java Naming Directory Interface).
4. Database - MySQL, PostGreSQL, Oracle, etc

<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/048/original/Hibernate_Architecture.png" width="300">

- The main elements of Hibernate framework are:
1. SessionFactory: This provides a factory method to get session objects and clients of ConnectionProvider. It holds a second-level cache (optional) of data.
2. Session: This is a short-lived object that acts as an interface between the java application objects and database data.
  a. The session can be used to generate transaction, query, and criteria objects.
  b. It also has a mandatory first-level cache of data.
3. Transaction: This object specifies the atomic unit of work and has methods useful for transaction management. This is optional.
4. ConnectionProvider: This is a factory of JDBC connection objects and it provides an abstraction to the application from the DriverManager. This is optional.
5. TransactionFactory: This is a factory of Transaction objects. It is optional.

<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/049/original/Hibernate_Framework_Objects.png" width="500">

### 16.Can you tell the difference between getCurrentSession and openSession methods?
- Both the methods are provided by the Session Factory. The main differences are given below:
1. getCurrentSession()
a. This method returns the session bound to the context.
b. This session object scope belongs to the hibernate context and to make this work hibernate configuration file has to be modified by adding <property name = "hibernate.current_session_context_class"> thread </property>. If not added, then using the method would throw an HibernateException.
c. This session object gets closed once the session factory is closed.
d. In a single-threaded environment, this method is faster than openSession().
2. openSession()
a. This method always opens a new session.
b. A new session object has to be created for each request in a multi-threaded environment. Hence, you need not configure any property to call this method.
c. It's the developer’s responsibility to close this object once all the database operations are done.
d. In single threaded environment, it is slower than getCurrentSession()single-threaded.
- Apart from these two methods, there is another method openStatelessSession() and this method returns a stateless session object.

### 17.Differentiate between save() and saveOrUpdate() methods in hibernate session.
- Both the methods save records to the table in the database in case there are no records with the primary key in the table. However, the main differences between these two are listed below:
1. save()
a. save() generates a new identifier and INSERT record into a database
b. The insertion fails if the primary key already exists in the table.
c. The return type is Serializable which is the newly generated identifier id value as a Serializable object.
d. This method is used to bring only a transient object to a persistent state.
2. saveOrUpdate()
a. Session.saveOrUpdate() can either INSERT or UPDATE based upon existence of a record.
b. In case the primary key already exists, then the record is updated.
c. The return type of the saveOrUpdate() method is void.
d. This method can bring both transient (new) and detached (existing) objects into a persistent state. It is often used to re-attach a detached object into a Session
- Clearly, saveOrUpdate() is more flexible in terms of use but it involves extra processing to find out whether a record already exists in the table or not.

### 18.Differentiate between get() and load() in Hibernate session
- These are the methods to get data from the database. The primary differences between get and load in Hibernate are given below:
1. get()
a. This method gets the data from the database as soon as it is called.
b. The database is hit every time the method is called.
c. The method returns null if the object is not found.
d. This method should be used if we are unsure about the existence of data in the database.
2. load()
a. This method returns a proxy object and loads the data only when it is required.
b. The database is hit only when it is really needed and this is called Lazy Loading which makes the method better.
c. The method throws ObjectNotFoundException if the object is not found.
d. This method is to be used when we know for sure that the data is present in the database.

### 19.What is criteria API in hibernate?
- Criteria API in Hibernate helps developers to build dynamic criteria queries on the persistence database.
- Criteria API is a more powerful and flexible alternative to HQL (Hibernate Query Language) queries for creating dynamic queries.
- This API allows to programmatically development criteria query objects.
- The org.hibernate.Criteria interface is used for these purposes.
- The Session interface of hibernate framework has createCriteria() method that takes the persistent object’s class or its entity name as the parameters and returns persistence object instance the criteria query is executed.
- It also makes it very easy to incorporate restrictions to selectively retrieve data from the database.
- It can be achieved by using the add() method which accepts the org.hibernate.criterion.Criterion object representing individual restriction.

-----

Usage examples:

To return all the data of InterviewBitEmployee entity class.
```
Criteria criteria = session.createCriteria(InterviewBitEmployee.class);
List<InterviewBitEmployee> results = criteria.list();
```
To retrive objects whose property has value equal to the restriction, we use Restrictions.eq() method. For example, to fetch all records with name ‘Hibernate’:
```
Criteria criteria= session.createCriteria(InterviewBitEmployee.class);
criteria.add(Restrictions.eq("fullName","Hibernate"));
List<InterviewBitEmployee> results = criteria.list();
```
To get objects whose property has the value “not equal to” the restriction, we use Restrictions.ne() method. For example, to fetch all the records whose employee’s name is not Hibernate:
```
Criteria criteria= session.createCriteria(InterviewBitEmployee.class);
criteria.add(Restrictions.ne("fullName","Hibernate"));
List<Employee> results = criteria.list()
```
To retrieve all objects whose property matches a given pattern, we use Restrictions.like() (for case sensitivenes) and Restrictions.ilike()(for case insensitiveness)
```
Criteria criteria= session.createCriteria(InterviewBitEmployee.class);
criteria.add(Restrictions.like("fullName","Hib%",MatchMode.ANYWHERE));
List<InterviewBitEmployee> results = criteria.list();
```
Similarly, it also has other methods like isNull(), isNotNull(), gt(), ge(), lt(), le() etc for adding more varieties of restrictions. It has to be noted that for Hibernate 5 onwards, the functions returning an object of typeCriteria are deprecated. Hibernate 5 version has provided interfaces like CriteriaBuilder and CriteriaQuery to serve the purpose:
```
javax.persistence.criteria.CriteriaBuilder
javax.persistence.criteria.CriteriaQuery

// Create CriteriaBuilder
CriteriaBuilder builder = session.getCriteriaBuilder();

// Create CriteriaQuery
CriteriaQuery<YourClass> criteria = builder.createQuery(YourClass.class);
```
For introducing restrictions in CriteriaQuery, we can use the CriteriaQuery.where method which is analogous to using the WHERE clause in a JPQL query.

-----

### 20.What is HQL?
- Hibernate Query Language (HQL) is used as an extension of SQL.
- It is very simple, efficient, and very flexible for performing complex operations on relational databases without writing complicated queries.
- HQL is the object-oriented representation of query language, i.e instead of using table name, we make use of the class name which makes this language independent of any database.
- This makes use of the Query interface provided by Hibernate. The Query object is obtained by calling the createQuery() method of the hibernate Session interface.
- Following are the most commonly used methods of query interface:
1. public int executeUpdate() : This method is used to run the update/delete query.
2. public List list(): This method returns the result as a list.
3. public Query setFirstResult(int rowNumber): This method accepts the row number as the parameter using which the record of that row number would be retrieved.
4. public Query setMaxResult(int rowsCount): This method returns a maximum up to the specified rowCount while retrieving from the database.
5. public Query setParameter(int position, Object value): This method sets the value to the attribute/column at a particular position. This method follows the JDBC style of the query parameter.
6. public Query setParameter(String name, Object value): This method sets the value to a named query parameter.
- Example: To get a list of all records from InterviewBitEmployee Table:
```
Query query=session.createQuery("from InterviewBitEmployee");  
List<InterviewBitEmployee> list=query.list();  
System.out.println(list.get(0));
```

### 21. Can you tell something about one to many associations and how can we use them in Hibernate?
- The one-to-many association is the most commonly used which indicates that one object is linked/associated with multiple objects.
- For example, one person can own multiple cars.
- In Hibernate, we can achieve this by using @OnetoMany of JPA annotations in the model classes. Consider the above example of a person having multiple cars as shown below:
```
@Entity
@Table(name="Person")
public class Person {

   //...

   @OneToMany(mappedBy="owner")
   private Set<Car> cars;

   // getters and setters
}
```
- In the Person class, we have defined the car's property to have @OneToMany association. The Car class would have owned property that is used by the mappedBy variable in the Person class. The Car class is as shown below:
```
@Entity
@Table(name="Car")
public class Car {

   // Other Properties
   
   @ManyToOne
   @JoinColumn(name="person_id", nullable=false)
   private Person owner;

   public Car() {}

   // getters and setters
}
```
@ManyToOne annotation indicates that many instances of an entity are mapped to one instance of another entity – many cars of one person.

### 22.What are Many to Many associations?
- Many-to-many association indicates that there are multiple relations between the instances of two entities.
- We could take the example of multiple students taking part in multiple courses and vice versa.
- Since both the student and course entities refer to each other by means of foreign keys, we represent this relationship technically by creating a separate table to hold these foreign keys.
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/053/original/Hibernate_Many_To_Many_Associations.png" width="500">
Here, Student-Course Table is called the Join Table where the student_id and course_id would form the composite primary key.

### 23. What does session.lock() method in hibernate do?
- session.lock() method is used to reattach a detached object to the session.
- session.lock() method does not check for any data synchronization between the database and the object in the persistence context and hence this reattachment might lead to loss of data synchronization.

### 24. What is hibernate caching?
- Hibernate caching is the strategy for improving the application performance by pooling objects in the cache so that the queries are executed faster.
- Hibernate caching is particularly useful when fetching the same data that is executed multiple times.
- Rather than hitting the database, we can just access the data from the cache.
- This results in reduced throughput time of the application.
- Types of Hibernate Caching
1. First Level Cache:
a. This level is enabled by default.
b. The first level cache resides in the hibernate session object.
c. Since it belongs to the session object, the scope of the data stored here will not be available to the entire application as an application can make use of multiple session objects.
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/051/original/Hibernate_First_Level_Caching.png" width="500">
2. Second Level Cache:
a. Second level cache resides in the SessionFactory object and due to this, the data is accessible by the entire application.
b. This is not available by default. It has to be enabled explicitly.
c. EH (Easy Hibernate) Cache, Swarm Cache, OS Cache, JBoss Cache are some example cache providers.
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/052/original/Hibernate_Second_Level_Caching.png?1614765951" width="500">

### 25. When is merge() method of the hibernate session useful?
- Merge() method can be used for updating existing values.
- The specialty of this method is, once the existing values are updated, the method creates a copy from the entity object and returns it.
- This result object goes into the persistent context and is then tracked for any changes. The object that was initially used is not tracked.

### 26. Collection mapping can be done using One-to-One and Many-to-One Associations. What do you think?
- False, collection mapping is possible only with One-to-Many and Many-to-Many associations.

### 27. Can you tell the difference between setMaxResults() and setFetchSize() of Query?
1.setMaxResults() the function works similar to LIMIT in SQL.
- Here, we set the maximum number of rows that we want to be returned.
- This method is implemented by all database drivers.
2. setFetchSize() works for optimizing how Hibernate sends the result to the caller for example: are the results buffered, are they sent in different size chunks, etc.
- This method is not implemented by all the database drivers.

### 28. Does Hibernate support Native SQL Queries?
- Yes, it does. Hibernate provides the createSQLQuery() method to let a developer call the native SQL statement directly and returns a Query object.
- Consider the example where you want to get employee data with the full name “Hibernate”.
- We don’t want to use HQL-based features, instead, we want to write our own SQL queries. In this case, the code would be:
```
Query query = session.createSQLQuery( "select * from interviewbit_employee ibe where ibe.fullName = :fullName")
                   .addEntity(InterviewBitEmployee.class)
                   .setParameter("fullName", "Hibernate"); //named parameters
List result = query.list();
```
Alternatively, native queries can also be supported when using NamedQueries.

### 29. What happens when the no-args constructor is absent in the Entity bean?
- Hibernate framework internally uses Reflection API for creating entity bean instances when get() or load() methods are called.
- The method Class.newInstance() is used which requires a no-args constructor to be present.
- When we don't have this constructor in the entity beans, then hibernate fails to instantiate the bean and hence it throws HibernateException.

### 30. Can we declare the Entity class final?
- No, we should not define the entity class final because hibernate uses proxy classes and objects for lazy loading of data and hits the database only when it is absolutely needed. This is achieved by extending the entity bean.
- If the entity class (or bean) is made final, then it cant be extended and hence lazy loading can not be supported.

### 31.What are the states of a persistent entity?
A persistent entity can exist in any of the following states:
1. Transient:
- This state is the initial state of any entity object.
- Once the instance of the entity class is created, then the object is said to have entered a transient state. These objects exist in heap memory.
- In this state, the object is not linked to any session. Hence, it is not related to any database due to which any changes in the data object don't affect the data in the database.
```
InterviewBitEmployee employee=new InterviewBitEmployee(); //The object is in the transient state.  
   employee.setId(101);  
   employee.setFullName("Hibernate"); 
   employee.setEmail("hibernate@interviewbit.com");
```
2. Persistent:
- This state is entered whenever the object is linked or associated with the session.
- An object is said to be in a persistence state whenever we save or persist an object in the database.
- Each object corresponds to the row in the database table.
- Any modifications to the data in this state cause changes in the record in the database.
- Following methods can be used upon the persistence object:
```
session.save(record);  
session.persist(record);  
session.update(record);  
session.saveOrUpdate(record);  
session.lock(record);  
session.merge(record);
```
3. Detached:
- The object enters this state whenever the session is closed or the cache is cleared.
- Due to the object being no longer part of the session, any changes in the object will not reflect in the corresponding row of the database. However, it would still have its representation in the database.
- In case the developer wants to persist changes of this object, it has to be reattached to the hibernate session.
- In order to achieve the reattachment, we can use the methods load(), merge(), refresh(), update(), or save() methods on a new session by using the reference of the detached object.
- The object enters this state whenever any of the following methods are called:
```
session.close();
session.clear();
session.detach(record);
session.evict(record);
```
<img src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/054/original/Hibernate_Persistent_Entity.png" width="500">
