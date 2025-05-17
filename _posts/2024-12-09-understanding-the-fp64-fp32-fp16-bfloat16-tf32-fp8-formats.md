---
layout: post
title: Understanding the FP64, FP32, FP16, BFLOAT16, TF32, FP8 Formats
subtitle: Choosing the Right Format for Speed, Accuracy, and Energy Savings
banner:
  image: https://i.postimg.cc/cHWQSpnw/image.png
  opacity: 0.75
author: Jeffrey Tse
categories: computer
tags:
  - AI
  - ML
  - note
---

## Floating-Point Formats Overview

### FP64 (Double-Precision)

- **Structure**: 1 sign bit, 11 exponent bits, 52 mantissa bits (64 bits total).
- **Precision/Range**: Highest precision and dynamic range.
- **Use Cases**: Scientific computing, simulations, and high-precision calculations.
- **Standards**: IEEE 754.

### FP32 (Single-Precision)

- **Structure**: 1 sign bit, 8 exponent bits, 23 mantissa bits (32 bits total).
- **Precision/Range**: Balanced precision and range.
- **Use Cases**: General-purpose computing, graphics (CUDA/OpenGL), traditional machine learning.
- **Standards**: IEEE 754.

### FP16 (Half-Precision)

- **Structure**: 1 sign bit, 5 exponent bits, 10 mantissa bits (16 bits total).
- **Precision/Range**: Lower precision and range; prone to overflow/underflow.
- **Use Cases**: Memory-constrained environments (mobile/embedded), deep learning inference, mixed-precision training.
- **Standards**: IEEE 754.

### BFLOAT16 (Brain Floating Point)

- **Structure**: 1 sign bit, 8 exponent bits, 7 mantissa bits (16 bits total).
- **Precision/Range**: Matches FP32's dynamic range but with reduced precision.
- **Use Cases**: Deep learning training/inference (Google TPUs, GPUs), replacing FP32/FP16 where range is critical.
- **Standards**: Developed by Google; not IEEE-standardized.

### TF32 (TensorFloat-32)

- **Structure**: 1 sign bit, 8 exponent bits, 10 mantissa bits (19 bits stored in 32-bit containers).
- **Precision/Range**: FP32-like range with FP16-like precision.
- **Use Cases**: Accelerated AI training on NVIDIA Ampere GPUs (Tensor Cores), matrix operations.
- **Standards**: NVIDIA proprietary format.

### FP8 (8-bit Floating Point)

- **Structure** (2 variants):
  - E4M3: 1 sign bit, 4 exponent bits, 3 mantissa bits (8 bits total).
  - E5M2: 1 sign bit, 5 exponent bits, 2 mantissa bits (8 bits total).
- **Precision/Range** (2 variants):
  - E4M3: Higher precision (3 mantissa bits) but limited dynamic range.
  - E5M2: Lower precision (2 mantissa bits) but wider dynamic range (similar to FP16).
- **Use Cases**:
  - Ultra-low-precision AI inference (e.g., edge devices, microcontrollers).
  - Quantization for memory-bound layers in neural networks (weights/activations).
  - Energy-efficient hardware (e.g., NVIDIA Hopper GPUs, Intel AMX).
- **Standards**:
  Emerging format; proposed in IEEE 754-2019 extensions.
  Vendor-specific implementations (NVIDIA, Intel, ARM).

FP8 bridges the gap between floating-point and integer quantization (e.g., INT8)
while maintaining some dynamic range flexibility.

## Key Comparisons

- **Precision**: FP64 > FP32 > TF32 ≈ BFLOAT16 > FP16 > FP8 (E4M3) > FP8 (E5M2).
- **Dynamic Range**: FP64 > FP32 ≈ BFLOAT16 ≈ TF32 > FP16 ≈ FP8 (E5M2) > FP8 (E4M3).
- **Memory Footprint**: FP64 > FP32 > TF32 (32-bit storage) > BFLOAT16 ≈ FP16.

## Hierarchy

| Format   | Bits | Precision | Dynamic Range | Typical Use Case               |
| -------- | ---- | --------- | ------------- | ------------------------------ |
| **FP64** | 64   | Extreme   | Extreme       | Scientific simulations         |
| **FP32** | 32   | High      | High          | General ML training            |
| **TF32** | 19   | Moderate  | High          | NVIDIA GPU matrix math         |
| **BF16** | 16   | Moderate  | High          | DL training (TPUs/GPUs)        |
| **FP16** | 16   | Moderate  | Moderate      | Inference, mixed-precision     |
| **FP8**  | 8    | Low       | Variable      | Edge AI, ultra-low-power chips |

## Applications & Trade-offs

- **Scientific Computing**: FP64 for accuracy in simulations.
- **General ML/Graphics**: FP32 for balance.
- **Edge Devices**: FP16 for efficiency; BFLOAT16 for DL training with better range.
- **Hardware-Specific**: TF32 optimizes NVIDIA GPUs; BFLOAT16 for TPUs.

## Considerations

- **Hardware Support**: Not all formats are universally supported (e.g., TF32 requires Ampere GPUs).
- **Quantization**: Techniques like INT8 reduce precision further for inference speed.
- **Mixed-Precision Training**: Combines FP16/FP32 or BFLOAT16/FP32 to maintain accuracy while improving speed.

## Standards & Development

- **IEEE Standards**: FP64, FP32, FP16.
- **IEEE 754**: FP64, FP32, FP16 are standardized. FP8 is under active development.
- **Vendor-Specific**: BFLOAT16 (Google), TF32 (NVIDIA).

## Summary

Choose a format based on the trade-offs between precision, range, memory, and
computational efficiency. Lower precision (e.g., FP16, BFLOAT16) benefits AI
and edge devices, while higher precision (FP64, FP32) remains vital for
scientific and traditional computing.
