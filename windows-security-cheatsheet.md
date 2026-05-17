# Windows Fundamentals Cheatsheet

## Quick Launch Commands
| Command | Opens |
|---------|-------|
| `msconfig` | System Configuration |
| `lusrmgr.msc` | Local Users and Groups |
| `regedit` | Registry Editor |
| `msinfo32` | System Information |
| `resmon` | Resource Monitor |
| `cmd` | Command Prompt |
| `control` | Control Panel |
| `taskmgr` | Task Manager |
| `winver` | Windows Version |

---

## File System
| Path | Purpose |
|------|---------|
| `C:\Windows\System32` | Core OS files, high-value target |
| `C:\Users\<username>` | User profiles and data |
| `C:\Program Files` | Installed 64-bit applications |
| `C:\Program Files (x86)` | Installed 32-bit applications |
| `C:\ProgramData` | Hidden app data |
| `%TEMP%` | Temp files, often used by malware |

**NTFS Feature:** Alternate Data Streams (ADS) allows files to contain more than one stream of data. Malware writers use ADS to hide data.

---

## User Accounts & Permissions
- **Account Types:** Administrator and Standard User
- **Administrator:** Full control over the system
- **Standard User:** Limited, cannot make system-level changes
- **UAC (User Account Control):** Prompts for confirmation before allowing elevated actions — prevents silent privilege escalation

---

## Registry
| Hive | Purpose |
|------|---------|
| `HKEY_LOCAL_MACHINE (HKLM)` | System-wide settings |
| `HKEY_CURRENT_USER (HKCU)` | Current user settings |
| `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` | Programs that start at boot — persistence mechanism |

---

## Task Manager Tabs
| Tab | Purpose |
|-----|---------|
| Processes | What is running and who owns it |
| Performance | CPU, memory, disk, network usage |
| Startup | What runs at boot |
| Services | Background services |
| Users | Active user sessions |

---

## System Configuration (MSConfig)
- Used for troubleshooting and managing startup
- **General Tab:** Selective, diagnostic, or normal startup
- **Boot Tab:** Boot options and safe mode
- **Services Tab:** Enable/disable background services
- **Startup Tab:** Redirects to Task Manager
- **Tools Tab:** Shortcuts to system utilities

---

## System Information (msinfo32)
- **System Summary:** OS version, hardware, BIOS info
- **Hardware Resources:** IRQs, memory addresses
- **Components:** Devices and drivers
- **Software Environment:** Running tasks, startup programs, environment variables

---

## Resource Monitor (resmon)
- Real-time view of CPU, memory, disk, and network usage
- More detailed than Task Manager
- Useful for identifying processes hogging resources

---

## Event Viewer — Event Types
| Type | Meaning |
|------|---------|
| Critical | System or application will stop functioning, immediate attention required |
| Error | Significant problem such as loss of data or functionality |
| Warning | Not currently a problem but could become one |
| Information | Successful operation of a program or service |
| Success Audit | Audited security access attempt succeeded |
| Failure Audit | Audited security access attempt failed |

---

## Windows Security Tools

### Windows Update
- Keeps OS patched against known vulnerabilities
- Should never be disabled in a production environment

### Windows Defender (Virus & Threat Protection)
- Real-time malware protection
- Quarantines and removes threats
- Controlled Folder Access — protects against ransomware

### Firewall & Network Protection
| Profile | Used When |
|---------|-----------|
| Domain | Connected to a domain network |
| Private | Home or trusted network |
| Public | Untrusted networks (coffee shops, airports) |

### App & Browser Control (SmartScreen)
- Blocks unrecognized apps and files
- Protects against phishing and malicious sites in Edge

### Device Security
- **Core Isolation / Memory Integrity:** Protects core OS processes from malware injection
- **Secure Boot:** Prevents unauthorized OS from loading at startup
- **TPM (Trusted Platform Module):** Hardware-based security chip for encryption and authentication

### BitLocker
- Full disk encryption for Windows volumes
- Protects data if device is stolen or drive is removed
- Requires TPM or a startup key/PIN

### Volume Shadow Copy Service (VSS)
- Creates snapshots (shadow copies) of files and volumes
- Used for backup and system restore
- **Attacker relevance:** Ransomware often deletes shadow copies to prevent recovery
- Command to delete shadow copies (used by malware): `vssadmin delete shadows /all /quiet`