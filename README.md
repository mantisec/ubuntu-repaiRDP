# **Ubuntu RDP Remediation & Configuration Toolkit**

Setting up Remote Desktop (RDP) on modern Ubuntu releases often leads to incredibly frustrating issues: black screens, immediate connection drops, conflicting lock files, and TLS certificate failures.

This toolkit is an interactive, all-in-one CLI utility designed to seamlessly install, meticulously configure, or completely repair your RDP environment.

**Idea & Concept by:** Mantisec

**Engineered by:** Google Gemini ( 3 prompts :) )

## **🌟 Features**

* **Comprehensive System Diagnostics:** Detects your OS, active Desktop Managers, phantom X11 locks, TLS permissions, and conflicting RDP packages.  
* **Support for Next-Gen gnome-remote-desktop:** Fully supports Ubuntu 24.04+ Native RDP in both **System Daemon Mode** (Headless login) and **User Mode** (Automated auto-login injection).  
* **Flawless XRDP & XFCE4 Support:** Automates .xsession files and applies the mandatory GNOME\_SHELL\_SESSION\_MODE fixes to prevent XRDP black screens.  
* **Automated TLS Certificate Generation:** Generates 10-year self-signed certificates and correctly assigns ssl-cert group permissions, resolving handshake drops.  
* **Deep Repair Mode:** Detects broken packages, purges conflicting configurations, clears ghost X11 locks (/tmp/.X\*-lock), and safely resets corrupt user dconf desktop profiles.  
* **Built-in Backup & Restore:** Automatically creates timestamped .tar.gz recovery archives with an audit log of every file changed. Roll back changes instantly via the built-in Restore Menu.

## **🚀 Quick Start**

1. **Download the script:**  
   wget \[https://raw.githubusercontent.com/mantisec/ubuntu-repaiRDP/main/main.sh\](https://raw.githubusercontent.com/mantisec/ubuntu-repaiRDP/main/main.sh)

2. **Make it executable:**  
   chmod \+x main.sh

3. **Run the toolkit as root:**  
   sudo ./main.sh

## **🖥️ Usage Guide**

Upon launching the script, you will be presented with a Main Menu:

### **1\) Run Comprehensive System Diagnostic Report**

Use this before making any changes. It will scan your machine to identify if XRDP or GRD are installed, check if Port 3389 is actually listening, and analyze the system for known issues (like missing user groups or phantom display locks).

### **2\) Install, Configure, or Repair RDP**

This is the main engine. You will be prompted to:

* Opt-in to **Deep Repair** (Highly recommended for broken systems).  
* Select your desired engine (**gnome-remote-desktop** or **xrdp**).  
* Select your Desktop Environment (**Gnome** or **XFCE4**).  
* Set up the RDP user and password (with double-confirmation).

*The script handles the rest: stopping conflicts, backing up original configs, installing dependencies, applying TLS fixes, and tweaking firewall rules.*

### **3\) Restore System from Backup Archive**

Every time you run an Install/Repair, the toolkit copies the original state of modified files (like /etc/xrdp/xrdp.ini, /etc/gdm3/custom.conf, user .config files) into a .tar.gz archive saved in /opt/rdp\_remediation\_backups/.

Select this menu option to extract an archive and instantly roll back the system.

## **🛠️ Under the Hood Fixes**

Here are some of the critical bugs this script automatically remediates:

* **XRDP Black Screen on Gnome:** Injects export GNOME\_SHELL\_SESSION\_MODE=ubuntu into /etc/xrdp/startwm.sh.  
* **TLS Dropouts:** Generates custom keys and ensures the xrdp or gnome-remote-desktop system users belong to the ssl-cert group.  
* **Zombie Display Ports:** Automates the removal of stale /tmp/.X\*-lock and /tmp/.X11-unix/X\* sockets that block new GUI sessions.  
* **Gnome Dconf Corruption:** Optionally wipes corrupt user dconf, mutter, and gnome-session configs that cause instant crashes upon connection.

## **📄 License**

MIT License. Free to use, fork, and distribute.
