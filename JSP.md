# JSP

## Index

1. [Set-up](##Set-up)
	- [Creating-a-JSP-project](###Creating-a-JSP-project)
	- [Running-the-application](###Running-the-application)
 2. [Spice-it-up](##Spice-it-up)


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

