# Documentation: Shared Library

---

## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  21-01-2026  |  1.0    |                |             |             |             |

---

## Table of Content

1. [What is a Shared Library?](#1-what-is-a-shared-library)
2. [Why Shared Library?](2#why-shared-library-?)
3. [Shared Library Structure](#3-shared-library-structure)
4. [Understanding vars](#4-understanding-vars)
5. [Understanding src](#5-understanding-src)
6. [Shared Library Workflow](#6-shared-library-workflow)
7. [Advantages](#7-advantages)
8. [Disadvantages](#8-disadvantages)
9. [Best Practices](#9-best-practices)
10. [Conclusion](#10-conclusion)
11. [Contact Information](#11-contact-information)
12. [References](#12-references)

---

## 1. What is a Shared Library ?

A Shared Library is a centralized place where common and reusable code is stored so that it can be used by multiple projects or automation workflows.

Instead of writing the same logic again and again, teams write it once in a shared library and reuse it everywhere.
This saves time, reduces errors, and keeps automation consistent.

---

## 2. Why Shared Library ?

### Without a shared library:

- Same code is copied into many places

- Fixing a bug requires multiple updates

- Different teams follow different practices

- Maintenance becomes difficult

### With a shared library:

- Common logic exists in one place

- Changes are applied once and used everywhere

- All teams follow the same standards

- Automation becomes clean and reliable

Shared libraries help organizations scale automation safely.

---

## 3. Shared Library Structure

A shared library follows a simple and organized structure:
```bash
shared-library/
├── vars/
│   ├── build.groovy
│   ├── test.groovy
│   └── deploy.groovy
├── src/
│   └── com/
│       └── company/
│           └── utils/
│               ├── BuildUtils.groovy
│               └── DeployUtils.groovy
├── resources/
│   └── templates/
│       └── config.yaml
└── README.md
```

---

## 4. Understanding vars

### What is vars?

- vars contains simple and reusable steps

- Each file represents a callable function

- Used to define what action should happen

- Easy to read and easy to use

---

### Purpose of vars

- Provide a clean entry point

- Keep automation scripts simple

- Orchestrate the overall flow

#### Example:
```bash
def call() {
    println "Build process started"
}
```
### When to Use vars

- For high-level steps

- For reusable workflow actions

- For logic that users will directly call

---

## 5. Understanding src
### What is src?
- src contains internal implementation logic

- Used for complex processing

- Follows a structured package format

- Not directly called by users

### Purpose of src

- Handle complex logic

- Improve code organization

- Allow reuse across multiple vars files

#### Example:
```bash
class BuildUtils {
    static void runBuild() {
        println "Running internal build logic"
    }
}
```
### Key Difference Between vars and src
|vars         | src      |
|-------------|----------|
|What to do   | How to do|
|Simple       |Complex   |
|User-facing  |Internal logic|

---

## 6. Shared Library Workflow
```bash
Main Script
   ↓
Calls vars function
   ↓
vars uses src logic
   ↓
Shared code executes
   ↓
Standard output
```
### Explanation:
- A project or script uses the shared library

- A function from vars is called

- vars uses helper logic from src

- The task runs in a standardized way

---

## 7. Advantages

- Code reuse across projects

- Centralized maintenance

- Cleaner automation scripts

- Consistent standards

- Faster onboarding for new team members

- Reduced errors and duplication

---

## 8. Disadvantages

- Initial setup takes time

- Beginners need time to understand structure

- Debugging may require tracing library code

- Poor design can make changes risky

---

## 9. Best Practices

- Keep vars simple and readable

- Move complex logic to src

- Use clear naming conventions

- Document each function properly

- Avoid breaking changes without version updates

- Review and test shared library changes

- Keep one responsibility per function

---

## 10. Conclusion

A shared library is an essential building block for scalable automation. It helps teams reuse code, follow standards, and maintain consistency across projects. By separating orchestration (vars) from implementation (src), organizations can build automation that is clean, reliable, and easy to maintain—even for beginners.

---

## 11. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

## 12. References

| Links                                                                                        | Descriptions                        |
| -------------------------------------------------------------------------------------------- | ----------------------------------- |
| [https://groovy-lang.org/documentation.html](https://groovy-lang.org/documentation.html)     | Groovy Official Documentation       |
| [https://www.jenkins.io/doc/book/pipeline/shared-libraries/](https://www.jenkins.io/doc/book/pipeline/shared-libraries/) | vars Concept – Global Variables / Steps |
| [https://www.jenkins.io/doc/book/pipeline/shared-libraries/](https://www.jenkins.io/doc/book/pipeline/shared-libraries/) | src Concept – Classes & Helper Logic |


---


