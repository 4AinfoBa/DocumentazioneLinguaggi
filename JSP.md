# JSP
## Index

1. [Set-up](##Set-up)
	- [Creating-a-JSP-project](###Creating-a-JSP-project)
	- [Running-the-application](###Running-the-application)
2. [Syntax](##Syntax)
	- [Control_statements_dependent_rendering](###Control_statements_dependent_rendering)
	- [Session](###Session)
3. [Databases_integration](##Database_integration)
4. [Spice-it-up](##Spice-it-up)


## Set-up
### Creating-a-JSP-project

In this tutorial i'll be using intelliJ as it is the most stright forward experience for java development, said so, you'll need to create a new project, using the webapp maven archetype (new > project > maven archetypes and then write this in archetypes `org.apache.maven.archetypes:maven-archetype-webapp`)

### Running-the-application

#### Configuration on intelliJ

If you can't run the project out of the box, you'll need to go to the top bar and click on the burger menu, then go under the section "Run" and click on "Edit configurations", in the menu that appeared, click on the "+" (in the top left corner) and scroll until you find "tomcat server" and select "local". 

Now you need to configure tomcat itself, by clicking on "configure" near "Application server", here, under the voice "Application home", you'll need to select the directory where tomcat is installed, search on the internet to find it if you don't know (if you are on linux try to use the command `which` or your package manager to find where the package is installed).

If you correctly found tomcat, now make sure that the HTTPS port is not set, and that the HTTP is.

Set the "On 'Update' action" and "On frame deactivation" options to "Update classes and resources" to be able to check changes, by only refreshing the webpage on your browser.

Then go to "Deployment" that is next to "Server", and check if there is something, if you don't find anything, click on "+", then on "artifact" and then on the one with "exloded" in the name. If you don't find anything or you can't click the "+", then click on the pencil. In the new menu click the "+", and select "Web Application: Exploded" > "From module", and you should be ready. 

>[!note]
>I'd advice to not disable the "open browser" after launch option  

### Static-files

Create a "resources" directory inside the "webapp" directory, and put all the Images, CSS and JS files inside that "resources" directory.
Then just normaly reference the files inside your JSP pages.


## Syntax

In a **JSP** page you can write **Java** code by wrapping the code like this:
```jsp
<% /*your code*/ %>
```

If we need to print the content of a variable to the html page we can use:
``` jsp
<%= Var %>
```

Everything outside of the special brackets ( <\% \%> ) will be considered as HTML
### Control_statements_dependent_rendering

With **Control statements** we mean all of the instructions that can change the flow of the code (if, switch, for, while, break, continue ... ).

We may want to render something for a certain amount of times, or only if a certain condition is met.

The best method (as you get HTML syntax highlighting):

```jsp
	<% 
	if(condition)
	{
	%>
	<!-- HTML to render if true -->
	<%
	} else {
	%>
	<!-- HTML to render if false -->
	<% } %>
```

This can be done with every other **control statement**. To make it easy, imagine that everything outside of the special brackets it's just a big string that needs to be printed before that other special brackets begin. Like this:
```jsp
<% 
	if(condition)
	{
	%>
	print(<!-- HTML to render if true -->)
	<%
	} else {
	%>
	print(<!-- HTML to render if false -->)
<% } %>
```
but those print are still inside the curly brackets ( "{}" ) of the **control statement** used, so they still get influenced by it.	


You could also just use this other method:
```jsp
<% 
	if(condition)
	{
		out.write("<!-- HTML to render if false -->");
	} else {
		out.write("<!-- HTML to render if false -->");
	}
%>
```
This can be more intuitive, but it is worse for complex html layouts.

### Session

When storing session data you'll create a cookie on the client, this cookie contains only the **session id**, that is used to retrieve the data stored in the server.

you can save data inside the session by using this function
```java
session.setAtribute("var",var);
```

then you can retrieve it using:
```java
session.getAtrribute("var")
```


## Database_integration

to connect a DB you'll need to add the drivers of your DBMS as a dependency in your `pom.xml`.
For ==MySQL==:
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```
For ==mariaDB== :
```xml
<dependency>
    <groupId>org.mariadb.jdbc</groupId>
    <artifactId>mariadb-java-client</artifactId>
    <version>3.5.2</version>
</dependency>
```

To activate a connection you'll need something like this:
```java
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.SQLException;  
import java.sql.*;

/*  your code */

public Connection connect() {  
		/*for mariaDB "org.mariadb.jdbc.Driver"*/ 
		String Driver = "com.mysql.jdbc.Driver" 
		/*for mariaDB "jdbc:mariadb://localhost:3306/Your_DB" */
		String URL = "jdbc:mysql://localhost:3306/Your_DB";  
		String USER = "utente_del_db";  
		String PASSWORD = "password_del_DB";
		
        try {  
            Class.forName(driver);  
        } catch (ClassNotFoundException e) {  
            e.printStackTrace();  
        }  
        try {  
            this.connection = DriverManager.getConnection(URL, USER, PASSWORD);  
        } catch (Exception e){  
            e.printStackTrace();  
        }  
}
```

This code should be in a class that you import in your JSP file like this:
```jsp
<%@ page import="your_package.your_class" %>
```

### How_to_query

to make queries we will need to use this code (put this in the class used to create teh connection):
```java
public ResultSet executeQuery(String query){  
    try{  
        return connection.prepareStatement(query).executeQuery();  
    }catch(SQLException e){  
        e.printStackTrace();  
        return null;  
    }  
}
```

this function it's the bare minimum for executing queries, you pass the full query to it and it returns a ResultSet variable with all the results.

> [!warning]
> this is not safe, it's vulnerable to SQL injection.
> later we will see how to sanitize strings

To use this in our JSP we also need to import this:
```
<%@ page import="java.sql.ResultSet" %>
```
## Spice-it-up

In this chapter we will go over some thing that will help us upgrade our webpages.

### Tailwind-Css

> if you want to learn it see [Tailwind CSS website](https://tailwindcss.com/) ([Documentation](Tailwind-CSS.md) is still WIP) 

To include Tailwind in our project we have two ways:
- [Include tailwind javascript in our pages](Tailwind-CSS.md###Link-in-your-HTML)
- Compile our TailwindCSS in our project

The latter is the clean way to do things, as it only compiles used css files, and let's us test even if we are offline once we have it set up correctly.

Follow these steps [( click here if the section after isn't displayed properly)](Tailwind-CSS.md###Tailwind-Cli):
![[Tailwind-CSS.md###Tailwind-Cli]]

and use `./src/main/webapp/resources/output.css` as your output.

