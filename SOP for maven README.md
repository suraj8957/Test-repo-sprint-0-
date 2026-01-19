# Standard Operating Procedure (SOP's) for JQ

## Step by step installation guide for **JQ** on Ubuntu

---

## Table of Contents

1. Purpose

2. Scope

3. Pre-requisites

4. Overview of Apache Maven

5. Commonly Used Maven Commands

   5.1 Check Maven Version

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

10.Useful Maven Options

11.Conclusion

---
## Purpose
The purpose of this SOP is to provide standardized guidelines for using Apache Maven to build, manage dependencies, and package Java applications. It also outlines commonly used Maven commands and debugging techniques to identify and resolve build-related issues efficiently

## Scope
This SOP applies to developers, DevOps engineers, and build/release teams working with Java-based applications that use Maven for build and dependency management across development, testing, and production environments.

## Pre-requisites

- Java (JDK 8, 11, or 17) installed

- JAVA_HOME configured

- Maven installed and accessible in PATH

- Basic understanding of Java projects

- Access to a Maven project (pom.xml)

---

## Overview of Apache Maven

Apache Maven is a build automation and dependency management tool primarily used for Java-based applications. It provides a standardized and declarative approach to building, testing, packaging, and deploying software projects. Maven uses a centralized configuration model called the Project Object Model (POM), defined in a pom.xml file, to describe the project structure, dependencies, plugins, and build behavior.

Maven follows a convention-over-configuration philosophy, which reduces the need for custom build scripts by enforcing standard project layouts and default build lifecycles. It defines three core build lifecycles—clean, default, and site—each composed of well-defined phases such as compile, test, package, install, and deploy. Executing a phase automatically triggers all preceding phases in that lifecycle, ensuring consistent and repeatable builds.

A key strength of Maven is its dependency management system, which automatically resolves and downloads required libraries and their transitive dependencies from remote repositories such as Maven Central, Nexus, or Artifactory. Maven also manages plugin execution to perform tasks like compilation, testing, packaging, and reporting, allowing build logic to be modular and extensible.

In enterprise and CI/CD environments, Maven enables deterministic builds, version-controlled dependency definitions, and seamless integration with automation tools like Jenkins and GitHub Actions. By standardizing build processes and reducing manual intervention, Apache Maven plays a critical role in delivering reliable, maintainable, and scalable Java applications.

---

## System Requirement

| Requirement             | Minimum Recommendation         |
| ----------------------- | ------------------------------ |
| Processor/Instance Type | Dual-Core / t2.micro or higher |
| RAM                     | 1 GB or Higher                 |
| ROM (Disk Space)        | 5 GB or Higher                 |
| OS Required             | Linux (Ubuntu Recommended)     |

---

## Dependencies

### Run-time Dependency

| Run-time Dependency | Version            | Description                                                   |
| ------------------- | ------------------ | ------------------------------------------------------------- |
| **glibc / libc6**   | Default OS version | Core Linux C library required to execute compiled jq binaries |

➡️ Explanation:
jq is written in C, so it needs the GNU C standard library (already available in Ubuntu).
No manual installation needed — it comes pre-installed with Linux.

---

### Other Dependency

| Other Dependency | Version                  | Description                                                            |
| ---------------- | ------------------------ | ---------------------------------------------------------------------- |
| **curl / wget**  | Latest package available | Used to fetch API responses or download JSON before processing with jq |
| **bash / shell** | Default OS shell         | jq is typically used inside bash scripts and CLI pipelines             |

➡️ Explanation:

jq itself does not require extra runtime packages.
In real DevOps workflows, jq is commonly used with curl:

```bash
curl https://api.github.com/users/octocat | jq '.id'
```

---

## Installation — Ubuntu (Debian-based Systems)

### 1️⃣ Update Package Index

```bash
sudo apt-get update -y
```

<img width="955" height="588" alt="image" src="https://github.com/user-attachments/assets/1d8b69af-bc4c-4043-930b-97a0e64a1086" />

---

### 2️⃣ Install jq

```bash
sudo apt-get install jq -y
```

<img width="952" height="363" alt="image" src="https://github.com/user-attachments/assets/0605c23e-ca5e-4ef7-ab28-aca5e870abe8" />

---

### 3️⃣ Verify Installation

```bash
jq --version
```

Expected output (example):

<img width="954" height="61" alt="image" src="https://github.com/user-attachments/assets/41e749e6-96ef-4d3c-9b7d-50288c3d0d62" />

---

## Quick Usage Test

### Step 1 — Create `sample.json`

```bash
echo '{"name":"Abhinav","batch":32,"tool":"jq"}' > sample.json
```

### Step 2 — Run jq

```bash
jq '.' sample.json
```

### Pretty-print Output

```json
{
  "name": "Abhinav",
  "batch": 32,
  "tool": "jq"
}
```

<img width="877" height="166" alt="image" src="https://github.com/user-attachments/assets/4e4a26cc-fa0d-4764-8311-9ac264f7ded5" />

---

## Troubleshooting (Ubuntu)

| Issue                   | Fix                                       |     |
| ----------------------- | ----------------------------------------- | --- |
| `jq: command not found` | Reinstall using `sudo apt-get install jq` |     |
| Output unreadable       | Use pipe `                                | jq` |
| Permission denied       | Run command with `sudo`                   |     |

---

## Uninstall jq

```bash
sudo apt-get remove jq -y
```

<img width="953" height="264" alt="image" src="https://github.com/user-attachments/assets/b9b4184a-22ae-4893-a1c5-3d15033618de" />

---

## Examples

| Command            | Purpose           |                       |
| ------------------ | ----------------- | --------------------- |
| `jq '.' file.json` | Pretty print JSON |                       |
| `curl <API>        | jq '.id'`         | Extract key from API  |
| `.[]               | select(.active)`  | Filter matching items |

---

## 📌 Summary

`jq` is a lightweight yet powerful command-line utility designed for **processing JSON data efficiently**.
It is widely used in DevOps workflows involving APIs, cloud services, logs, and automation pipelines.

---

## Author

| Name             | Role            | Team                 |
| ---------------- | --------------- | -------------------- |
| Abhinav Sikarwar | DevOps Trainee | Saarthi |

---

## Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Email        | [abhinavsikarwar011@gmail.com](mailto:abhinavsikarwar011@gmail.com) |


---

## References

| Reference                 | Link                                                             |
| ------------------------- | ---------------------------------------------------------------- |
| Official jq Documentation | [https://jqlang.github.io/jq/](https://jqlang.github.io/jq/)     |
| jq GitHub Repository      | [https://github.com/jqlang/jq](https://github.com/jqlang/jq)     |
| Ubuntu jq Package         | [https://packages.ubuntu.com/jq](https://packages.ubuntu.com/jq) |
| JSON Validator            | [https://jsonlint.com](https://jsonlint.com)                     |

---
