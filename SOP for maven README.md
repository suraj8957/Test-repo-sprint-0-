# Standard Operating Procedure (SOP's) for Maven

---

## Table of Contents

1. [Purpose](#1-Purpose)

2. [Scope](#2.Scope)

3. [Pre-requisites](#3-Pre-requisites)

4. [Overview of Apache Maven](#4-Overview of Apache Maven)

5. [Commonly Used Maven Commands](#5-Commonly Used Maven Commands)

   5.1 [Check Maven Version](#51-Check Maven Version)

   5.2 Clean Project

   5.3 Compile Source Code

   5.4 Run Unit Tests

   5.5 Package Application

   5.6 Install to Local Repository

   5.7 Deploy to Remote Repository

   5.8 Full Build Lifecycle

6. Dependency Management Commands

   6.1 Resolve Dependencies

   6.2 View Dependency Tree

   6.3 Analyze Dependencies

   6.4 Update Dependencies

7. Debugging and Troubleshooting Commands

   7.1 Enable Debug Logs

   7.2 Display Error Stack Traces

   7.3 Skip Tests

   7.4 Run Specific Tests

   7.5 Force Dependency Updates

   7.6 Offline Builds

8. Common Issues and Resolutions

9. Best Practices

10.Conslusion

11.Author Details


---
## 1. Purpose
The purpose of this SOP is to provide standardized guidelines for using Apache Maven to build, manage dependencies, and package Java applications. It also outlines commonly used Maven commands and debugging techniques to identify and resolve build-related issues efficiently

## 2. Scope
This SOP applies to developers, DevOps engineers, and build/release teams working with Java-based applications that use Maven for build and dependency management across development, testing, and production environments.

## 3. Pre-requisites

- Java (JDK 8, 11, or 17) installed

- JAVA_HOME configured

- Maven installed and accessible in PATH

- Basic understanding of Java projects

- Access to a Maven project (pom.xml)

---

## 4. Overview of Apache Maven

Apache Maven is a build automation and dependency management tool primarily used for Java-based applications. It provides a standardized and declarative approach to building, testing, packaging, and deploying software projects. Maven uses a centralized configuration model called the Project Object Model (POM), defined in a pom.xml file, to describe the project structure, dependencies, plugins, and build behavior.

Maven follows a convention-over-configuration philosophy, which reduces the need for custom build scripts by enforcing standard project layouts and default build lifecycles. It defines three core build lifecycles—clean, default, and site—each composed of well-defined phases such as compile, test, package, install, and deploy. Executing a phase automatically triggers all preceding phases in that lifecycle, ensuring consistent and repeatable builds.

A key strength of Maven is its dependency management system, which automatically resolves and downloads required libraries and their transitive dependencies from remote repositories such as Maven Central, Nexus, or Artifactory. Maven also manages plugin execution to perform tasks like compilation, testing, packaging, and reporting, allowing build logic to be modular and extensible.

In enterprise and CI/CD environments, Maven enables deterministic builds, version-controlled dependency definitions, and seamless integration with automation tools like Jenkins and GitHub Actions. By standardizing build processes and reducing manual intervention, Apache Maven plays a critical role in delivering reliable, maintainable, and scalable Java applications.

---

## 5. Commonly Used Maven Commands
### 5.1 Check Maven Version
```bash
mvn --version
```
### 5.2 Clean Project
Removes previously compiled files.
```bash
mvn clean
```
### 5.3 Compile Source Code
Compiles the source code of the project.
```bash
mvn compile
```
### 5.4 Run Unit Tests
Executes test cases.
```bash
mvn test
```
### 5.5 Package Application
Creates JAR/WAR file.
```bash
mvn package
```
### 5.6 Install to Local Repository
Installs the artifact into the local .m2 repository.
```bash
mvn install
```
### 5.7 Deploy to Remote Repository
Uploads artifact to remote repository (Nexus/Artifactory).
```bash
mvn deploy
```
### 5.8 Full Build Lifecycle
Uploads artifact to remote repository (Nexus/Artifactory).
```bash
mvn clean install
```


---

## 6. Dependency Management Commands

### 6.1 Resolve Dependencies
Resolves and downloads all project dependencies defined in pom.xml into the local Maven repository.
```bash
mvn dependency:resolve
```
### 6.2 View Dependency Tree
Displays the complete hierarchical tree of project dependencies, including transitive dependencies.
```bash
mvn dependency:tree
```
### 6.3 Analyze Dependencies
Analyzes project dependencies to identify unused and missing dependencies in the pom.xml.
```bash
mvn dependency:analyze
```
### 6.4 Update Dependencies
Updates all project dependencies to their latest available release versions.
```bash
mvn versions:use-latest-releases
```

---

## 7. Debugging and Troubleshooting Commands

### 7.1 Enable Debug Logs
Shows detailed Maven execution logs.
```bash
mvn clean install -X
```
### 7.2 Display Error Stack Traces
Displays only error stack traces.
```bash
mvn clean install -e
```
### 7.3 Skip Tests
Builds the project while skipping test execution to speed up the build process
```bash
mvn clean install -DskipTests
```
### 7.4 Run Specific Tests
Runs only the specified test class instead of executing all tests.
```bash
mvn -Dtest=TestClassName test
```
### 7.5 Force Dependency Updates
Forces Maven to update snapshots and re-download dependencies from remote repositories before building the project.
```bash
mvn clean install -U
```
### 7.6 Offline Builds
Builds the project in offline mode using only locally cached dependencies, without accessing remote repositories.
```bash
mvn clean install -o
```

---

## 8. Common Issues and Resolutions
| Issue                      | Possible Cause                | Resolution                                    |
|----------------------------|-------------------------------|-----------------------------------------------|
| mvn: command not found     | Maven is not installed or not added to the system PATH | Add the Maven bin directory to the PATH environment variable   |
| Dependency download failure        | Network issues or repository access problems     | mvn clean install -U   |
| Build fails due to test failures   | Unit or integration tests are failing    | mvn clean install -DskipTests   |
| Dependency version conflicts      | Conflicting transitive dependencies   | mvn dependency:tree        |

## 9. Best Practices
- Use LTS Java versions (JDK 8, 11, or 17) and keep Java/Maven versions consistent across environments

- Always define explicit dependency and plugin versions in pom.xml

- Avoid using LATEST or RELEASE versions in production

- Run clean builds for releases:
```bash
   mvn clean install
```
- Use dependency:tree and dependency:analyze to avoid conflicts and unused dependencies

- Do not skip tests in production builds; use -DskipTests only for local or temporary builds

- Use centralized repositories like Nexus or Artifactory for dependency management

- Enable debug (-X) or stack trace (-e) options only when troubleshooting

## Conslusion
This SOP provides standardized guidance for using Apache Maven to build, test, and manage Java applications efficiently. By following the defined commands, dependency management practices, and best practices, teams can achieve consistent, reliable, and repeatable builds across all environments. Adhering to this SOP helps reduce build failures, improve CI/CD stability, and ensure production-ready artifacts.

## 11. Author Details
| Name             | Role            | Team                 | Contact Type | Details |  
|------------------|-----------------|----------------------|--------------|---------|
| Suraj Tripathi   | Devops Trainee  |  Saarthi             |Email         |[surajtripathi167@gmail.com](mailto:surajtripathi167@gmail.com)

