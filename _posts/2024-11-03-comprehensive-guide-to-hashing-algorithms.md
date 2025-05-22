---
layout: post
title: Comprehensive Guide to Hashing Algorithms
subtitle: A systematic overview of hashing algorithms, their properties, and applications
author: Jeffrey Tse
categories: computer
tags:
  - programming
  - security
  - note
---

Hashing algorithms are fundamental to modern computing, serving critical roles
in data integrity, cryptography, and efficient data retrieval. This guide
systematically categorizes and compares key hashing algorithms, their
properties, and use cases, drawing insights from authoritative sources.

## 1. Traditional General-Purpose Hashing Algorithms

- **MD5 (Message Digest 5)**
  - **Properties**: Generates a 128-bit hash, fast computation, but vulnerable
    to collision attacks (e.g., Wang Xiaoyun's team demonstrated vulnerabilities).
  - **Use Cases**: Non-security scenarios like file integrity checks (e.g.,
    verifying downloads).
  - **Replacement**: Unsafe even with salting; upgrade to SHA-2/SHA-3 or KDFs.
- **SHA Family**
  - **SHA-1**: 160-bit hash, once widely used but deprecated due to collision
    vulnerabilities (e.g., SHAttered attack in 2017).
  - **SHA-2 (SHA-256/384/512)**: Collision-resistant, used in digital signatures,
    blockchain (e.g., Bitcoin).
  - **SHA-3**: Sponge construction design, superior security to SHA-2 but less
    widely adopted.

---

## 2. Cryptographically Secure Hashing Algorithms

- **BLAKE2**
  - **Properties**: Faster than MD5, supports variable-length output, adopted by
    Argon2.
  - **Applications**: Data integrity checks, password libraries.
- **SM3 (Chinese National Standard)**
  - **Properties**: 256-bit hash, security comparable to SHA-256.
  - **Use Cases**: Government and financial systems requiring localization compliance.
- **RIPEMD-160**
  - **Properties**: 160-bit hash, stronger collision resistance than SHA-1, used
    in Bitcoin address generation.

## 3. Key Derivation Functions (KDFs) & Slow Hashing

- **PBKDF2**
  - **Properties**: Iterative HMAC-based, low memory usage but vulnerable to
    GPU attacks.
  - **Applications**: Legacy systems, Wi-Fi
    password protection.
- **Bcrypt**
  - **Properties**: Built-in salt and cost factor, resistant to rainbow table
    attacks.
  - **Advantages**: Cost-effective for small-to-medium projects.
- **Scrypt**
  - **Properties**: Memory-hard design, increases hardware cracking costs (e.g., Litecoin).
  - **Drawbacks**: Complex parameter tuning, poor performance on low-end devices.
- **Argon2**
  - **Properties**: Winner of the 2015 Password Hashing Competition, resists
    GPU/ASIC attacks via adjustable memory, parallelism, and iterations.
  - **Variants**: ◦ **Argon2d**: GPU-resistant, ideal for cryptocurrencies.
  - **Argon2i**: Side-channel attack-resistant, suited for password storage.
  - **Argon2id**: Hybrid mode, recommended for general use.

## 4. Non-Cryptographic Hashing Algorithms

- **CRC32**
  - **Properties**: 32-bit checksum, ultra-fast but insecure; used in network
    protocols and file validation.
- **MurmurHash**
  - **Properties**: High-speed, uniform distribution; ideal for hash tables and
    caching systems.

## 5. Application Scenarios & Recommendations

| **Scenario**                           | **Recommended Algorithms**           | **Rationale**                                    |
| -------------------------------------- | ------------------------------------ | ------------------------------------------------ |
| High-security password storage         | Argon2 > Scrypt > Bcrypt             | Memory-hard design thwarts hardware attacks.     |
| Legacy web systems                     | Bcrypt                               | Easy integration, built-in salt and cost factor. |
| Blockchain & cryptocurrencies          | SHA-256 (Bitcoin), Scrypt (Litecoin) | Balance of collision resistance and efficiency.  |
| Data integrity checks                  | BLAKE2 > SHA-256                     | High speed with adequate security.               |
| Localized systems (China)              | SM3                                  | Compliant with national cryptographic standards. |
| Non-security scenarios (e.g., caching) | MurmurHash, CRC32                    | Prioritize performance over security.            |

## **Summary**

- **Deprecated Algorithms**: MD5 and SHA-1 are obsolete for security-critical
  tasks; migrate to SHA-2/SHA-3 or KDFs.
- **Trends**: Argon2 is emerging as the gold standard for password storage,
  while Bcrypt remains popular in low-risk contexts.
- **Parameter Tuning**: For KDFs, balance security and performance by adjusting
  parameters (e.g., Argon2 memory ≥64MB).
