# SpringBoot
## Index

[Before-you-start](##Before-you-start)
- [key-concepts](###key-concepts)
	- [RESTful-APIs](####RESTful-APIs)
	- [Notations](####Notations)
	
[Bases](##Bases)
- [Installation](###Installation)
- [Creating-a-new-project](###Creating-a-new-project)
- [Starting-a-web-server](###Starting-a-web-server)

[Databases](##Databases)
- [connecting-to-mariaDB](###connecting-to-mariaDB)
- [Making-entities](###Making-entities)


## Before-you-start

If this is your first backend framework, let's go over some fundamentals and best practices to follow to write good code.
### key-concepts

#### RESTful-APIs

Nowadays the "trend" of backend programming are [REStful APIs](https://www.redhat.com/en/topics/api/what-is-a-rest-api) i won't be going into details (for that read the linked article ), but we want to follow it's constrains, especially the **Stateless** constrain, which dictates that each request should not retain any data of the previous request. We will also follow the **Uniform interface** constrain, meaning that we are gonna send all the data in the same format.
#### Notations

sometimes in your code you'll find some lines that have something similar to a comment, like:

```java
 @GeneratedValue(strategy=GenerationType.AUTO) 
```

those are notations, and are things that can define special things in your code, for example in backend frameworks are used especially to define to want function a route is associated, or of what type a certain value will be in the database.
that helps the "Runner" infer some more thing that it should do, other than the code you wrote
>[!TLDR]
> they are special thing that helps the "Runner" infer some more thing that it should do, other than the code you wrote

## Bases
### Installation

To install SpringBoot on linux you need to first install maven ( or Gradle ), then download the tar. Then extract it using:

```bash
tar -xzvf spring-boot-cli-3.3.4-bin.tar.gz -C ~/<Destination>
```

then add this line to your .zshrc or -bashrc file:

```sh
export PATH=$PATH:/home/<Username>/<springDirectory>/bin
```

### Creating-a-new-project

to create a new project use this command
```bash
spring init --build=maven -d -n <projectName> <projectDir>/
```

### Starting-a-web-server

to start a web server you'll need to have this dependencies in your `pom.xml` :

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

after that you'll be able to run your application using:
```
mvn spring-boot:run
```

## Databases

### connecting-to-mariaDB

![[MariaDB#Bases]]

you'll need to add these dependencies to your `pom.xml`:

```xml
<dependency>  
    <groupId>org.mariadb.jdbc</groupId>  
    <artifactId>mariadb-java-client</artifactId>  
</dependency>  

<dependency>  
    <groupId>jakarta.persistence</groupId>  
    <artifactId>jakarta.persistence-api</artifactId>  
</dependency>  

<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>
```

Then in your `application.properties` **add** these strings:

```css
spring.datasource.url = jdbc:mariadb://localhost:3306/<DBName> 
spring.datasource.username = <DatabaseUser>  
spring.datasource.password = <DatabasePassword> 
spring.datasource.driver-class-name = org.mariadb.jdbc.Driver  
spring.jpa.hibernate.ddl-auto = update  
spring.jpa.database-platform = org.hibernate.dialect.MariaDBDialect
```


### Making-entities

to make an entity, just make a class resembling your desired table, meaning that a column in the db, will be mapped to a propriety of the object.

for example: 
```java

import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;  
import jakarta.persistence.GenerationType;

@Entity

public class Student {  
  
    @Id  
    @GeneratedValue(strategy=GenerationType.AUTO)  
    private Integer id;
}
```

It's up to you to make the rest of the logic in the class. But we are not finished, we may want to impose some costrains to some field. For example if we want to impose that some field must not be blank we can make something like this:

```java
import jakarta.validation.constraints.NotBlank;

//rest of the code


@NotBlank(message = "First name is required")  
private String name;

```

We may be finished with the class itself, but we need to add other things to make it work correctly, we need a repository: a tool to make operation on the whole table (like making queries to find a specific object). This will be our repository:

``` java

import com.example.demo.Entity.Student;  //change it accordingly to your dir structure

import org.springframework.data.jpa.repository.JpaRepository;  
  
public interface StudentRepository extends JpaRepository<Student, Integer>{  
    boolean existsByEmail(String email);  
}

```

>[!note]
>Remember to keep all the components of your code organized, you may want to create a directory for each type of component (controllers, entities, repositories and services), or for each object (all Student related components in one place and so on).

