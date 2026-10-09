# Patched Go SDK for Windows Server 2012, Windows Server 2012 R2 and Windows 8.1

This is a patched Go SDK that allows the Go toolchain to run on legacy Windows versions and allows Go binaries built with the patched SDK to target those systems, including **Windows Server 2012 with rollups**, **Windows Server 2012 R2 with April 2014 Update (KB2919355)**, and **Windows 8.1 with April 2014 Update (KB2919355)**. Only fixed some incompatible code that will break running on these operating systems from [Go](https://github.com/golang/go). This is a strip down version of XTLS/go-win7 .

This SDK is used for building binaries that can run on listed OSes that is not supported officially by Go now. You can use it freely to build binaries targeting these listed OSes from Go.

If you need other pre-built SDK binaries that are not found in Release, you may fork and build it.

## Compatibility

Since Go 1.25, the baseline of the compatibility is:

- Windows Server 2012 with rollups
- Windows 8.1 with April 2014 Update (KB2919355)
- Windows Server 2012 R2 with April 2014 Update (KB2919355)

Updates below are recommended besides the baseline requirements:

- KB2999226 (Windows Server 2012 R2, Windows Server 2012, Windows 8.1): Update for Universal C Runtime in Windows.
- KB3140245 (Windows Server 2012): Providing support for TLS 1.1 and 1.2 in system SChannel, which is used by many system components. You may need to use Easy fix from Microsoft to enable TLS 1.2 support correctly which update several registery keys.
- .NET Framework updates: This enable correct TLS 1.2 support in .NET Framework applications correctly in older OSes.
  - .NET Framework 4.5.1 or 4.5.2 (Windows Server 2012 R2, Windows Server 2012, Windows 8.1): Install at least latest updates for 4.5.1 or 4.5.2 as a baseline.

- **The binary executables compiled by this SDK can run normally on Windows NT 6.2/6.3. This is guaranteed during the maintenance of the project.**

### Testing environment

Testing on legacy Windows versions is performed manually because GitHub Actions does not provide Windows 8.1 hosted runners.

Testing environment:
- Windows 8.1 with April 2014 Update (KB2919355) / Windows Server 2012 R2 with April 2014 Update (KB2919355) (Build 9600.17415) (with no other updates installed)

## Supported version

Current support status: 1.27.x (main), 1.26.x (check)

## Patches applied into the project

### Go 1.25

- Lock SDK to a local one and never download a different one
- Remove PEB hack for long path support (adapted from Microsoft Go)
- Fix `os.RemoveAll` failing on legacy Windows

### Go 1.26

- Lock SDK to a local one and never download a different one (new deployment only)
- Remove PEB hack for long path support (adapted from Microsoft Go)
- Fix `os.RemoveAll` failing on legacy Windows (before 1.26.9)

### Go 1.27

- Lock SDK to a local one and never download a different one (new deployment only)
- Remove PEB hack for long path support (adapted from Microsoft Go)
- Fix PE header locking on minimum Windows NT 10.0
- Fix `os.RemoveAll` failing on legacy Windows (before 1.27.2)
