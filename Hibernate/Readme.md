### 1. What is ORM in Hibernate?
- Hibernate ORM stands for Object Relational Mapping.
- This is a mapping tool pattern mainly used for converting data stored in a relational database to an object used in object-oriented programming constructs.
- This tool also helps greatly in simplifying data retrieval, creation, and manipulation.
![alt text](https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/042/original/Object_Relational_Mapping.png?1614751673)

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
![alt text](https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/043/original/Hibernate%E2%80%99s_Inheritance_Mapping.png?1614752403)

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

![alt text](https://s3.ap-south-1.amazonaws.com/myinterviewtra…48/original/Hibernate_Architecture.png?1614765415)

### 16.
