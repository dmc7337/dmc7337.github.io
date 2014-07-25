---
layout: post
title: "Code signing for iOS"
description: "Describes the code signing process for an iOS app."
tags: [iOS, codesign]
comments: true
---
#Overview
This post looks at how code signing has been implemented for iOS apps.
It is intended to provide background for subsequent articles on automating the building and signing of iOS apps.

The post assumes some level of understanding of asymmetric cryptography.
##Code signing - the basic technology
Code signing generates a hash of a file using a private key. The file and the publlic key are distributed together allowing the reveiver to verify:
1. That the file came form the owner of the public key
2. That the file has not been modified since it was signed.

The public key is usually distributed in a certificate which may be a separate file or more usually embedded within the file that was signed.
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
however this keychain must also be in the keychain search list. If the --keychain argument is used, identity is only looked-for in the specific keychain given. This is meant to help disambiguate references to identities[^1].




#References
[^1]: codesign [man page](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/codesign.1.html)
