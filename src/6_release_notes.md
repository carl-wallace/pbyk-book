# Release Notes

## v0.4.1

* Changes some language displayed to users when provisioning a YubiKey that has not been configured with the expected management key. 

## v0.4.0

* Adds support for YubiKeys that use AES management keys
* Adds support for larger RSA key sizes on YubiKeys that support larger RSA key sizes. For devices that support larger RSA key sizes, a 3072-bit RSA key is generated during pre-enrollment (instead of the default 2048-bit key). During enrollment and user key management, key sizes are dictated by the payloads supplied by the Purebred portal. If a device does not support a requested key size, a 2048-bit key is generated instead. Recovery operations that attempt to install an RSA key larger than the target YubiKey supports will fail.
* Removes prohibition on using "nipr" and "om_nipr" features
* Update Rust edition and version
* Align with pre-release versions of PKI-related crates, i.e., x509-cert, certval, etc.
* Use updated PKI artifacts from pb_pki
* Copy and paste functionality now works in GUI mode on macOS
* YubiKey reset capability is now available on macOS on x86_64 hardware

## v0.3.0

* Added support for VSCs

## v0.2.0

* Added GUI

## v0.1.0

* Command line only app release