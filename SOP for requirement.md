# Title: SOP for requirement.txt

---

| Created By      | Created on   | Version | Last updated by   | Pre Reviewer   | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|-------------------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  | 2026-01-19   | 1.0     | Suraj Tripathi    |                |             |             |             |

---

## Table of Contents

1.1. [Purpose](#1-purpose)
2. [Scope](#2-scope)
3. [Definitions](#3-definitions)
4. [Prerequisites](#4-prerequisites)
5. [Installation from requirement.txt](#5-installation-from-requirementtxt)
   - [5.1 Navigate to Project Directory](#51-navigate-to-project-directory)
     - [5.1.1 Create a Virtual Environment (Recommended)](#511-create-a-virtual-environment-recommended)
     - [5.1.2 Activate the Virtual Environment](#512-activate-the-virtual-environment)
     - [5.1.3 Create requirements.txt and Install Packages](#513-create-the-file-requirementtxt-and-install-the-packages-from-the-requirement-file)
     - [5.1.4 Verify Installation](#514-verify-installation)
     - [5.1.5 Deactivate Virtual Environment](#515-deactivate-virtual-environment)
6. [Generating Dependencies in requirement.txt](#6-generating-dependencies-in-requirementtxt)
   - [6.1 Activate Virtual Environment](#61-activate-virtual-environment)
   - [6.2 Install Required Packages](#62-install-required-packages)
   - [6.3 Generate requirements.txt](#63-generate-requirementstxt)
   - [6.4 Verify requirements.txt](#64-verify-requirementstxt)
   - [6.5 Upgrading Dependencies from requirements.txt](#65-Upgrading-dependencies-from-requirementstxt)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. Purpose
This SOP provides a standardized and consistent approach for installing Python packages using a requirements.txt file, generating dependency lists, and troubleshooting common dependency-related issues.

Following this SOP ensures:

- Accurate environment setup

- Efficient dependency management

- Reduced errors due to version conflicts or missing packages

Reliable and repeatable application setups across development, testing, staging, and production environments
---

## 2. Scope
This SOP applies to all team members involved in developing, maintaining, and supporting Python-based applications.

It covers:

- Installing dependencies from requirements.txt

- Generating and maintaining dependency lists

- Handling version conflicts and missing packages

- Usage across development, testing, staging, and production environments

---

## 3. Definitions

| Term | Description |
|------|-------------|
| pip | Python package manager used to install Python dependencies |
| requirements.txt | File containing a list of required Python packages and versions |
| Virtual Environment | Isolated Python environment to manage project dependencies |
| Version Pinning | Locking dependency versions to avoid breaking changes 

---

## 4. Prerequisites
### Supported Python Versions
- Python 3.8
- Python 3.9
- Python 3.10
- Python 3.11

#### System & Access Requirements

- Linux, macOS, or Windows system

- Terminal / command-line access

- Python installed and available in system PATH

- pip installed and configured

- Virtual environment tool (venv, virtualenv, or conda) – recommended

- Valid requirements.txt file

- Internet access to PyPI or private repositories

- Sufficient permissions to install packages or create virtual environments

- Basic command-line knowledge

---

## 5. Installation from requirement.txt

## 5.1 Navigate to Project Directory
<img width="663" height="157" alt="image" src="https://github.com/user-attachments/assets/59a7fb2b-85f9-470a-a614-d5e941fb5af6" />


### 5.1.1 Create a Virtual Environment (Recommended)
Create an isolated environment to avoid dependency conflicts.
```bash
python3 -m venv surajvenv
```
### 5.1.2 Activate the Virtual Environment
<img width="961" height="143" alt="image" src="https://github.com/user-attachments/assets/d811553c-3186-4af6-9a0b-6472798ef094" />

### 5.1.3 Create the file "requirement.txt" and install the packages from the requirement file
<img width="1912" height="506" alt="image" src="https://github.com/user-attachments/assets/983e19cb-7358-44ba-8dd7-2e8616837e19" />

The **requirement.txt** file should list each Python package on a new line. For best results, use "version pinning" to ensure your code doesn't break when a library updates. 
- **Standard Entry**: package_name==version (e.g., pandas==2.2.3).
- **Alternative (Ranges):** package_name>=1.0.0 (allows any version 1.0.0 or newer).

### 5.1.4 Verify Installation
```bash
pip list
```
<img width="1025" height="405" alt="image" src="https://github.com/user-attachments/assets/ba9eccf5-8352-4d9f-829d-0168716f4353" />

### 5.1.5 Deactivate Virtual Environment
After completing the required tasks, deactivate the virtual environment:
```bash
deactivate
```

## 6. Generating Dependencies in requirement.txt
### 6.1. Activate Virtual Environment
```bash
source surajvenv/bin/activate
```
### 6.2. Install Required Packages
```bash
pip install flask requests numpy
```
### 6.3. Generate requirements.txt
- Freeze all installed dependencies into a file
```bash
pip freeze > requirements.txt
```
### 6.4. Verify requirements.txt
- Open the file and confirm contents:
```bash
cat requirements.txt
```
### 6.5. Upgrading Dependencies from requirements.txt
To upgrade all packages based on the versions defined in requirements.txt:
```bash
pip install --upgrade -r requirements.txt
```
To upgrade a specific package:
```bash
pip install --upgrade package_name
```

## 7. Troubleshooting

| Issue                     | Possible Cause                                  | Solution                                   |
|---------------------------|--------------------------------------------     |--------------------------------------------|
| pip: command not found    | pip is not installed or not in PATH.            | python3 -m pip install --upgrade pip       |
| Permission Denied Error   | Installing packages without permissions.        | Check `/etc/security/limits.conf`, relogin |
| Python Version Mismatch   | Required Python version not installed           | Install the correct Python version and recreate the virtual environment     |  

---

**End of SOP**
