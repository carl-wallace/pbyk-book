# Miscellaneous topics

## Resetting a YubiKey with yubico-piv-tool

The [pbyk reset-yubikey](2_command_line.md#reset) feature performs the equivalent of the following yubico-piv-tool commands
to lock then reset a YubiKey.

```bash
  yubico-piv-tool -a verify-pin -P 32165498
  yubico-piv-tool -a verify-pin -P 32165498
  yubico-piv-tool -a verify-pin -P 32165498
  yubico-piv-tool -a change-puk -P 12345679 -N 32165498
  yubico-piv-tool -a change-puk -P 12345679 -N 32165498
  yubico-piv-tool -a change-puk -P 12345679 -N 32165498
  yubico-piv-tool -a reset
  yubico-piv-tool -a set-chuid
  yubico-piv-tool -a set-ccc
  yubico-piv-tool -a set-mgm-key -n 020203040506070801020304050607080102030405060708
  yubico-piv-tool -a change-puk -P 12345678 -N 12345678
  yubico-piv-tool -a change-pin -P 123456 -N 77777777
```

The reset_yubikey function is intended to perform the equivalent steps.

The caller is assumed to have enforced PIN and PUK requirements. If either the PIN or PUK fails
to satisfy requirements (as described [here](https://docs.yubico.com/yesdk/users-manual/application-piv/pin-puk-mgmt-key.html),
then the attempt to set the PIN or PUK will fail.

## Sample logging configuration

The `pbyk` utility uses the [log4rs](https://crates.io/crates/log4rs) crate for logging support. YAML is used to define 
a logging configuration. See <https://docs.rs/log4rs/latest/log4rs/> for a description of the YAML format. The snip below
provides a sample that outputs `pbyk` and `pbyklib` information at the `debug` level. Several dependencies are listed and
configured at the `error` level. The volume of logging information can be controlled be adjusting the level for the various
components used by `pbyk.`

```yaml
refresh_rate: 30 seconds
appenders:
  stdout:
    kind: console
    encoder:
      pattern: "{d} {l} {t} - {m}{n}"
  pbyk:
    kind: rolling_file
    path: "./pbyk.log"
    encoder:
      pattern: "{d} {l} {t} - {m}{n}"
    # The policy which handles rotation of the log file. Required.
    policy:
      # Identifies which policy is to be used. If no kind is specified, it will
      # default to "compound".
      kind: compound

      # The remainder of the configuration is passed along to the policy's
      # deserializer, and will vary based on the kind of policy.
      trigger:
        kind: size
        limit: 100 mb

      roller:
        kind: delete      
root:
  appenders:
    - pbyk
    - stdout
loggers:
  # turn dependencies on at desired level to see additional log output
  reqwest:
    level: error
  rustls:
    level: error
  certval:
    level: error
  yubikey:
    level: error
  pbyklib:
    level: debug
  pbyk:
    level: debug
```

## Source code

The `pbyk` utility is written in the Rust programming language. The source code for the application is available
[here](https://github.com/carl-wallace/pbyk).

## Additional resources

Additional information on the Purebred process can be found on the [DoD Cyber Exchange site](https://public.cyber.mil/pki-pke/purebred/). 
Contact information for various support resources can be found [here](https://public.cyber.mil/pki-pke/help/).