---
title: Killua
toc: True
description: Vulnerbility Assesment on Unix-Based Debian systems
courses: {'csp': {'week': 3}}
type: hacks
---

# Comprehensive Understanding of Linux Bash and Shell Scripting

In this script, we demonstrate a comprehensive understanding of Linux Bash scripting to perform system configuration and security checks. This script evaluates various aspects of a Linux system to ensure its security and compliance with best practices.

## 1. Functions for Success and Failure Messages

We define functions for displaying success and failure messages with appropriate colors, making the output easily readable and informative.

```bash
function SuccessMessage () {
    # Display success message in green
}

function FalseMessage () {
    # Display failure message in red
}
```

## File and Command Checks
We use conditional statements and commands to check for specific conditions within files and the output of commands. 
Here are some notable examples:

### FileContains and FileContainsNot
These functions check if a specified pattern exists or does not exist within a file, displaying appropriate messages.
```bash
FileContains "dpkg -l aide" "no packages" "1.3.1" "Ensure AIDE is installed"
FileContainsNot "dpkg -l prelink" "prelink" "1.5.3" "Ensure prelink is not installed"
```
### CommandContains and CommandContainsNot
These functions execute commands and check if the output contains or does not contain a specific pattern.
```bash
CommandContains "systemctl is-enabled autofs" "disabled" "1.1.23" "Disable Automounting"
CommandContainsNot "dpkg -l xserver-xorg*" "no packages" "2.1.2" "Ensure X Window System is not installed"
```

## 3. System Configuration Checks

Ensuring the absence of unnecessary services:
```bash
CommandContainsNot "dpkg -l rsh-client" "no packages" "2.2.2" "Ensure rsh client is not installed"
```

Checking for required software packages:
```bash
CommandContains "dpkg -l auditd" "no packages" "4.1.1.1" "Ensure auditd is installed"```
```

Validating system log settings:
```bash
CommandContains "grep max_log_file_action /etc/audit/auditd.conf" "max_log_file_action = keep_logs" "4.1.2.2" "Ensure audit logs are not automatically deleted"
```
## 4. Security and Compliance Measures
The script covers a wide range of security and compliance measures, such as disabling unnecessary services, controlling USB storage, and ensuring the presence of required packages. It also checks for proper log management and configuration. These are also taken directly from CIS benchmarks and has direct use from real corporations and small businesses for people

## 5. Output Clarity
The script utilizes colorful output messages to clearly indicate whether a check passed or failed, making it easy for users to identify issues at a glance.

In summary, this script demonstrates a deep understanding of Linux Bash scripting, including functions, conditional statements, file manipulation, and command execution. It is a powerful tool for system administrators and security professionals to assess and maintain the security and compliance of Linux systems.


```python
%%script bash

####### Format: Vuln name (V-4249) and then the actual vuln "Grub has a password"
function SuccessMessage () {
    echo -e "\e[92m[+]\e[39m Check for OS: Ubuntu 20 - \e[92m$1: $2"
}

function FalseMessage () {
    echo -e "\e[91m[-]\e[39m Check for OS: Ubuntu 20 - \e[91m$1: $2"
}

####### Format: file, pattern to look for in a file, vuln name, and then the acutal vuln
function FileContains () {
    if [ ! -f "$1" ]; then
        echo -e "\e[93m$3: $4. - $1 does not exist"
    else
        if grep -Fxq "$2" $1
        then
            # code if found
            SuccessMessage "$3" "$4"
        else
            # code if not found
            FalseMessage "$3" "$4"
        fi
    fi
    
}

function FileContainsNot () {
    if [ ! -f "$1" ]; then
        echo -e "\e[93m$3: $4. - $1 does not exist"
    else
        if grep -q $2 "$1"
        then
            # code if found
            FalseMessage "$3" "$4"
        else
            # code if not found
            SuccessMessage "$3" "$4"
        fi
    fi
    
}

function CommandContains() {
    if $1 | grep -q "$2"; then
        SuccessMessage "$3" "$4"
    else
        FalseMessage "$3" "$4"
    fi
}

function CommandContainsNot() {
    if $1 | grep -q "$2"; then
        FalseMessage "$3" "$4"
    else
        SuccessMessage "$3" "$4"
    fi
}

