#openssl
<center>[Home](../index.html)</center>

[TOC]

##Encrypt and decrypt files

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

***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a></center>

