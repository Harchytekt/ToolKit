# Security
<center>[Home](../index.html)</center>

[TOC]

## Encrypt and decrypt files _(OpenSSL)_

### Encryption

```bash
openssl enc -aes-256-cbc -e -in fileToEncrypt -out encryptedFile
```

> The password will be ask twice for safety.

### Decryption

```bash
openssl enc -aes-256-cbc -d -in encryptedFile -out fileToEncrypt
```

> The password will be ask.


## Set a Firmware Password _(OS X 10.9 or higher)_

### What is a Firmware Password and why use one ?

A firmware password offers an advanced level of protection : it is a lower level layer of security that is set on the actual Mac logicboards firmware, rather than at the software layer like **_FileVault_** encryption or the standard login password.  

The result of setting an firmware password is that your Mac can't be booted from an external boot volume, single user mode, or target disk mode, and it also prevents resetting of PRAM and the ability to boot into Safe Mode _(e.g. to reset an user password)_, without logging in through the firmware password first.
This effectively prevents a wide variety of methods that could potentially be used to compromise a Mac.

### Setting the Firmware Password

Setting a firmware password is rather simple :

1. Reboot the Mac, and hold down **Command(⌘)-R** to boot into _Recovery Mode_.
2. On the menu bar of the utilities window, choose **Utilities > Firmware Password Utility**.
3. Click **Turn on Firmware Password…**
4. Enter your Firmware Password in the provided fields, and click **Set Password**.  
⚠️ **Do not forget your password**, you'd have to take an appointment with an Apple Store. ⚠️
5. Now, quit the _Firmware Password Utility_, then choose **Apple() menu > Restart**.

### When and where will it appear ?

On regular restart or boot of your Mac, nothing will change.
It's only when attempting to boot from alternate methods that you'll have to enter it.

You're using one of these methods when you attempt to boot from an _Mac OS X installer drive_, an _external boot volume_, _Recovery Mode_, _Single User Mode_, _Verbose Mode_, _Target Disk Mode_, _resetting the PRAM_, or any other alternative booting approach.

![Firmware Password Screen](../img/UNIX/macOS/firmwarePasswordScreen.jpg "The Firmware Password Screen")

As you can see, there are no hints or details provided on the screen.

An incorrect firmware password does nothing and offers no indication of login failure except that the Mac won't boot.

## Additional source
* [support.apple.com](https://support.apple.com/en-us/HT204455)



***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a></center>

