# RansomwareTool.exe

Educational ransomware simulation tool for testing file encryption/decryption workflows.

## Overview

RansomwareTool.exe is a Python-based file encryption tool compiled to a standalone Windows executable. ItDemonstrates file locking using Fernet symmetric encryption (derived from AES-128). The tool is Intended for educational and authorized testing purposes only.

## Password

```
here_is_gun
```

**Important:** This password is hardcoded in the application for demonstration purposes.

## Supported File Extensions

| Category | Extensions |
| -------- | ---------- |
| Documents | .txt, .docx, .doc, .xlsx, .xls, .pptx |
| Images | .jpg, .png |
| Archives | .zip, .rar |
| Other | .pdf |

## How It Works

### Encryption
1. Reads the target directory recursively
2. For each supported file (not already `.locked`):
   - Generates encryption key from password using SHA-256
   - Encrypts file contents with Fernet (AES-128)
   - Saves encrypted data to `filename.ext.locked`
   - Deletes original file

### Decryption
1. Scans for files ending with `.locked`
2. Uses password to derive decryption key
3. Decrypts and restores original filename
4. Deletes encrypted file

## Usage

```bash
wine RansomwareTool.exe
```

Or on Windows:
```
RansomwareTool.exe
```

### Interactive Menu
1. Select `[1]` to encrypt files
2. Enter directory path when prompted
3. Select `[2]` to decrypt files
4. Enter directory path containing `.locked` files

## Technical Details

| Component | Details |
| --------- | --------
| Language | Python 3.x |
| Encryption | Fernet (symmetric, URL-safe base64) |
| Key Derivation | SHA-256 hash of password |
| Compiled | PyInstaller |

## Legal Disclaimer

This tool is provided for educational purposes only. The developer is not responsible for any misuse or damages caused by this software. Always obtain explicit authorization before testing on any system.

## File Structure

```
dist123/
├── RansomwareTool.exe  # Compiled executable
└── README.md          # This file
```

## Building from Source

```bash
# Install dependencies
pip install cryptography pyinstaller

# Build executable
pyinstaller --onefile --name RansomwareTool main.py
```