#CommandContains "journalctl 'protection: active'" "kernel: NX (Execute Disable) protection: active" "1.5.1" "Ensure XD/NX support is enabled"
CommandContains "systemctl is-enabled autofs" "disabled" "1.1.23" "Disable Automounting"
CommandContains "modprobe -n -v usb-storage" "install /bin/true" "1.1.24" "Disable USB Storage"
CommandContains "dpkg -l aide" "no packages" "1.3.1" "Ensure AIDE is installed"
CommandContains "dpkg -l aide-common" "no packages" "1.3.1" "Ensure aide-common is installed"
CommandContainsNot "dpkg -l prelink" "prelink" "1.5.3" "Ensure prelink is not installed"
CommandContains "dpkg -l apparmor" "no packages" "1.6.1.1" "Ensure AppArmor is installed"
CommandContainsNot "dpkg -l xserver-xorg*" "no packages" "2.1.2" "Ensure X Window System is not installed"
CommandContainsNot "dpkg -l avahi-daemon" "no packages" "2.1.3" "Ensure RPC is not installed"
CommandContainsNot "dpkg -l isc-dhcp-server" "no packages" "2.1.5" "Ensure DHCP Server is not installed"
CommandContainsNot "dpkg -l nfs-kernel-server" "no packages" "2.1.7" "Ensure NFS is not installed"
CommandContainsNot "dpkg -l nis" "no packages" "2.1.17" "Ensure NIS Server is not installed"
CommandContainsNot "dpkg -l rsh-client" "no packages" "2.2.2" "Ensure rsh client is not installed"
CommandContainsNot "dpkg -l talk" "no packages" "2.2.3" "Ensure talk client is not installed"
CommandContainsNot "dpkg -l ldap-clients" "no packages" "2.2.5" "Ensure LDAP client is not installed"
CommandContainsNot "dpkg -l rpcbind" "no packages" "2.2.6" "Ensure RPC is not installed"
CommandContainsNot "dpkg -l iptables-persistent" "no packages" "3.5.1.2" "Ensure iptables-persistent is not installed with ufw"
CommandContains "dpkg -l auditd" "no packages" "4.1.1.1" "Ensure auditd is installed"
CommandContains "dpkg -l audispd-plugins" "no packages" "4.1.1.1" "Ensure audispd-plugins is installed"
CommandContains "systemctl is-enabled auditd" "enabled" "4.1.1.2" "Ensure auditd service is enabled"
CommandContains "grep max_log_file_action /etc/audit/auditd.conf" "max_log_file_action = keep_logs" "4.1.2.2" "Ensure audit logs are not automatically deleted"
CommandContains "grep '^\s*[^#]' /etc/audit/rules.d/*.rulestail -1" "-e 2" "4.1.17" "Ensure the audit configuration is immutable"
CommandContainsNot "dpkg -l rsyslog" "no packages" "4.2.1.1" "Ensure rsyslog is installed"
CommandContains "grep -e ForwardToSyslog /etc/systemd/journald.conf" "ForwardToSyslog=yes" "4.2.2.1" "Ensure journald is configured to send logs to rsyslog"
CommandContains "grep -e Compress /etc/systemd/journald.conf" "Compress=yes" "4.2.2.2" "Ensure journald is configured to compress large log files"
CommandContains "grep -e Storage /etc/systemd/journald.conf" "Storage=persistent" "4.2.2.1" "Ensure journald is configured to write logfiles to persistent disk"
```

    Failed to get unit file state for autofs.service: No such file or directory


    [91m[-][39m Check for OS: Ubuntu 20 - [91m1.1.23: Disable Automounting


    modprobe: FATAL: Module usb-storage not found in directory /lib/modules/5.10.16.3-microsoft-standard-WSL2


    [91m[-][39m Check for OS: Ubuntu 20 - [91m1.1.24: Disable USB Storage


    dpkg-query: no packages found matching aide


    [91m[-][39m Check for OS: Ubuntu 20 - [91m1.3.1: Ensure AIDE is installed


    dpkg-query: no packages found matching aide-common


    [91m[-][39m Check for OS: Ubuntu 20 - [91m1.3.1: Ensure aide-common is installed


    dpkg-query: no packages found matching prelink


    [92m[+][39m Check for OS: Ubuntu 20 - [92m1.5.3: Ensure prelink is not installed
    [91m[-][39m Check for OS: Ubuntu 20 - [91m1.6.1.1: Ensure AppArmor is installed


    dpkg-query: no packages found matching xserver-xorg*


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.1.2: Ensure X Window System is not installed


    dpkg-query: no packages found matching avahi-daemon


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.1.3: Ensure RPC is not installed


    dpkg-query: no packages found matching isc-dhcp-server


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.1.5: Ensure DHCP Server is not installed
    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.1.7: Ensure NFS is not installed
    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.1.17: Ensure NIS Server is not installed
    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.2.2: Ensure rsh client is not installed


    dpkg-query: no packages found matching talk


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.2.3: Ensure talk client is not installed


    dpkg-query: no packages found matching ldap-clients


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.2.5: Ensure LDAP client is not installed


    dpkg-query: no packages found matching rpcbind


    [92m[+][39m Check for OS: Ubuntu 20 - [92m2.2.6: Ensure RPC is not installed


    dpkg-query: no packages found matching iptables-persistent


    [92m[+][39m Check for OS: Ubuntu 20 - [92m3.5.1.2: Ensure iptables-persistent is not installed with ufw


    dpkg-query: no packages found matching auditd


    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.1.1.1: Ensure auditd is installed


    dpkg-query: no packages found matching audispd-plugins


    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.1.1.1: Ensure audispd-plugins is installed


    Failed to get unit file state for auditd.service: No such file or directory


    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.1.1.2: Ensure auditd service is enabled


    grep: /etc/audit/auditd.conf: No such file or directory


    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.1.2.2: Ensure audit logs are not automatically deleted


    grep: /etc/audit/rules.d/*.rulestail: No such file or directory


    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.1.17: Ensure the audit configuration is immutable
    [92m[+][39m Check for OS: Ubuntu 20 - [92m4.2.1.1: Ensure rsyslog is installed
    [92m[+][39m Check for OS: Ubuntu 20 - [92m4.2.2.1: Ensure journald is configured to send logs to rsyslog
    [92m[+][39m Check for OS: Ubuntu 20 - [92m4.2.2.2: Ensure journald is configured to compress large log files
    [91m[-][39m Check for OS: Ubuntu 20 - [91m4.2.2.1: Ensure journald is configured to write logfiles to persistent disk



```python

```
