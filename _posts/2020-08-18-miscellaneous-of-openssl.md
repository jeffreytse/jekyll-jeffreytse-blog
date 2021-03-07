---
layout: post
title: Miscellaneous of OpenSSL
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - misc
  - note
---

## Generating RSA key pair

OpenSSL can generate several kinds of public/private keypairs. RSA is the most
common kind of keypair generation.

### Generating an RSA private key

You can generate a 2048-bit RSA private key with the following commands:

```bash
openssl genpkey -algorithm RSA -out rsa_private.pem \
  -pkeyopt rsa_keygen_bits:2048
```

or

```bash
openssl genrsa -out rsa_private.pem 2048
```

Execute this command to make a 2048-bit encrypted private key file.

```bash
openssl genrsa -out rsa_private.pem -aes256 2048
```

To get the supported encryption algorithms with the following commands:

```bash
openssl enc -list
```

Some encryption algorithms as below:

- -aes256
- -aes-256-cbc
- -aria256
- -aria-256-ofb
- ...

### Extracting the public key from an RSA private key

In the RSA algorithm the public key is build using the modulus and the public
exponent, which means that we can always derive the public key from the private
key. OpenSSL can easily do this with the rsa module, producing the public key
in PEM format.

```bash
openssl rsa -in rsa_private.pem -pubout -out rsa_public.pem
```

It is relatively easy to do some cryptographic calculations to calculate the
public key from the prime1 and prime2 values in the public key file.

However, OpenSSL has already pre-calculated the public key and stored it in the
private key file.

So this command doesn't actually do any cryptographic calculation, it merely
copies the public key bytes out of the file and writes the Base64 PEM encoded
version of those bytes into the output public key file.

### Generating RSA key pair with ssh-keygen

Other popular ways of generating RSA public/private key pairs is ssh-keygen.
You can generate 2048-bit RSA key pair with the following commands:

```bash
ssh-keygen -b 2048 -t rsa
```

### Generating an RSA key with a self-signed X.509 certificate

To generate a 2048-bit RSA private key and a self-signed X.509 certificate with
a SHA-256 signature, run the following command:

```bash
openssl req -x509 -nodes -newkey rsa:2048 -keyout rsa_private.pem \
    -out rsa_cert.pem -subj "/CN=unused"
```

## Viewing the key elements

This format is called PEM (Privacy-Enhanced Email). The private key is encoded
as a big blob of Base64 text.

To parse it, you need to use the "rsa" command:

```bash
openssl rsa -text -in rsa_private.pem

```

or

```bash
openssl rsa -text < rsa_private.pem
```

or use the "asn1parse" command:

```bash
openssl asn1parse -inform pem -in rsa_private.pem
```

or for PKCS8 format:

```bash
openssl asn1parse -inform pem -in rsa_private.pem -strparse 22
```

Note that the ASN.1 structure contains the type of the object (rsaEncryption,
in this case). You can further decode the `OCTET STRING` field, which is the
actual key, specifying the offset 22.

While the `asn1parse` module is a generic ASN.1 parser, the `rsa` module knows the
structure of an RSA key and can properly output the field names.

## Key File Encoding

Key data may be encoded in three general ways:

### Binary DER-encoded format

This is sometimes called ASN.1 BER-encoded (there is a subtle difference between
BER- and DER-encodings: DER is just a stricter subset of BER, but consider them
the same here). The most compact form. If you try to view the file with a text
editor it is full of "funny" characters. The first byte in the file should be a
'0' character (U+0030).

### PEM or base64 format

