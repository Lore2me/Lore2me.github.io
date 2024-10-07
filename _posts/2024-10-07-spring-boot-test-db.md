---
layout: post
title: Spring Boot Test DB
date: 2024-10-07 11:25 +0200
categories: [Coding, Spring Boot, Database, Testing]
tags: [H2, Database, Spring Boot, JUnit]
description: "Spring Boot Test DB"
---
# Spring Boot Test DB
If you have a Spring Application that uses a database, you might want to test it. You can use an in-memory database for testing purposes. In this post, I will show you how to use an H2 database for testing your Spring Boot application.

## H2 Database
The H2 (Hypersonic 2) database is an in-memory, lightweight, and open-source database commonly used for development and testing purposes. H2 is a relational database management system (RDBMS) with multiple benefits that operate in memory. Its lightweight design assures that it won’t add more complexity to your application, which is one of its biggest benefits. H2 is also quite effective, enabling your application to process data fast and efficiently.

So again, H2 is an in-memory database which key features are:
- It is easy to set up and use.
- It is lightweight and fast.
- It is open-source.
- It is reliable and efficient.
- It is compatible with most SQL databases.
- It is written in Java.
- It supports SQL and JDBC API.
- It is easy to integrate with Spring Boot.

Overall, H2 is a good choice for testing and development purposes.

Side note: H2 is developed by Thomas Mueller, a swiss softwareegnieer and is available under the Eclipse Public License.

## Implementation in Spring Boot

You can use H2 in your Spring Boot application by adding the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>test</scope>
</dependency>
```

After adding the dependency, you can configure the H2 database in the application.properties file. But I recommend creating a separate application.properties file for testing purposes. You can do this by creating a new file called `application-test.properties` in the `src/test/resources` directory. In this file, you can configure the H2 database as follows:

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

## Need data in the database?

If you need to insert data into the database before running your tests, you can use the `data.sql` file. This file should be placed in the `src/test/resources` directory. The data in this file will be inserted into the database before running the tests.

The `data.sql` file should contain the SQL statements to insert the data into the database. For example:

```sql
INSERT INTO tbl_lms_user(
 user_id, user_first_name, user_last_name, user_phone_number, user_location, user_time_zone, user_linkedin_url, user_edu_ug, user_edu_pg, user_comments, user_visa_status, creation_time, last_mod_time, user_middle_name)
 VALUES
('U01', 'John', 'Matthew', 123456789, 'New Jersey', 'EST', 'https://www.linkedin.com/in/John Matthew/', 'Computer Science Engineering', 'MBA', null, 'Not-Specified', '2021-10-04 18:09:38.076245', '2021-10-04 18:09:38.076245', null),


INSERT INTO tbl_lms_user_login(
 user_id, user_password, user_login_status, creation_time, last_mod_time, user_login_email)
 VALUES ('U01', '$2a$12$rp4D458edb501.gXGeVyhu0n.cqSIH3UXrGlZRzlUXRZFrtIsPxZO', 'ACTIVE', '2021-10-04 18:11:10.357897', '2021-10-04 18:11:10.357897', 'John.Matthew@gmail.com');

INSERT INTO tbl_lms_userrole_map(
 user_role_id, user_id, role_id, user_role_status, creation_time, last_mod_time)
 VALUES (1, 'U01', 'R01', 'Active', '2021-10-04 18:18:40.000121', '2021-10-04 18:18:40.000121');

INSERT INTO tbl_lms_program(
 program_id, program_name, program_description, program_status, creation_time, last_mod_time)
 VALUES (1, 'SDET', 'Testing batch', 'Active', '2021-10-04 18:14:48.326714', '2021-10-04 18:14:48.326714');

INSERT INTO public.tbl_lms_batch(
 batch_id, batch_name, batch_description, batch_status, batch_program_id, batch_no_of_classes, creation_time, last_mod_time)
 VALUES (1, 01, 'SDET BATCH 01', 'Active', 1, 5, '2021-10-04 18:16:02.713333', '2021-10-04 18:16:02.713333');
```
Just insert the Insert statements in the `data.sql` file, the creation of tables is taken care of by Hibernate automatically.


## Implement a Unit Test

Now that you have configured the H2 database, you can write a unit test to test your Spring Boot application.
Important to know is
that you have to set @TestPropertySource to the location of the application-test.properties file for each test class.

```java
@TestPropertySource("classpath:application-test.properties")
public class AssignmentControllerIT {

        //write the test 
}
```

## Self-Contained Example
A demonstration of a implementation by my own can be found in the software project from DEVOPS.
It's a URL-Shortener, running with Docker and a separate Docker database.
Initially developed for ENLAB (Enterprise Programming Lab) and further developed in DEVOPS (Development and Operations).

Project: [urlshortener](git@gitlab.switch.ch:hslu/edu/bachelor-computer-science/devops/24hs01/g02/g02-urlshortener.git)

# Conclusion
In this post, I showed you how to use an H2 database for testing your Spring Boot application.
H2 is an in-memory database that is lightweight, fast, and easy to use.
You can configure the H2 database in the application-test.properties file and insert data into the database
using the data.sql file.
Finally, you can write unit tests to test your Spring Boot application using the H2 database.
