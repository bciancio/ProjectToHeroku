
*Important:* I'm doing this on windows, some things might be different on mac.

# How to:
###### Heroku requires the following:
* a Heroku account (which is free)
* Java 8 installed
* A Maven project

###### Setting up a heroku account if you dont have one:
  1. Sign-up [here](https://signup.heroku.com/dc)
  
###### If your project is not built on a Maven framework: 

1. [IntelliJ - Convert a Java project/module into a Maven project/module](http://stackoverflow.com/questions/7642456/intellij-convert-a-java-project-module-into-a-maven-project-module)
  
  This step will add the Maven framework to your project.
  When the framework is added a  pom.xml file is created.
  The pom.xml file is where you need to setup dependencies.
  You can generate them all/most of them with intelliJ.

2.  At this point everything should be broken ;) Lets start by adding maven dependencies

  You could try to [Generate pom.xml dependencies -       Intellij](https://www.jetbrains.com/idea/help/generating-maven-dependencies.html). However I was unable to get this to work.
  
  1. Navigate to the pom.xml file
  2. I only needed to add hibernate/jersey/mySql (thus far) to my project dependencies so in my pom.xml file I added:

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

        <!-- This is what I added to add mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.36</version>
        </dependency>
        
    </dependencies>
  ```

  [*A GREAT RESOURCE*](http://mvnrepository.com/search?q=SEARCH+WHAT+YOU+WANT+HERE) for knowing what the <dependency>looks     like.
  
  3. It is also important to specify your build in the pom.xml (before the dependencies):
  ```xml
  
    <!-- This is the language level /  -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.7</source> <!-- Langauge Level -->
                    <target>1.7</target> <!-- Langauge Level -->
                </configuration>
            </plugin>
        </plugins>
    </build>

  
  
  ```
  3. When I added these in the top right some message came up saying 'maven needs something' I  hit 'enable auto something'.
    * Basically every time a dependency is added it adds it to your project. IT TAKES A BIT when you add a dependency for it       your project to re-index.
    
3. Check to see if *we broke the project* (run main method) - This step might be repeated if errors match/similiar
  * ```Error:(73, 49) java: diamond operator is not supported in -source 1.5(use -source 7 or     higher to enable diamond operator)``` [Source4Below](https://madjavaenterprise2015.slack.com/files/mcalabro/F0EBBAJJH/screen_shot_2015-11-11_at_5.58.52_pm.png)

    1. Navigate: Project Structure > Modules > 
    2. Under the language level change it to 7.
    
  * ```Error:java: javacTask: source release 1.7 requires target release 1.7```  [Source4Below](http://stackoverflow.com/questions/12900373/idea-javac-source-release-1-7-requires-target-release-1-7)
 
    1. Navigate: Settings > Build,Execution,Deployment > Java Compiler
    2. Under the "Per-module bytecode version" Change your modules target bytecode version to the one that maches your error.        (the error above required a bytecode version of 1.7.

  * ```hibernate.cfg.xml not found```
  
    1. When you added the maven framework to your project it generated a Resources folder Navigate to it.
    2. Drag in your hibernate / all your table config files to this new folder.


4. Why are my files 'brown' color?

  1. Right click your module > git > add directory
  2. This will add all the files/structure to git. Now you can commit easy peasy.
  
  * Sources
    *  [Intelij File Colors](https://www.jetbrains.com/idea/help/file-status-highlights.html)
    *  [Why do we have brown files!?](http://stackoverflow.com/questions/21341683/intellij-idea-red-brown-highlighted-file-na     me)

5. If all functionality works as expected than continue.

###### Installing the Heroku toolbelt:
  
  1.  Download [here](https://devcenter.heroku.com/articles/getting-started-with-java#set-up). Most steps from here on out     will be my experience with following the getting started with java heroku tutorial (in that link)
  2.  Follow install wizard. I choose full install.

###### Loging In / Creating a heroku app / Pushing to app
  1. In command prompt I did:
    ![cmdPromtScreenie](http://oi68.tinypic.com/2r4sd1s.jpg)

  2. Now you need to push to that heroku app you created 
  3. Type: ```cmd git push heroku master``` in cmd
