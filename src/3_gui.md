# Using pbyk as a desktop application

The features provided by `pbyk` will vary with how the utility was built. Some builds may target different environments.
Some may provide only a command-line interface, while others provide a graphical user interface (GUI) and
a command line interface. This chapter addresses usage via the GUI.

## Purebred Workflow

The Purebred workflow consists of four steps: [pre-enroll](#pre-enroll), [enroll](#enroll), [user key management](#user-key-management)
and [recovery](#recover). When enrolling a YubiKey, these steps are preceded by a device [reset](#reset) operation.

The following sections demonstrate enrolling a YubiKey device with the serial number 15995762 with the cooperation of a
Purebred Agent whose EDIPI is 5533442211. 

### Reset

The reset feature can be accessed in one of two ways depending on the state of the device. For devices that have not
been enrolled with Purebred previously, and thus have a different management key installed, simply launching the pbyk app
will display an alert like the one shown below.

<div align="center">
    <img src="screenshots/reset_alert.png">
</div>

For devices that have been enrolled with Purebred previously, launching the app then clicking the DISA logo five times
within five seconds will display the same alert.

When the 'Yes' button is clicked, the app will display a form like the one shown below, which can be used to complete
the reset process.

<div align="center">
    <img src="screenshots/reset.png">
</div>

### Pre-enroll

The next two steps require Purebred Agent participation. The agent should provide their EDIPI and a 
Pre-enrollment OTP. Pre-enrollment must be completed within three minutes of generating the Pre-enrollment OTP. To complete
Pre-enrollment, provide the requested information as shown in the screenshot below then click the Pre-enroll button. In this example,
the YubiKey with serial number 15995762 is being enrolled in the Development environment with the assistance of a Purebred Agent
whose EDIPI is 5533442211.

<div align="center">
    <img src="screenshots/pre_enroll.png">
</div>

The YubiKey Serial Number field is a drop list and will feature multiple options when multiple YubiKeys are available.
When a different device is changed, the form displayed by the app may change to match the state of the newly selected device.

### Enroll

Next, the Purebred Agent will affirm the hash value displayed following pre-enrollment to establish trust in the device and will provide an Enrollment OTP.
As with Pre-enrollment, the Enrollment operation must be completed within three minutes of generating the Enrollment OTP.

<div align="center">
    <img src="screenshots/enroll.png">
</div>

The YubiKey Serial Number field is a read-only text box and will feature the value selected on the Pre-enroll view.

### User key management

Provisioning user keys does not require Purebred Agent co-operation but does require a UKM OTP. To generate a UKM OTP, 
browse to the My Devices tab on the Purebred portal and click the `Generate OTP` link for the target device to obtain a 
UKM OTP for your device. Provide the value to `pbyk` as shown below. The UKM process must be completed within three minutes of
generating the OTP value.

<div align="center">
    <img src="screenshots/ukm.png">
</div>

The YubiKey Serial Number field is a drop list and will feature multiple options when multiple YubiKeys are available.
When a different device is changed, the form displayed by the app may change to match the state of the newly selected device.

### Recover

The Recover operation is optional and follows the same steps as described for UKM. After obtaining a UKM OTP complete
the Recover operation as shown below taking care to clcik the `Recover Old Decryption Keys` checkbox before clicking the
`User Key Management` button. The recovery process must be completed within three minutes of generating the OTP value.

<div align="center">
    <img src="screenshots/recover.png">
</div>

The YubiKey Serial Number field is a drop list and will feature multiple options when multiple YubiKeys are available.
When a different device is changed, the form displayed by the app may change to match the state of the newly selected device.

## Using command-line interface

In some cases, using the command-line interface may be more convenient even when a GUI is available. To exercise the 
command-line interface using a `pbyk` instance that provides a GUI simply add `--interactive` when launching the application
along with other appropriate arguments. The following shows the commands given in the [command line](2_command_line.md) chapter with the 
additional argument.

```bash
$ ./pbyk -iy
Name: Yubico YubiKey OTP+FIDO+CCID; Serial: 15995762
$ ./pbyk -s 15995762 -ir
Starting reset of YubiKey with serial number 15995762. Use Ctrl+C to cancel.
Enter new PIN; PINs must contain 6 to 8 ASCII characters: 
Re-enter new PIN: 
Enter new PIN Unlock Key (PUK); PUKs must be 6 to 8 bytes in length: 
Re-enter new PIN Unlock Key (PUK): 
$ ./pbyk -s 15995762 -a 5533442211 -e dev -i1 22735141
Enter PIN for YubiKey with serial number 15995762: 
Pre-enroll completed successfully: BF8FD6C91095CC4B02925EE299D3FD6A57F3F965
$ ./pbyk -s 15995762 -a 5533442211 -e dev -i -2 93638350
Enter PIN for YubiKey with serial number 15995762: 
Enroll completed successfully
$ ./pbyk -s 15995762 -e dev -i -3 19475568
Enter PIN for YubiKey with serial number 15995762: 
UKM completed successfully
$ ./pbyk -s 15995762 -e dev -i -4 41537238
Enter PIN for YubiKey with serial number 15995762: 
Recover completed successfully
```