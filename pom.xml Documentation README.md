# Apache Maven `pom.xml` Documentation

## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  2026-01-16  |  1.0    |                |             |             |             |

## Overview
This document explains **what `pom.xml` is**, **why it exists**, **its real-world use cases**, and **best practices for dependency versioning** based on Apache Maven official documentation and industry standards.

---

## What is `pom.xml`?
`pom.xml` stands for **Project Object Model**.  
It is the **core configuration file** used by Apache Maven to build and manage Java-based projects.

Maven reads `pom.xml` to understand:
- Project identity
- Dependencies
- Build lifecycle
- Plugins
- Repository information

In short, `pom.xml` is the **heart of a Maven project**.

---

## Why `pom.xml` Exists

Before Maven:
- JAR files were managed manually
- Dependency conflicts were common
- Builds were not reproducible
- CI/CD integration was difficult

With `pom.xml`:
- Dependency management is automated
- Builds are consistent across environments
- Project configuration is standardized
- CI/CD pipelines become reliable

### Key Benefits
- **Declarative configuration**
- **Automatic dependency resolution**
- **Reproducible builds**
- **Convention over configuration**
- **Extensible via plugins**

---

## Core Elements of `pom.xml`

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo-app</artifactId>
  <version>1.0.0</version>
  <packaging>jar</packaging>
</project>
```

### Element Explanation
| Element | Description |
|------|------------|
| groupId | Organization or group name |
| artifactId | Project name |
| version | Project version |
| packaging | Output format (jar, war, etc.) |

---

## Use Cases of `pom.xml`

### 1. Dependency Management
Defines libraries required by the project.

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.2.1</version>
  </dependency>
</dependencies>
```

Maven automatically downloads:
- Required dependency
- Transitive dependencies

---

### 2. Build Automation
`pom.xml` defines how the project is:
- Compiled
- Tested
- Packaged
- Deployed

Example:
```bash
mvn clean package
```

---

### 3. Multi-Module Projects
Used to manage large enterprise projects.

```xml
<modules>
  <module>service-api</module>
  <module>service-core</module>
</modules>
```

Parent POM controls versions and plugins for all modules.

---

### 4. Plugin Configuration
Controls build behavior.

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.11.0</version>
    </plugin>
  </plugins>
</build>
```

---

## Dependency Versioning Best Practices

### 1. Always Use Fixed Versions
❌ Avoid:
```xml
<version>LATEST</version>
```

✅ Prefer:
```xml
<version>1.2.3</version>
```

This ensures **reproducible builds**.

---

### 2. Follow Semantic Versioning
Format:
```
MAJOR.MINOR.PATCH
```

| Version Change | Meaning |
|------|--------|
| MAJOR | Breaking changes |
| MINOR | Backward-compatible features |
| PATCH | Bug fixes |

---

### 3. Use `dependencyManagement`
Centralizes versions in parent POMs.

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>6.1.0</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```

Child POMs omit versions.

---

### 4. Use Properties for Versions
Avoid repeating version numbers.

```xml
<properties>
  <junit.version>5.9.2</junit.version>
</properties>
```

Usage:
```xml
<version>${junit.version}</version>
```

---

### 5. Use BOM (Bill of Materials)
Ensures compatible dependency versions.

Example:
```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-dependencies</artifactId>
      <version>3.2.1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

---

### 6. Control Dependency Scope

| Scope | Purpose |
|-----|--------|
| compile | Default |
| provided | Runtime provided by server |
| runtime | Runtime-only |
| test | Testing libraries |

---

## 7. Best Practices Summary
- Lock dependency versions
- Use `dependencyManagement`
- Avoid `LATEST` and version ranges
- Prefer BOMs
- Use semantic versioning
- Always define plugin versions

---

## 8. Conclusion
`pom.xml` is a **central, declarative configuration file** that enables Maven to:
- Manage dependencies
- Automate builds
- Ensure consistency
- Support CI/CD pipelines

Correct dependency versioning is critical to maintain **stable, secure, and reproducible builds**.

---

## 9. References
- Apache Maven Official Documentation  
  https://maven.apache.org/pom.html
