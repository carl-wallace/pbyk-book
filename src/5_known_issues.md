# Known Issues

## General
- NIPR and O&M NIPR builds are not presently supported owing to lack of support for BER decoding in the `cms` crate used by `pbyk` and the current NIPR CA's usage of BER encoding when returning CA certificates during SCEP processing.  The next NIPR CA update should enable these features to be used.
- GUI support is not presently provided for Linux

## GUI mode
- Copy and Paste does not work on macOS (see [Dioxus issue 1691](https://github.com/DioxusLabs/dioxus/issues/1691))
- Console window may remain visible when run in GUI mode except on Windows
- State information is only saved when an action is performed, not when app is closed
- YubiKey reset capability is not available on macOS on x86_64 hardware

## Windows
- When the VSC feature is used, the app takes several seconds to close
- On Windows 11, elevated permissions are required to generate attestations. On Windows 10, attestations are available without elevated permissions. On Windows 11, use of elevated permissions (or not) should remain constant throughout enrollment. For example, enrolling with elevation then performing UKM without will not work. A device must be deleted on the portal to remove attestation expectation once it has been established.
- The VSC state information maintained in the .pbyk folder in the user's home directory will grow without bound across multiple reset generations. The file can be manually deleted when a VSC is destroyed and recreated as a mitigation.
