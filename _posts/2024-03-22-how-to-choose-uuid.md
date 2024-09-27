---
layout: post
title: How to choose UUID
subtitle: A brief comparison of UUID v4, v5, and v7
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - programming
  - note
---

UUIDs (Universally Unique Identifiers) are standardized 128-bit identifiers used
to uniquely identify information in computer systems. Here’s a brief comparison
of UUID v4, v5, and v7:

### UUID v4

- **Random-based**: UUID v4 is generated using random numbers.
- **Uniqueness**: High probability of uniqueness due to randomness.
- **Use case**: Suitable for most general-purpose applications where uniqueness
  is required without a need for determinism.
- **Example**: `550e8400-e29b-41d4-a716-446655440000`

### UUID v5

- **Name-based (SHA-1)**: UUID v5 is generated using a namespace identifier and
  a name, hashed with SHA-1.
- **Deterministic**: The same namespace and name will always produce the same UUID.
- **Use case**: Useful when you need to generate the same UUID for the same
  input (e.g., generating UUIDs from URLs).
- **Example**: `3c4e2b84-6414-5b6b-8a2b-4d6e1e4b6c8a`

### UUID v7

- **Time-ordered**: UUID v7 is a new proposed standard that combines a timestamp
  with random bits.
- **Uniqueness and ordering**: Provides both uniqueness and time-ordering, making
  it useful for distributed systems where order matters.
- **Use case**: Suitable for scenarios where you need unique identifiers that can
  also be sorted chronologically.
- **Example**: Not yet standardized, but would look similar to other UUIDs with
  a time-based component.

### Summary

- **v4**: Random, high uniqueness, general-purpose.
- **v5**: Deterministic, name-based, useful for consistent UUIDs from the same input.
- **v7**: Time-ordered, combines uniqueness with chronological sorting, useful for
  distributed systems.

Choose the version based on your specific requirements for uniqueness, determinism,
and ordering.