It is the same data as the DER-encoded file but it is encoded in base64 with
additional header and footer lines ([RFC 7518](https://www.ietf.org/rfc/rfc7468.txt), Textual Encodings of PKIX, PKCS, and CMS Structures):

```txt
-----BEGIN LABEL-----
MIICLDCCAdKgAwIBAgIBADAKBggqhkjOPQQDAjB9MQswCQYDVQQGEwJCRTEPMA0G
A1UEChMGR251VExTMSUwIwYDVQQLExxHbnVUTFMgY2VydGlmaWNhdGUgYXV0aG9y
aXR5MQ8wDQYDVQQIEwZMZXV2ZW4xJTAjBgNVBAMTHEdudVRMUyBjZXJ0aWZpY2F0
...
-----END LABEL-----
```

The PEM format is used to store cryptographic keys the body of the content
is in a format called PKCS #8. Initially a standard created by a private company
(RSA Laboratories), it became a de facto standard so has been described in
various RFCs, most notably [RFC 5208](https://www.ietf.org/rfc/rfc5208.txt),
Public-Key Cryptography Standards (PKCS) #8: Private-Key Information Syntax
Specification Version 1.2.

The PKCS#8 format describes the content using the [ASN.1](https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One)
(Abstract Syntax Notation One) description language and the relative DER
(Distinguished Encoding Rules) to serialize the resulting structure. This
means that Base64-decoding the content will return some binary content
that can be processed only by an ASN.1 parser.

Let's visually recap the structure:

```txt
-----BEGIN label-----
+--------------------------- Base64 ---------------------------+
|                                                              |
| PKCS#8 content:                                              |
| ASN.1 language serialized with DER                           |
|                                                              |
+--------------------------------------------------------------+
-----END label-----
```

Please note that, due to the structure of the underlying ASN.1 structure, every
PEM body starts with the MII characters.

The first version of the PKCS standard (PKCS#1) was specifically tailored to
contain an RSA key. Its ASN.1 definition can be found in
[RFC 8017](https://www.ietf.org/rfc/rfc8017.txt), PKCS#1: RSA Cryptography
Specifications Version 2.2.

Subsequently, as the need to describe new types of algorithms increased, the
PKCS#8 standard was developed. This can contain different types of keys, and
defines a specific field for the algorithm identifier. Its ASN.1 definition
can be found in [RFC 5958](https://www.ietf.org/rfc/rfc5958.txt), Asymmetric
Key Packages.

### XML format

There are W3C standards for this, and, er, a .NET way that predates the latest
W3C standard. Here is an example of the W3C
([XKMS](http://www.w3.org/TR/xkms2/)) 2.0 format.

```xml
<RSAKeyPair>
  <Modulus>4IlzOY3Y9fXoh3Y5f06wBbtTg94Pt6vcfcd1KQ0FLm0S36aGJtTSb6pYKfyX7PqCUQ8wgL6xUJ5GRPEsu9
    gyz8ZobwfZsGCsvu40CWoT9fcFBZPfXro1Vtlh/xl/yYHm+Gzqh0Bw76xtLHSfLfpVOrmZdwKmSFKMTvNXOFd0V18=
  </Modulus>
  <Exponent>AQAB</Exponent>
  <P>9tbgIiFMXwpw/yf85bNQap3lD7WFlsZA+qgKtJubDFXCAR35N4KKFMjykw6SzaVmIbk80ga/tFUxydytypgt0Q==</P>
  <Q>6N6wESUJ0gJRAd6K6JhQ9Xd3YaRFk2sIVZZzXfTIWxKTInOLf9Nwf/Wkqrt0/Twiato4kSqGW2wU6K5MnvqOLw==</Q>
  <DP>l0zwh5sXf+4bgxsUtgtqkF+GJ1Hht6B/9eSI41m5+R6b0yl3OCJI1yKxJZi6PVlTt/oeILLIURYjdZNR56vN8Q==</DP>
  <DQ>LPAkW/qgzYUi6tBuT/pszSHTyOTxhERIZHPXKY9+RozsFd7kUbOU5yyZLVVleyTqo2IfPmxNZ0ERO+G+6YMCgw==</DQ>
  <InverseQ>
    WIjZoVA4hGqrA7y730v0nG+4tCol+/bkBS9u4oiJIW9LJZ7Qq1CTyr9AcewhJcV/+wLpIZa4M83ixpXub41fKA==
  </InverseQ>
  <D>pAPDJ0d2NDRspoa1eUkBSy6K0shissfXSAlqi5H3NvJ11ujNFZBgJzFHNWRNlc1nY860n1asLzduHO4Ovygt9DmQb
    zTYbghb1WVq2EHzE9ctOV7+M8v/KeQDCz0Foo+38Y6idjeweVfTLyvehwYifQRmXskbr4saw+yRRKt/IQ==
  </D>
</RSAKeyPair>
```

The .NET version uses <RsaKeyValue> instead, which is strictly only for a public
key.

## Private key format

### RSA_PEM (PKCS#1)

RSAPrivateKey DER SEQUENCE (binary or PEM encoding)

PEM header:

- BEGIN RSA PRIVATE KEY

### RSA_PEM (PKCS#8)

PrivateKeyInfo DER SEQUENCE (binary or PEM encoding)

A PKCS#8 file can be encrypted with a password to protect the private key.
PKCS#8 standard actually has two versions: non-encrypted and encrypted.

PEM header:

- BEGIN PRIVATE KEY (unencrypted)
- BEGIN ENCRYPTED PRIVATE KEY (encrypted)

## Public key format

### RSA_PEM (PKCS#1)

RSAPublicKey DER SEQUENCE (binary or PEM encoding). An RSA public key encoded
in base64. Can be used to verify RS256 signatures in JWT tokens
([RFC 7518](https://www.ietf.org/rfc/rfc7518.txt)).

PEM header:

- BEGIN RSA PUBLIC KEY

If it uses PKCS #1, however, there has to be an external identification of the
algorithm, so the algorithm identification is placed in header and footer.

### RSA_X509_PEM

An RSA_PEM key, encoded in base64, wrapped in an X.509v3 certificate
([RFC 5280](https://www.ietf.org/rfc/rfc5280.txt)).

PEM header:

- BEGIN PUBLIC KEY

### ES256_PEM

The public key for the ECDSA algorithm (using P-256 and SHA-256), encoded in
base64. Can be used to verify JWT tokens with the ES256 algorithm
([RFC 7518](https://www.ietf.org/rfc/rfc7518.txt)). This public key is not
wrapped in a certificate; this keeps the key size small, which is one of
ES256's main advantages.

PEM header:

- BEGIN PUBLIC KEY

### ES256_X509_PEM

An ES256_PEM key, encoded in base64, wrapped in a X.509v3 certificate
([RFC 5280](https://www.ietf.org/rfc/rfc5280.txt)).

PEM header:

- BEGIN CERTIFICATE

## The OpenSSH public key format

The public key saved by ssh-keygen is written in the so-called SSH-format,
which is not a standard in the cryptography world. It's structure is
`<algorithm> <key> <comment>`, where the `<key>` part of the format is
encoded with Base64.

For example:

```txt
ssh-rsa AAAAB3NzaC1yfasDGdfG...sFASdqYk user@host
```

To manually decode the central part of the key you can run the following code:

```bash
cat key.pub | cut -d " " -f2 | base64 -d | hexdump -ve '/1 "%02x "' -e '2/8 "\n"'
```

The structure of this binary file is pretty simple, and is described in two
different RFCs. [RFC 4253](https://www.ietf.org/rfc/rfc4253.txt), SSH Transport
Layer Protocol, states in section 6.6 that:

```txt
The "ssh-rsa" key format has the following specific encoding:

string    "ssh-rsa"
mpint     e
mpint     n
```

while the definition of the string and mpint types can be found in
[RFC 4251](https://www.ietf.org/rfc/rfc4251.txt), SSH Protocol Architecture,
section 5 that:

```txt
string

    [...] They are stored as a uint32 containing its length
    (number of bytes that follow) and zero (= empty string) or more
    bytes that are the value of the string.  Terminating null
    characters are not used. [...]

mpint

    Represents multiple precision integers in two's complement format,
    stored as a string, 8 bits per byte, MSB first. [...]
```

This means that the above sequence of bytes is interpreted as 4 bytes of length
(32 bits of the uint32 type) followed by that number of bytes of content.

```txt
(4 bytes)   00 00 00 07          = 7
(7 bytes)   73 73 68 2d 72 73 61 = "ssh-rsa" (US-ASCII)
(4 bytes)   00 00 00 03          = 3
(3 bytes)   01 00 01             = 65537 (a common value for the RSA exponent)
(4 bytes)   00 00 01 01          = 257
(257 bytes) 00 b2 .. ca a6 0d    = The key modulus
```

Please note that since we created a key of 2048 bits we should have a modulus of
256 bytes. Instead this key uses 257 bytes prefixing the number with a 00 byte
to avoid it being interpreted as negative (two's complement format).

The structure shown above is the reason why all the RSA public SSH keys start
with the same 12 characters `AAAAB3NzaC1y`. This string, converted in Base64
gives the initial 9 bytes `00 00 00 07 73 73 68 2d 72` (Base64 characters are
not a one-to-one mapping of the source bytes). If the exponent is the standard
65537 the key starts with `AAAAB3NzaC1yc2EAAAADAQAB`, which encoded gives the
fist 18 bytes `00 00 00 07 73 73 68 2d 72 73 61 00 00 00 03 01 00 01`.

## Converting PEM/PKCS#1 to PEM/PKCS#8

To convert it, you need to use the "pkcs8" command:

```bash
openssl pkcs8 -topk8 -inform PEM -outform PEM -in rsa_private.pem \
    -nocrypt > rsa_private.pkcs8.pem
```

## Converting OpenSSH public to PEM/PKCS#8

```bash
ssh-keygen -e -f rsa_public.pub -m PKCS8 > rsa_public.pem
```

## Converting PEM/PKCS#8 to OpenSSH public

```bash
ssh-keygen -i -f rsa_public.pem -m PKCS8 > rsa_public.pub
```

## Key File Extension

- X.509 public key certificates are usually named `.cer` or `.der`
- A textual PEM-format version might be named `.pem` or `.crt`
- Private keys stored using the PKCS#8 convention are conventionally named `.p8`
  or `.p8e`, but you'll also find `.pri`, `.key`, `.bin` and `.pem` being used

## References

- [RSA Key Formats](https://samsclass.info/141/proj/pCH-RKF.htm)
- [RSA Key Formats](https://www.cryptosys.net/pki/rsakeyformats.html)
- [Creating Key pairs](https://cloud.google.com/iot/docs/how-tos/credentials/keys)
- [Cryptography/Generate a keypair using OpenSSL](https://en.wikibooks.org/wiki/Cryptography/Generate_a_keypair_using_OpenSSL#cite_note-5)
- [Public key cryptography: RSA keys](https://www.thedigitalcatonline.com/blog/2018/04/25/rsa-keys/)
