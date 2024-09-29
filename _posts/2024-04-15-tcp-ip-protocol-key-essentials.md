---
layout: post
title: TCP/IP Protocol Key Essentials
subtitle: Understanding TCP/IP protocols and their reliability mechanisms
banner:
  image: https://private-user-images.githubusercontent.com/9413601/431460925-bfc5ab6a-f604-44d9-b2c6-0d63d40fe73a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDQxMjgyMDMsIm5iZiI6MTc0NDEyNzkwMywicGF0aCI6Ii85NDEzNjAxLzQzMTQ2MDkyNS1iZmM1YWI2YS1mNjA0LTQ0ZDktYjJjNi0wZDYzZDQwZmU3M2EucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI1MDQwOCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNTA0MDhUMTU1ODIzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NzcwOWI2ZWQ4M2QzMDlmNDIxYjhmNmQ4NWQ4ZDFjMDJjMDljMDk5ZmNmODkxMzI3MTNjZTQ3YTI0YmM4NjRkMyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.-h1elqPgBwh-o2fpXvY0affWB6F0wmtv1t0pBl6XUIE
  opacity: 0.8
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - programming
  - networking
---

## Introduction

TCP/IP (Transmission Control Protocol/Internet Protocol) is the backbone of
modern networking, enabling reliable communication over the internet. This post
explores the key essentials of TCP/IP protocols, focusing on the three-way
handshake and four-way wavelet processes that ensure reliable data transmission.
TCP/IP is a suite of protocols that govern how data is transmitted over the
internet. It consists of multiple layers, each responsible for different aspects
of communication. The two most important protocols in this suite are TCP and IP.

## Three-Way Handshake

The TCP three-way handshake establishes a reliable connection between two endpoints
(e.g., Client A and Server B) over an unreliable network. It ensures synchronization
of sequence numbers and confirms bidirectional communication readiness.

**Process Flow**

```
1. SYN, seq = x
A -----------------> B
    (Client initiates connection with SYN flag and initial sequence number *x*)

2. SYN-ACK, ACK = x + 1, seq = y
A <----------------- B
    (Server responds with SYN-ACK flag, acknowledges *x+1*, and sends its initial sequence *y*)

3. ACK = y + 1
A -----------------> B
    (Client confirms server's sequence *y+1*; connection established)
```

**Key Purposes**

- **Sequence Synchronization**: Both parties exchange initial sequence numbers
  (_x_ and _y_) to track data order and detect duplicates.
- **Reliability**: Prevents stale/duplicate connections (e.g., delayed SYN packets)
  by requiring explicit ACKs.
- **Why Not Two-Way?** If a delayed SYN packet arrives after a previous connection
  closes, a two-way handshake would allow the server to accept it erroneously.
  The third ACK ensures the client actively validates the connection.

## Four-Way Wavelet

TCP connections are full-duplex; closing requires independent termination of each
direction. The four-way wavelet ensures graceful shutdown without data loss.

**Process Flow**

```
1. FIN, seq = x+3, ACK = y+1
A -----------------> B
    (Client initiates termination with FIN flag, ending its data stream)

2. ACK = x+3
A <----------------- B
    (Server acknowledges client's FIN)

3. FIN, seq = y+1
A <----------------- B
    (Server sends its FIN after finishing data transmission)

4. ACK = y+2
A -----------------> B
    (Client confirms server's FIN; connection fully closed)
```

**Key Reasons**

- **Full-Duplex Closure**: Each party independently signals termination (FIN)
  and acknowledges the other's FIN.
- **TIME_WAIT State**: After sending the final ACK, the client waits for _2MSL_
  (Maximum Segment Lifetime) to handle delayed packets and prevent old data
  from interfering with new connections.

## Technical Mechanisms Supporting Reliability

1. **Sequence & Acknowledgment Numbers**  
   • Track byte order and confirm receipt.
2. **Flow Control**  
   • Sliding window adjusts transmission rates based on receiver buffer capacity.
3. **Error Detection**  
   • Checksums validate header and data integrity; corrupted segments are discarded.
4. **Retransmission**  
   • Unacknowledged packets trigger retransmission after timeout.
5. **Congestion Control**  
   • Algorithms (slow start, fast recovery) prevent network overload.

## Summary

The three-way handshake and four-way wavelet are foundational to TCP's reliability.
By synchronizing sequence numbers, validating bidirectional readiness, and ensuring
graceful closure, TCP mitigates risks in untrusted networks. Combined with mechanisms
like sliding windows and checksums, these processes enable robust data transmission
for applications requiring high integrity.
