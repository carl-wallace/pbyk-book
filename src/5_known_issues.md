# Known Issues

## General
- NIPR and O&M NIPR builds are not presently supported owing to lack of support for BER decoding in the `cms` crate and the current NIPR CA's usage of BER encoding when returing CA certificates during SCEP processing
- GUI support is not presently provided for Linux

## GUI mode
- Presence of multiple YubiKeys is not supported
- Copy and Paste does not work on MacOS (see [Dioxus issue 1691](https://github.com/DioxusLabs/dioxus/issues/1691))
- Console window from which app is launched in GUI mode is always hidden on Windows (this may not be desired when launching from a command prompt)
- State information is only saved when an action is performed, not when app is closed
- YubiKey reset capability is not available on MacOS on x86_64 hardware
