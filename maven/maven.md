## Maven - Software Project Management

### Overview:

#### What is Maven?

* Maven is a build tool
* Dependency management tool
* Project management tool
* Standardized approach to building software
* Command line tool
* IDE integration

Maven is a build automation tool. You may be familiar with a similar tool like ant or make which compiles source code into a deliverable like a distributable library; for example:  a .jar or .war file.  Maven automates this process in a way that  emphasises convention over configuration.

Maven can manage a project's build, reporting and documentation from a central piece of information. It can build and manage any Java based project.

However the most favorite feature of maven is dependency management. Especially applications that depend on third party libraries. As a project management tool, maven can manage version numbers, who is working on the project and provides a good overview of what is being used in our project. Maven provides a standardized approach to building software. If we have 5 project we are building and maven is being used for each project, we will see a consistent approach to each project which leads to consistent and easy to understand workflow. Maven is primarily a command line interface (CLI) tool. Make sure maven is found on your computer's PATH statement. In addition, maven can be integrated in major IDE's like Eclipse or NetBeans.

#### Build tools

* Creates deployable artifacts from source code
* Automated/repeatable builds
* Deploying artifacts on servers
* IDE independence
* Integration with other build tools

Maven creates an automated build process. Steps are not missed. A new developer can easily join a software project and as long as the developer knows how to use maven, the project can be built directly from source code easily. Maven's output can be automatically stored to a specific path on a local or remote server too. Those are the main advantages of using maven as a build tool. Maven allows any developer to build a project from source code rather than using rudimentary compiler tools or a specific IDE. Maven makes your build process IDE agnostic and repeatable by anyone on your team. Maven allow has integration with other build tools like [Hudson](http://hudson-ci.org/) and [Bamboo](https://www.atlassian.com/software/bamboo).

#### Dependency management tool

* Download project dependencies from centralized repositories
* Automatically resolve the libraries required by project dependencies
* Dependency scoping

This is one of the most popular aspects of maven. Maven can connect with online repositories to download lets say a framework. This eliminates the need to manually search for and download from an online repository. If the library being downloaded has its own POM file, then we know its dependecies. Because just like our application has its own dependencies, the framework we are downloading has its own dependencies too. Maven will reach out and grab the dependencies of the dependent framework, file or whatever. Also known as transitive dependencies. Maven also allow you to specify scope of dependency in case a specific dependency is not needed or if it is conditionally included as certain points in a software development lifecycle.

#### Project management tool

* Artifact versioning
* Change Logs
* Documentatio
* Javadocs
* Reports

Every maven project has an XML based POM file which list every detail about the project like: version, list of developers, project website address, source code repositories and change logs. Maven can also automatically create software documentation during build process. It can alos create Javadocs about the code we are developing. that provides information for users of the software. Maven can also generates reports for example: [Clover Code Coverage Reports](https://confluence.atlassian.com/clover/about-code-coverage-71599496.html).

#### Standardized approach to building software

* Uniformity across projects through patterns
* Convention over configuration
* Consistent path for all projects
* Philosophy of Maven

Using maven across multiple projects creates uniformity across those projects through patterns like a standard directory structure because maven knows where to place certain files. Maven is opinionated software. It dictates the file structure of a project to achieve "convention over configuration." Which leads to conformity over a portfolio of projects. Maven adheres to compile, test and deploy phases for all projects because they appear to every life cycle of every project. Therefore maven projects look the same and have similar processes and layouts. This is the power of maven.

At one point in time, each Apache project was unique.  When a developer moved from one Apache project to another, the developer had to learn a new build system and file structure. Maven was created to solve this problem.

### References:
1. [Apache Maven Home Page](http://maven.apache.org/)
2. [Apache Maven Tutorial Video](https://www.youtube.com/playlist?list=PLtNErhYMkHnG6eH4B9UKAddirFid7plYi)
