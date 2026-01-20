# Standard Operating Procedure (SOP's) for Java Installation and Upgrade Using Bash Script (Ubuntu/Debian)

## Document Details

---

## Table of Contents

 1. [Purpose](#1-Purpose)
 2. [Scope](#2-Scope)
 3. [Prerequisites](#3-Prerequisites)
 4. [Script_Overview](#4-Script_Overview)
 5. Create the Bash Script
 6. Grant Execute Permission
 7. Execute the Script
 8. Java Version Selection
 9. Java Installation Process
10. Java Upgrade / Version Switching
11. Author
12. References

---

## 1. Purpose

This SOP describes the step-by-step procedure to install and manage Java using a generic Bash script.
The script supports multiple Java versions (8, 11, 17, 21) and allows safe upgrades or version switching without removing existing Java installations.

---

## 2. Scope

|Operating System|Java Distribution|Supported Java Versions|Installation Type|Upgrade Support|
|----------------|-----------------|-----------------------|-----------------|---------------|
| Ubuntu / Debian |     OpenJDK     |     8, 11, 17, 21     | Automated via Bash script| Yes (via update-alternatives)|

---

## 3. Prerequisites

Before running the script, ensure the following:

- Ubuntu or Debian-based system

- User has sudo access

- Internet connectivity is available

- Bash shell is available

#### Verify prerequisites
```bash
lsb_release -a
```
```bash
whoami
```

---

## 4. Script_Overview

- The script performs the following actions:

- Verifies OS compatibility

- Checks for existing Java installation

- Prompts user to select a Java version

- Installs the selected OpenJDK version

- Switches default Java using update-alternatives

- Configures JAVA_HOME system-wide

- Verifies installation

---

## 5. Create the Bash Script
Create a file for the Java installation script: install_java.sh
```bash
#!/bin/bash

# -------------------------------
# Generic Java Installation Script
# Supports Java 8, 11, 17, 21
# Works on Ubuntu/Debian
# -------------------------------

set -e

SUPPORTED_VERSIONS=("8" "11" "17" "21")

echo "==============================="
echo " Java Installation Script"
echo "==============================="

# Check OS
if ! command -v apt &>/dev/null; then
  echo "❌ This script supports only Debian/Ubuntu systems."
  exit 1
fi

# Show installed Java (if any)
if command -v java &>/dev/null; then
  echo "✔ Existing Java installation found:"
  java -version
else
  echo "ℹ No Java installation found."
fi

# Ask for Java version
echo ""
echo "Supported Java versions: ${SUPPORTED_VERSIONS[*]}"
read -p "Enter Java version to install: " JAVA_VERSION

if [[ ! " ${SUPPORTED_VERSIONS[*]} " =~ " ${JAVA_VERSION} " ]]; then
  echo "❌ Unsupported Java version."
  exit 1
fi

PACKAGE="openjdk-${JAVA_VERSION}-jdk"

echo ""
echo "Installing ${PACKAGE} ..."

sudo apt update -y
sudo apt install -y ${PACKAGE}

echo "✔ Java ${JAVA_VERSION} installed successfully."

# Configure alternatives
echo ""
echo "Configuring default Java version..."
sudo update-alternatives --set java /usr/lib/jvm/java-${JAVA_VERSION}-openjdk-amd64/bin/java || true

# Set JAVA_HOME
JAVA_HOME_PATH="/usr/lib/jvm/java-${JAVA_VERSION}-openjdk-amd64"

echo "Setting JAVA_HOME=${JAVA_HOME_PATH}"

PROFILE_FILE="/etc/profile.d/java.sh"

sudo bash -c "cat > ${PROFILE_FILE}" <<EOF
export JAVA_HOME=${JAVA_HOME_PATH}
export PATH=\$JAVA_HOME/bin:\$PATH
EOF

sudo chmod +x ${PROFILE_FILE}

echo ""
echo "✔ JAVA_HOME configured."
echo "✔ Java installation completed."

echo ""
echo "==============================="
echo " Java Version"
echo "==============================="
java -version

echo ""
echo "Please logout/login or run: source ${PROFILE_FILE}"

```

## 6. Grant Execute Permission
Make the script executable:
```bash
chmod +x install_java.sh
```

## 7. Execute the Script
Run the script using:
```bash
./install_java.sh
```

Used to update the local package index from repositories.

➡️ Note: APT internally uses dpkg for installing, removing, and managing packages.

## 8. Java Version Selection
When prompted, enter one of the supported Java versions:
```bash
8 | 11 | 17 | 21
```
#### Notes:
If an unsupported version is entered, the script will exit safely.

## 9. Java Installation Process
After version selection, the script will:

- Update package repositories

- Install the selected OpenJDK package

- Display a success message after installation

<img width="1736" height="940" alt="image" src="https://github.com/user-attachments/assets/a5ef6920-7c45-4845-b6de-6c24fdfdbd00" />


## 10. Java Upgrade / Version Switching

- To upgrade or switch Java versions:

- Re-run the same script

- Select a different Java version

#### Behavior:

- New Java version is installed

- Default Java version is switched using update-alternatives

- Existing Java versions are not removed
 ---
 ## 11. JAVA_HOME Configuration
 The script configures JAVA_HOME system-wide by creating:
 ```bash
/etc/profile.d/java.sh
```
Contents include:
```bash
export JAVA_HOME=/usr/lib/jvm/java-<version>-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
```
#### Apply immediately:
```bash
source /etc/profile.d/java.sh
```

 ## 12. Verification
 Verify Java installation:
 ```bash
java -version
```
<img width="956" height="156" alt="image" src="https://github.com/user-attachments/assets/444e278a-6725-4297-ac9b-066d68ea7608" />

Verify JAVA_HOME:
 ```bash
echo $JAVA_HOME
```
<img width="676" height="98" alt="image" src="https://github.com/user-attachments/assets/51b0b944-8fc0-4c40-9347-5d3150196eb7" />

## 13. Troubleshooting

#### Issue: Java version not switching
```bash
sudo update-alternatives --config java
```

#### Issue: JAVA_HOME not updated
- Log out and log back in
  OR
  ```bash
  source /etc/profile.d/java.sh
  ```

#### Issue: Script fails immediately
- Ensure OS is Ubuntu/Debian

- Ensure apt command is available

## 14. Best Practices
- Do not manually remove older Java versions

- Always use update-alternatives for switching Java

- Use scripts to ensure consistency across environments

- Re-run the script for upgrades instead of manual installs
---

## 15. Conclusion
This SOP provides a standardized, repeatable, and upgrade-safe method to install and manage Java using a Bash script.
