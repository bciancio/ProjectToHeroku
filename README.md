

# How to:

###### Heroku requires the following:
* a Heroku account (which is free)
* Java 8 installed
* A Maven project

###### If your project is not built on a Maven framework: 

1. [IntelliJ - Convert a Java project/module into a Maven project/module](http://stackoverflow.com/questions/7642456/intellij-convert-a-java-project-module-into-a-maven-project-module)
  
  This step will add the Maven framework to your project.
  When the framework is added a  pom.xml file is created.
  The pom.xml file is where you need to setup dependencies.
  You can generate them all/most of them with intelliJ.

2.  At this point everything should be broken ;) Lets start by adding maven dependencies

  1. Navigate to the pom.xml file
  2. I only needed to add hibernate/jersey (thus far) to my project dependencies
  
  I added: 

  ```xml 
  
    <!-- dependencies must be enclosed in the <dependencies> tags -->
    <dependencies>

        <!-- This is what I added to add jersery -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>3.5.1-Final</version>
        </dependency>

        <!-- This is what I added to add jersery -->
        <dependency>
            <groupId>com.sun.jersey</groupId>
            <artifactId>jersey-bundle</artifactId>
            <version>1.12-b01</version>
        </dependency>

    </dependencies>
  ```

3. Check to see if we broke the project (run main method) - This step might be repeated if errors match/similiar
  * ```Error:(73, 49) java: diamond operator is not supported in -source 1.5(use -source 7 or     higher to enable diamond operator)``` [Source4Below](https://madjavaenterprise2015.slack.com/files/mcalabro/F0EBBAJJH/screen_shot_2015-11-11_at_5.58.52_pm.png)

    1. Navigate: Project Structure > Modules > 

    2. Under the language level change it to 7.
    
  * ```Error:java: javacTask: source release 1.7 requires target release 1.7```  [Source4Below](http://stackoverflow.com/questions/12900373/idea-javac-source-release-1-7-requires-target-release-1-7)
 
    1. Navigate: Settings > Build,Execution,Deployment > Java Compiler
  
    2. Under the "Per-module bytecode version" Change your modules target bytecode version to the one that maches your error.        (the error above required a bytecode version of 1.7.

    
    
  You should now be able to at least run the Maven project. It probably doesn't function like it did though!
  
  * ```hibernate.cfg.xml not found```
  
    1. When you added the maven framework to your project it generated a Resources folder Navigate to it.
    2. Drag in your hibernate / all your table config files to this new folder.


3. [Generate pom.xml dependencies - Intellij](https://www.jetbrains.com/idea/help/generating-maven-dependencies.html)
