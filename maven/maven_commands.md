## Maven Commands

1. Using command line interface (CLI), go to project root directory and run command below. Pom.xml should be located in root folder of every maven project.

```
mvn package
```

The typical invocation for building a Maven project uses a Maven life cycle phase.

Reads pom.xml for project information, dependencies and plugin goals. Dependency manager makes sure you have all needed files for build.

A few lines in pom.xml in and one command produces the deliverable in folder named "target" using a standard naming convention such as  "target/Articfact-VersionNumber."

2. Verify Maven installation

```
mvn --version
```
3. View all available options 

```
mvn -h
```