# SOP: Apache Maven `pom.xml`
## Step-by-Step Installation & Usage Guide

This document is a **Standard Operating Procedure (SOP)** explaining how to **install Maven**, **understand `pom.xml`**, and **use it step by step** in real projects.  .

---
## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  2026-01-16  |  1.0    |                |             |             |             |

## 1. Purpose of this SOP

This SOP is created to:
- Install Apache Maven correctly
- Understand the role of `pom.xml`
- Use `pom.xml` step by step
- Follow dependency versioning best practices
- Ensure reproducible and stable builds

---

## 2. What is `pom.xml`?

`pom.xml` (Project Object Model) is the **core configuration file** of Apache Maven.

It defines:
- Project identity
- Dependencies
- Build lifecycle
- Plugins
- Versioning strategy

Without `pom.xml`, Maven **cannot build a project**.

---

## 3. Prerequisites

Before using `pom.xml`, ensure:

| Requirement | Command |
|-----------|--------|
| Java installed | `java -version` |
| Java version | Java 8+ |
| OS | Linux / macOS / Windows |

---

## 4. Step-by-Step Maven Installation

### Step 4.1: Install Java (Ubuntu)

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```

---

### Step 4.2: Install Maven (Ubuntu)

```bash
sudo apt install maven -y
mvn -version
```

Expected output should show:
- Maven version
- Java version
- OS details

---

## 5. Create a Maven Project

### Step 5.1: Generate Project Structure

```bash
mvn archetype:generate
```

Select default options or provide:
- groupId
- artifactId
- version

---

### Step 5.2: Maven Standard Directory Structure

```
project-name/
├── pom.xml
└── src/
    ├── main/java
    └── test/java
```

Maven **expects this structure**.

---

## 6. Understanding Basic `pom.xml`

```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.company</groupId>
  <artifactId>demo-app</artifactId>
  <version>1.0.0</version>
  <packaging>jar</packaging>
</project>
```

### Explanation:
| Tag | Description |
|----|------------|
| modelVersion | Maven model version |
| groupId | Organization name |
| artifactId | Project name |
| version | Project version |
| packaging | Output type |

---

## 7. Adding Dependencies

### Step 7.1: Add Dependency Block

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.2.1</version>
  </dependency>
</dependencies>
```

### What Happens:
- Maven downloads dependency
- Transitive dependencies are resolved
- Stored in `.m2` directory

---

## 8. Dependency Versioning SOP (Best Practices)

### Rule 1: Never Use Dynamic Versions

❌ Avoid:
```xml
<version>LATEST</version>
```

✅ Use:
```xml
<version>1.2.3</version>
```

---

### Rule 2: Follow Semantic Versioning

```
MAJOR.MINOR.PATCH
```

| Change Type | Example |
|------------|--------|
| Breaking | 2.0.0 |
| Feature | 1.1.0 |
| Bug fix | 1.0.1 |

---

### Rule 3: Use Properties for Versions

```xml
<properties>
  <java.version>17</java.version>
  <junit.version>5.9.2</junit.version>
</properties>
```

Usage:
```xml
<version>${junit.version}</version>
```

---

### Rule 4: Use dependencyManagement (Parent POM)

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

Child POMs **must not define versions**.

---

### Rule 5: Use BOM (Bill of Materials)

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

Ensures **compatible versions**.

---

## 9. Build & Test Using Maven

### Compile
```bash
mvn compile
```

### Run Tests
```bash
mvn test
```

### Package Application
```bash
mvn clean package
```

Output will be inside:
```
target/
```

---

## 10. Plugin Versioning SOP

Always define plugin versions.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.11.0</version>
</plugin>
```

Avoid relying on default versions.

---

## 11. Common Issues & Fixes

| Issue | Fix |
|-----|----|
| Dependency conflict | Use dependencyManagement |
| Build differs in CI | Lock versions |
| Plugin failure | Define plugin version |
| Class not found | Run `mvn dependency:tree` |

---

## 12. Best Practices Checklist

- [ ] Java version fixed
- [ ] Dependency versions locked
- [ ] No LATEST or ranges
- [ ] Plugins versioned
- [ ] Parent POM used
- [ ] Clean directory structure

---

## 13. Conclusion

This SOP ensures:
- Consistent builds
- Secure dependency handling
- CI/CD compatibility
- Enterprise-ready Maven projects

---

## References
- https://maven.apache.org/pom.html
- https://maven.apache.org/guides/
