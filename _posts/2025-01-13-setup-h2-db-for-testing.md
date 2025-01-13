---
layout: post
title: Setup H2 DB for Testing
date: 2025-01-13 15:40 +0100
categories: [Testing]
tags: [h2, database, testing]
description: How to setup an H2 database only for testing purposes.
---
# Setup H2 DB for Testing
This guide will show you how to set up an H2 database for testing your Spring Boot application.
Sometimes you need a database for testing purposes.
You can use an in-memory database like H2 for this.
In this post, I will show you how to set up an H2 database for testing your application.  

*Sidenote: If your DB runs on docker, you can use a test container to spin up a new container for testing. Check out [Testcontainers](https://www.testcontainers.org/).*
## H2 Database
H2 Database is an in-memory, lightweight, and open-source database commonly used for development and testing purposes.
H2 is a relational database management system (RDBMS) with multiple benefits that operate in memory.
Its lightweight design assures that it won’t add more complexity to your application,
which is one of its biggest benefits.
H2 is also quite effective, enabling your application to process data fast and efficiently.
It is developed by Thomas Mueller, a Swiss software engineer, and is available under the Eclipse Public License.

H2 is an in-memory database which key features are:
- It is easy to set up and use.
- It is lightweight, fast and open-source.
- It is reliable and efficient.
- It is compatible with most SQL databases and supports SQL and JDBC API.
- It is written in Java.

Overall, H2 is a good choice for testing and development purposes, but not recommended for production.

# Step by Step
## 1. Add the H2 dependency to your `pom.xml` file:
```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>test</scope>
</dependency>
```
Please note that the scope is set to `test` to ensure that the H2 database is only used for testing purposes.

## 2. Create a separate `application-test.properties` file in the `src/test/resources` directory.

Add the following configuration to the `application-test.properties` file:
```properties
spring.datasource.url=jdbc:h2:mem:public
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
jpa.hibernate.ddl-auto=create
spring.jpa.show-sql=true
spring.jpa.defer-datasource-initialization=true
spring.sql.init.mode=always
```
- spring.data.url is the JDBC URL for the H2 database.
- spring.datasource.driverClassName is the driver class name for the H2 database.
- spring.datasource.username and spring.datasource.password are the credentials for the H2 database.  
*Change the `spring.datasource.username` and `spring.datasource.password` to your desired values.
To be said, that these credentials are not security relevant,
because the database is in-memory and only used for testing.
Also, the DB is created and destroyed with each test run.*  
- spring.jpa.database-platform is the Hibernate dialect for the H2 database.
- jpa.hibernate.ddl-auto=create will create the database schema automatically.
- spring.jpa.show-sql=true will show the SQL queries in the console.
- spring.jpa.defer-datasource-initialization=true will defer the initialization of the datasource.
- spring.sql.init.mode=always will ensure that the database is initialized before running the tests.

## 3. If you need to insert data into the database before running your tests, you can use the `data.sql` file.
This file should be placed in the `src/test/resources` directory.
   The data in this file will be inserted into the database before running the tests.

Example `data.sql` file:
```sql
INSERT INTO users (id, name, email) VALUES (1, 'Alice', 'Doe');
INSERT INTO users (id, name, email) VALUES (2, 'Bob', 'Doe');
```

## 4. Set Testproperties in your test class:
That your tests use the `application-test.properties` file, you need to set the `@TestPropertySource` annotation in your test class.

```java
@SpringBootTest
@TestPropertySource(locations = "classpath:application-test.properties")
class YourTestClass {
    // your test code
}
```

That's it! You have successfully set up an H2 database for testing your Spring Boot application.
