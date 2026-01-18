# Title: SOP for requirement.txt

---

| Created By      | Created on   | Version | Last updated by   | Pre Reviewer   | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|-------------------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  | 2026-01-16   | 1.0     | Suraj Tripathi    |                |             |             |             |

---

## Table of Contents

1. [Purpose](#1-purpose)
2. [Scope](#2-scope)
3. [Prerequisites](#3-prerequisites)
4. [Procedure](#4-procedure)  
   4.1. [Check Disk Usage](#41-check-disk-usage)  
   &nbsp;&nbsp;&nbsp;4.1.1. [List All Mounted Filesystems & Usage](#411-list-all-mounted-filesystems--usage)  
   &nbsp;&nbsp;&nbsp;4.1.2. [Identify Top Disk Consumers](#412-identify-top-disk-consumers)  
   &nbsp;&nbsp;&nbsp;4.1.3. [Check Inode Usage](#413-check-inode-usage)  
   4.2. [Check and Manage Mount Points](#42-check-and-manage-mount-points)  
   &nbsp;&nbsp;&nbsp;4.2.1. [List Active Mounts](#421-list-active-mounts)  
   &nbsp;&nbsp;&nbsp;4.2.2. [Verify `/etc/fstab` for Persistent Mounts](#422-verify-etcfstab-for-persistent-mounts)  
   &nbsp;&nbsp;&nbsp;4.2.3. [Mount/Unmount Filesystems (if necessary)](#423-mountunmount-filesystems-if-necessary)  
   4.3. [Configure Ulimit Settings](#43-configure-ulimit-settings)  
   &nbsp;&nbsp;&nbsp;4.3.1. [Check Current Ulimit Values](#431-check-current-ulimit-values)  
   &nbsp;&nbsp;&nbsp;4.3.2. [Set Temporary Ulimit for Current Session](#432-set-temporary-ulimit-for-current-session)  
   &nbsp;&nbsp;&nbsp;4.3.3. [Configure Persistent Ulimits for Users](#433-configure-persistent-ulimits-for-users)  
   &nbsp;&nbsp;&nbsp;4.3.4. [Verify Effective Limits for a User/Process](#434-verify-effective-limits-for-a-userprocess)  
5. [Troubleshooting](#5-troubleshooting)
6. [References](#6-references)
7. [Revision History](#7-revision-history)

---

## 1. Purpose
This SOP outlines standardized procedures to provide a structured and consistent approach for installing Python packages using a requirements.txt file, generating dependency lists, and troubleshooting common dependency-related issues. This SOP ensures that application environments are set up accurately, dependencies are managed efficiently, and errors caused by version conflicts or missing packages are resolved quickly. By following this SOP, teams can achieve reliable, repeatable, and stable application setups across development, testing, and production environments.

---

## 2. Scope
This SOP applies to all team members involved in setting up, maintaining, and supporting Python-based applications. It covers the installation of dependencies from a requirements.txt file, the generation and maintenance of dependency lists, and the troubleshooting of common dependency-related issues such as version conflicts, missing packages, and environment inconsistencies. The scope includes usage across development, testing, staging, and production environments to ensure consistent and reliable application deployments.

---

## 3. Prerequisites
- **Operating System Access**-Access to a Linux, macOS, or Windows system with terminal/command-line access.
- **Python Installed**-A supported version of Python (for example, Python 3.8 or higher) installed and available in the system PATH.
- **Package Manager (pip)**-pip must be installed and configured for the corresponding Python version.
- **Virtual Environment Tool**- (Recommended)-**Availability of tools such as venv, virtualenv, or conda to isolate project dependencies.
- **requirements.txt File**-A valid requirements.txt file containing the required Python package names and versions.
- **Internet Connectivity**-Stable internet access to download packages from Python Package Index (PyPI) or configured private repositories
- **Basic Command-Line Knowledge**-Familiarity with basic terminal commands and Python package installation commands.
- **Access Permissions**-Sufficient permissions to install packages or create virtual environments on the system.

---

## 4. Installation from requirement.txt

### 4.1 Navigate to Project Directory
<img width="663" height="157" alt="image" src="https://github.com/user-attachments/assets/59a7fb2b-85f9-470a-a614-d5e941fb5af6" />


#### 4.1.1 Create a Virtual Environment (Recommended)
Create an isolated environment to avoid dependency conflicts.
```bash
python3 -m venv surajvenv
```
#### 4.1.1 Activate the Virtual Environment
<img width="961" height="143" alt="image" src="https://github.com/user-attachments/assets/d811553c-3186-4af6-9a0b-6472798ef094" />

#### 4.1.1 Activate the Virtual Environment
<img width="961" height="143" alt="image" src="https://github.com/user-attachments/assets/d811553c-3186-4af6-9a0b-6472798ef094" />

#### 4.1.1 Create the file "requirement.txt" and install the packages from the requirement file
<img width="1912" height="506" alt="image" src="https://github.com/user-attachments/assets/983e19cb-7358-44ba-8dd7-2e8616837e19" />

The **requirement.txt** file should list each Python package on a new line. For best results, use "version pinning" to ensure your code doesn't break when a library updates. 
- **Standard Entry**: package_name==version (e.g., pandas==2.2.3).
- **Alternative (Ranges):** package_name>=1.0.0 (allows any version 1.0.0 or newer).

#### 4.1.1 Verify Installation
```bash
pip list
```
<img width="1025" height="405" alt="image" src="https://github.com/user-attachments/assets/ba9eccf5-8352-4d9f-829d-0168716f4353" />

## 5. Generating Dependencies in requirement.txt
### 5.1. Activate Virtual Environment
```bash
source surajvenv/bin/activate
```
### 5.2. Install Required Packages
```bash
pip install flask requests numpy
```
### 5.3. Generate requirements.txt
- Freeze all installed dependencies into a file
```bash
pip freeze > requirements.txt
```
### 5.4. Verify requirements.txt
- Open the file and confirm contents:
```bash
cat requirements.txt
```

## 5. Troubleshooting

| Issue                     | Possible Cause                                  | Solution                                   |
|---------------------------|--------------------------------------------     |--------------------------------------------|
| pip: command not found    | pip is not installed or not in PATH.            | python3 -m pip install --upgrade pip       |
| Permission Denied Error   | Installing packages without permissions.        | Check `/etc/security/limits.conf`, relogin |
| Python Version Mismatch   | Dependencies require a different Python version.| Update `/etc/fstab` and mount manually     |  

---
---

## 6. Revision History

| Version | Date       | Author        | Change Description       |
|---------|------------|---------------|--------------------------|
| 1.0     | 2026-01-18 | Suraj tripathi| Initial version          |

---

**End of SOP**
