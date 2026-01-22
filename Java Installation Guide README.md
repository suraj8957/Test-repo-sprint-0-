# Java Installation Guide (Windows, Linux, macOS)

This document provides a step-by-step guide to **download, install, and configure Java** on **Windows, Linux, and macOS** systems.  
It also explains how to verify the installation and configure environment variables.

---
## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  2026-01-16  |  1.0    |                |             |             |             |

## Table of Contents

1. Introduction  
2. Java Installation on Windows  
3. Java Installation on Linux  
4. Java Installation on macOS  
5. Conclusion

---

## 1. Introduction

Java is a widely used programming language and runtime environment required for building and running Java-based applications.  
In this guide we covers the installation of **Java Development Kit (JDK)** on different operating systems and the configuration required to run Java programs from the command line.

---

## 2. Java Installation on Windows (64-bit)

This process works for **Windows 7, 8, 10, and 11**.

### Step 1: Download Java

1. Open the official Oracle website: https://www.oracle.com/in/java/
2. Click on **Download Java**
3. Select **Windows**
4. Download the **x64 Installer (.exe)** for the latest JDK version

---

### Step 2: Install Java

1. Go to the **Downloads** folder
2. Double-click on the downloaded file  
   `jdk-23_windows-x64_bin.exe`
3. Click **Next**
4. Click **Next** again to start the installation
5. Wait for the installation to complete
6. Click **Close** to finish

---

### Step 3: Configure Environment Variables (JAVA PATH)

1. Go to:
```bash
C:\Program Files\Java\jdk-23\bin
```
2. Copy the full path of the **bin** folder
3. Search for **Environment Variables** in Windows
4. Click **Edit the system environment variables**
5. Click **Environment Variables**
6. Under **System variables**, select **Path**
7. Click **Edit**
8. Click **New**
9. Paste the copied path
10. Click **OK** → **OK** → **OK**

---

### Step 4: Verify Java Installation (Windows)
1. Open **Command Prompt**
2. Run:
```bash
java --version
```
3. If Java version is displayed, installation is successful ✅

---

## 3. Java Installation on Linux

### Step 1: Identify Linux Distribution
```bash
cat /etc/os-release
```
---
### Step 2: Update System Packages
|Operating System|Command|
|----------------|-------|
| Ubuntu / Debian|sudo apt update|
|Amazon Linux / CentOS / RHEL / Rocky / Alma|sudo yum update -y|
|Arch Linux|sudo pacman -Syu|

---

### Step 3: Install Java (OpenJDK)
|Operating System|Command|
|----------------|-------|
|Ubuntu / Debian|sudo apt install openjdk-17-jdk -y|
|Amazon Linux 2|sudo yum install java-17-amazon-corretto -y|
|RHEL / CentOS / Rocky / Alma|sudo dnf install java-17-openjdk -y|
|Arch Linux|sudo pacman -S jdk17-openjdk|

---

### Step 4: Verify Java Installation (Linux)
```bash
java --version
```
---

### Step 5: Find Java Installation Path
```bash
readlink -f $(which java)
```
---
### Step 6: Set JAVA_HOME
1. Open .bashrc file:
```bash
nano ~/.bashrc
```
2. Add the following lines:
```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```
3. Save and exit:
```bash
CTRL + O → Enter
CTRL + X
```
4. Reload configuration:
```bash
source ~/.bashrc
```
5. Verify:
```bash
echo $JAVA_HOME
```
---
### Step 7: Manage Multiple Java Versions (Optional)
```bash
sudo update-alternatives --config java
```
---
## 4. Java Installation on macOS
### Step 1: Update Homebrew
```bash
brew update
```
---
### Step 2: Install OpenJDK
```bash
brew install openjdk@17
```
---
### Step 3: Set JAVA_HOME (macOS)
```bash
echo 'export JAVA_HOME=/opt/homebrew/opt/openjdk@17' >> ~/.zshrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.zshrc
source ~/.zshrc
```
---
### Step 4: Verify Java Installation (macOS)
```bash
java -version
```
---
## 5. Conclusion
Java is now successfully installed and configured on your system.




