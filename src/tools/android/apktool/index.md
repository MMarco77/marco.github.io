# Android Apktool for Reverse Engineering

A tool for reverse engineering 3rd party, closed, binary Android apps. It can decode resources to nearly original form and rebuild them after making some modifications. It also makes working with an app easier because of the project like file structure and automation of some repetitive tasks like building apk, etc.

It is `NOT` intended for piracy and other non-legal uses. It could be used for localizing, adding some features or support for custom platforms, analyzing applications and much more.

## Download and Documentation

[Official Apktool Website][apktool-url]{target=\_blank}

## APKTool

- Decoding code

```shell
$ apktool d foo.jar
# decodes foo.jar to foo.jar.out folder

$ apktool decode foo.jar
# decodes foo.jar to foo.jar.out folder

$ apktool d bar.apk
# decodes bar.apk to bar folder

$ apktool decode bar.apk
# decodes bar.apk to bar folder

$ apktool d bar.apk -o baz
# decodes bar.apk to baz folder
```

- Building

```shell
$ apktool b foo.jar.out
# builds foo.jar.out folder into foo.jar.out/dist/foo.jar

$ apktool build foo.jar.out
# builds foo.jar.out folder into foo.jar.out/dist/foo.jar

$ apktool b bar
# builds bar folder into bar/dist/bar.apk

$ apktool b .
# builds current directory into ./dist

$ apktool b bar -o new_bar.apk
# builds bar folder into new_bar.apk

$ apktool b bar.apk
# WRONG: brut.androlib.AndrolibException: brut.directory.PathNotExist: apktool.yml
# Must use folder, not apk/jar file
```

## How to Sign APK After Compile

In order to install modified APK on Android device, you need to sign it with a certificate. Android APK won't be signed by default. You need to sign it manually.

Install **apksigner**

```bash
apt install -y apksigner
```

Create certificate at the same folder you've compiled your modified APK

```bash
keytool -genkey -v -keystore keystore.jks -keyalg RSA -keysize 2048 -validity 10000
```

Enter A password (we will need it to singe the APK), enter any data you wish for the certificate information. At the end enter **'y'** at the end to create the certificate.

Now we should have 2 files: your.apk, keystore.jks. The only step left is to singe the APK with new certificate.

```bash
apksigner sign --ks keystore.jks your.apk
```

When installing the APK you will be prompted with a warning of "unknown certificate" just hit Install.

<!-- appendices -->

[apktool-url]: https://ibotpeaches.github.io/Apktool/ 'Apktool Official Website'

<!-- end appendices -->
