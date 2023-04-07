---
layout: post
title: The Handbook of Different Authentications for Security
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - software
  - note
---

## Two Factor Authentication

Make your account much more secure with two factor authentication. You will
need a client app that supports the protocol before being able to use this
service. You can find common client applications below.

Client Applications:

- [Google Authenticator for Android](https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2)
- [Google Authenticator for iPhone](https://itunes.apple.com/us/app/google-authenticator/id388497605)
- [Microsoft Authenticator](http://www.windowsphone.com/en-us/store/app/authenticator/e7994dbc-2336-4950-91ba-ca22d653759b)

## One Time Use 2FA Codes

Your one time use 2FA codes can be used as a second factor if for some
reason you do not have access to your normal 2FA application or security
key. These should be stored securely in a safe location.

## Web Authentication (WebAuthn)

WebAuthn is a new W3C global standard for secure authentication on the Web
supported by all leading browsers and platforms. We can make WebAuthn as a
second factor login option.

You can read more about WebAuthn at [yubico.com/webauthn](https://www.yubico.com/webauthn/).

Physical Security Keys:

- Yubico YubiKey
- Google Titan
- SoloKeys

## IP Restriction

Only allow logins from certain IP addresses. You can add IPv4 and IPv6 addresses.
