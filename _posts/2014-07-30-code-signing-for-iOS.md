---
layout: post
title: "Code signing for iOS"
description: "Describes the code signing process for an iOS app."
tags: [iOS, codesign]
comments: true
---

## Overview
This post looks at how code signing has been implemented for iOS apps.
It is intended to provide background for subsequent articles on automating the building and signing of iOS apps.

The post assumes some level of understanding of asymmetric cryptography.

## Digital Signatures
From wikipedia [^1]:

A digital signature scheme typically consists of three algorithms:
 * A key generation algorithm that selects a private key uniformly at random from a set of possible private keys. The algorithm outputs the private key and a corresponding public key.
 * A signing algorithm that, given a message and a private key, produces a signature.
 * A signature verifying algorithm that, given a message, public key and a signature, either accepts or rejects the message's claim to authenticity.

A digital signature can be applied to any data and can be embedded with that data or as a separate file.

## Code signing - the basic technology

Code signing uses digital signatures and implements all three of the points above. Typically it will also enforce the code signing so that if the signature cannot be verified then the code is not installed or run.

Code signing can be done with:

 * OpenPGP/GnuPG where typically the signature details are provided as a separate file (.asc or .sig) which can be used to verify the matching package.
 * Java provides keytool to manage keystores and jarsigner to sig and verify jar files
 * Authenticode is the Microsoft implementation used in Windows and the Internet Explorer browser
 * Mach-O code signing used by OS X and iOS

The OS X and iOS code signing use the same codesigning utility to sign but iOS has a more complete verification.

## OS X and iOS code signing
Code for both OS X and iOS are signed using the OS X utilit codesign.
This tool is installed as part of OS X but also with the Xcode tools and some SDKs.
For example with Xcode and the iPhone 7 SDK installed there are three different versions of code sign installed.

* /usr/bin/codesign





### codesign

##Signing identity
To be used for

##Default keychain and keychain search list
To be used for code signing, a digital identity must be stored in a keychain that is on the calling user's keychain search list.
It is important to note that the keychain search list is different to the default keychain. To display the keychain search list run:

`security list-keychains`

With no other keychains configured this will list the login keychain for the current user and a System keychain.
The System keychain is always in the keychain search list.

By default, the default keychain (sorry about that) is the users login keychain. This can be checked by running:

`security default-keychain`

The keychain to look in for the signing identity can be specified as an option to the codesign command,
however this keychain must also be in the keychain search list. If the --keychain argument is used, identity is only looked-for in the specific keychain given. This is meant to help disambiguate references to identities[^2].




#References
[^1]: [Digital signatures](http://en.wikipedia.org/wiki/Digital_signature)

[^2]: [codesign man page](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/codesign.1.html)
