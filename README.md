

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

2. Check to see if we broke the project (run main method)
  * If you get something like this  ```Error:(73, 49) java: diamond operator is not supported in -source 1.5(use -source 7 or     higher to enable diamond operator)```

    1. Navigate: Project Structure > Modules > 

    2. Under the language level change it to 7.
    
  * If you get something like this ```Error:java: javacTask: source release 1.7 requires target release 1.7``` than do the       following
 
    1. Navigate: Settings > Build,Execution,Deployment > Java Compiler
  
    2. Under the "Per-module bytecode version" Change your modules target bytecode version to the one that maches your error.        (the error above required a bytecode version of 1.7.

    [Source](http://stackoverflow.com/questions/12900373/idea-javac-source-release-1-7-requires-target-release-1-7)
    
  You should now be able to at least run the Maven project. It probably doesn't function like it did though!

3. [Generate pom.xml dependencies - Intellij](https://www.jetbrains.com/idea/help/generating-maven-dependencies.html)
