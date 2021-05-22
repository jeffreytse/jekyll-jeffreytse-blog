---
layout: post
title: Hash Algorithms
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - cryptography
  - note
---

## MD-family

The MD family of hashing algorithms were designed by Ron Rivest during the
late 1980’s and early 1990’s. MD actually stands for "Message Digest".

### MD2

It was optimized to run on 8-bit computers and generates a 128-bit hash
value the hashes are generally displayed as hexadecimal string which is
32 characters long. This hash exhibits features of the avalanche effect,
and so even a very small change in the text string will result in a very
different hexadecimal string being created.

### MD4

It was developed by Ronald Rivest in 1990. The digest length is 128 bits.
The algorithm has influenced later designs, such as the MD5, SHA-1 and
RIPEMD algorithms. The first full collision attack against MD4 was
published in 1995 and several newer attacks have been published since
then and it has been severely compromised.

### MD5

It was developed in 1991 and it replaced the earlier hash function MD4 due
to believed weaknesses in this algorithm. 1996 was a very damaging year to
MD5 however, a flaw was discovered in its design. The size of the hash is
128 bits, and so is small enough to allow a birthday attack. Once considered
really safe, now completely broken.

## SHA-family

The SHA series of algorithms stand for “Secure Hash Algorithm” they were
developed by NIST. Due to the avalanche effect even a small change in the
data to be encrypted will probably result in a very different hash string.
Because the SHA algorithms show signs of the avalanche effect they are
believed to have quite a good randomization feature. SHA algorithms were
based upon the MD4&5 algorithms developed by Ron Rivest. SHA was released
by the national security authority as a US government standard.

### SHA0

It was published in 1993 and officially known as SHA, it was the first
incarnation of the secure hashing algorithm. This first version was
withdrawn soon after release due to weaknesses in the design. SHA-1 was
released a couple of years later that fixed these problems.

### SHA1

It was published in 1994 and developed by NIST, it has been compromised
in 2005, but its real “death” occurred in 2010, Xiaoyun Wang managed to
break the popular hashes, which is now unsafe. SHA-1 is similar to MD4
and MD5 hashing algorithms, and due to the fact that it is slightly more
secure than MD4 & MD5 it is considered as MD5’s successor, but it's also
slower than MD5. It produces a 160-bit (20-byte) hash value. It’s typically
rendered as a 40 digits long hexadecimal number.

### SHA2

It shares the same structure and mathematical operations as its predecessor
(SHA-1)someday maybe will be unsafe also. Its family has six hash functions
with digests as below.

- SHA224
- SHA256 (32-byte words)
- SHA384
- SHA512 (64-byte words)
- SHA512/224
- SHA512/256

### SHA3

A hash function formerly called [Keccak](https://www.wikiwand.com/en/SHA-3),
chosen in 2012 after a public competition among non-NSA designers. It
supports the same hash lengths as SHA-2, and its internal structure differs
significantly from the rest of the SHA family.

## HAVAL

HAVAL is another popular hash function, it differs from many other hash
functions because it is possible for it to generate hash values in different
lengths, the lengths of the hashes can be 128 bits, 160 bits, 192 bits,
224 bits or 245 bits. HAVAL was designed in 1992. This hashing function
exhibits the avalanche effect and so even a small change in the string is
likely to result in a very different hash value. Recent research, mostly
by Xiaoyun Wang has indicated that HAVAL has a number of weaknesses, perhaps
putting the use of it on hold.

## RIPEMD

RIPEMD was developed by a European consortium, and was designed as an
extension of the original RIPEMD hash function.

- RIPEMD-160
- RIPEMD-320

## Whirlpool

Whirlpool is a cryptographic hash function designed by Vincent Rijmen and
Paulo S. L. M. Barreto, who first described it in 2000. Whirlpool is based
on a substantially modified version of the Advanced Encryption Standard (AES).
Whirlpool produces a hash digest of 512 bits (64 bytes).

## References

- [Hashing Algorithms](https://blog.jscrambler.com/hashing-algorithms)
- [What is the strongest hash algorithm?](https://www.streetdirectory.com/etoday/what-is-the-strongest-hash-algorithm-ejcluw.html)
- [Secure Hash Algorithms](https://www.wikiwand.com/en/Secure_Hash_Algorithms)
