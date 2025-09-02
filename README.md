# OpenSSL vcpkg NuGet Package

[![Build Status](https://github.com/darioajr/openssl-vcpkg-nuget/workflows/build-nuget/badge.svg)](https://github.com/darioajr/openssl-vcpkg-nuget/actions)
[![NuGet Version](https://img.shields.io/nuget/v/openssl.vcpkg.svg)](https://www.nuget.org/packages/openssl.vcpkg/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

This project creates a NuGet package of OpenSSL compiled using vcpkg for Windows x64 with Visual Studio 2022 (vc143).

## 📋 Overview

OpenSSL is a robust, commercial-grade, and full-featured cryptography library for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library.

This NuGet package includes:
- 🔐 **OpenSSL version 1.1.1n (NuGet: 1.1.1.14)**
- 📚 **Static and dynamic libraries**
- 📁 **Development headers**
- ⚙️ **Automatic configuration for Visual Studio**
- 🖥️ **Windows x64 support**

## 🚀 Installation

### Via NuGet Package Manager

```powershell
Install-Package openssl.vcpkg
```

### Via .NET CLI

```bash
dotnet add package openssl.vcpkg
```

### Via PackageReference

```xml
<PackageReference Include="openssl.vcpkg" Version="1.1.1.14" />
```

## 📦 Package Contents

```
openssl.vcpkg/
├── build/
│   └── native/
│       ├── include/           # OpenSSL headers
│       ├── lib/
│       │   └── x64/
│       │       ├── Release/   # Release libraries
│       │       └── Debug/     # Debug libraries
│       ├── bin/
│       │   └── x64/
│       │       ├── Release/   # Release DLLs
│       │       └── Debug/     # Debug DLLs
│       └── openssl.vcpkg.targets
```

## 🔧 Usage

### Automatic Configuration

The package automatically configures:
- **Include Directories**: OpenSSL headers are automatically added
- **Library Directories**: Libraries are automatically linked
- **Dependencies**: `libssl.lib`, `libcrypto.lib`, `ws2_32.lib`, `crypt32.lib`
- **DLLs**: Automatically copied to output directory

### C++ Usage Example

```cpp
#include <openssl/ssl.h>
#include <openssl/err.h>
#include <openssl/crypto.h>

int main() {
    // Initialize OpenSSL
    SSL_library_init();
    SSL_load_error_strings();
    OpenSSL_add_all_algorithms();
    
    // Your application here
    printf("OpenSSL Version: %s\n", OPENSSL_VERSION_TEXT);
    
    // Cleanup
    EVP_cleanup();
    CRYPTO_cleanup_all_ex_data();
    ERR_free_strings();
    
    return 0;
}
```

## ⚙️ Requirements

- **Operating System**: Windows 10/11
- **Architecture**: x64
- **Visual Studio**: 2022 (vc143)
- **Runtime**: Visual C++ Redistributable 2022

## 🏗️ Included Libraries

### Release
- `libssl.lib` - SSL library
- `libcrypto.lib` - Cryptography library

### Debug
- `libssl.lib` - SSL library (Debug)
- `libcrypto.lib` - Cryptography library (Debug)

### System Dependencies
- `ws2_32.lib` - Windows Sockets API
- `crypt32.lib` - Windows Cryptography API

## 🔒 OpenSSL Version

This package uses **OpenSSL 1.1.1n** (NuGet version: 1.1.1.14), which includes:
- Complete TLS/SSL support
- Symmetric and asymmetric cryptography algorithms
- Cryptographic hash functions
- X.509 certificates
- Cryptographically secure random number generators

## � Version Mapping

OpenSSL uses a versioning scheme that includes letters (e.g., `1.1.1n`), but NuGet Package Manager only accepts numeric versions in SemVer format (`major.minor.patch[.build]`). This package uses the following conversion:

| OpenSSL Version | NuGet Version | Description |
|----------------|---------------|-------------|
| `1.1.1n` | `1.1.1.14` | Where `n` represents the 14th letter of the alphabet |

### Version Format Rules
- OpenSSL letter suffixes are converted to numeric equivalents
- `a` = `1`, `b` = `2`, ..., `n` = `14`, etc.
- This ensures compatibility with NuGet's SemVer requirements

### Creating the Package
To create the NuGet package locally:

```bash
# Navigate to project directory
cd openssl-vcpkg-nuget

# Create the package
nuget pack openssl.vcpkg.nuspec -OutputDirectory out

# Output: openssl.vcpkg.1.1.1.14.nupkg
```

## �🛠️ Build Process

This project uses vcpkg to compile OpenSSL:

```bash
# vcpkg setup
vcpkg install openssl:x64-windows

# NuGet package is automatically created via GitHub Actions
```

## 📋 vcpkg Configuration

The project includes:
- `vcpkg.json` - Specifies dependencies
- `vcpkg-configuration.json` - Registry configuration
- Updated baseline to the latest vcpkg version

## 🤝 Contributing

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🔗 Useful Links

- [OpenSSL Official Website](https://www.openssl.org/)
- [OpenSSL Documentation](https://www.openssl.org/docs/)
- [vcpkg Repository](https://github.com/microsoft/vcpkg)
- [NuGet Package](https://www.nuget.org/packages/openssl.vcpkg/)

## 📞 Support

If you encounter issues or have questions:
- Open an [Issue](https://github.com/darioajr/openssl-vcpkg-nuget/issues)
- Check the [OpenSSL documentation](https://www.openssl.org/docs/)

## 📊 Build Status

The package is automatically built using GitHub Actions whenever there are changes to the repository. The current build status can be checked in the badge at the top of this README.

---

⭐ **If this project was useful to you, consider giving it a star!**