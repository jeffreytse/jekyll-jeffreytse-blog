---
layout: post
title: The Handbook of Software Architecture
subtitle: >-
    Not only techniques, but also arts for the minimization
    of manpower in all phases of development.
author: Jeffrey Tse
banner:
  image: https://user-images.githubusercontent.com/9413601/213461408-ffecd351-d963-4d8a-af57-f2d0d8af61b2.png
  opacity: 0.80
categories:
  - computer
tags:
  - software
  - architecture
  - note
---

Nowadays heterogenous systems have been developed and served for us, they
were designed by different architectures, which were practical guidelines
to get better software like maintainable, testable, easy to use, scalable
and many more.

Different architectures are born to solve different, problems, the
architecture is just a framework, we put different business logic and
algorithms into it. This handbook is mainly about the software
architecture, and hope it can get you systematic domain knowledge.

## Software Architecture Development

Main Streaming:

- Monolithic
- Service-Oriented Architecture (SOA)
  - ESB is one of the main technologies to realize SOA
- Microservice

Others:

- Event-driven Architectures (EDA)
  - **Event Producer** -> **Event Router** -> **Event Consumer**
  - Event Router can be Kafka, etc.
- Cloud Native (Utilize cloud services such as EC2, S3, AWS Lambda, etc.)

## Communication between Different Architecture

- SOAP = HTTP + XML
- RESTful = HTTP + JSON
- RPC = SOCKET + CUSTOM

Classic examples:

- CXF is a SOAP/RESTful framework
- Dubbo is a RPC framework
- SpringCloud is a RESTful eco-system

## Distributed System

### Fallacies of Distributed Systems

- Network is Reliable
- Latency is zero
- Bandwidth is infinite
- Topology doesn't change
- Network is secure
- Only one administrator
- Transport cost is zero

### Distributed System Characteristics

- No shared clock
- No shared memory
- Shared resources
- Concurrency and consistency

### Load Balancing

- Client-side load balancing
  - Advantages:
    - No more single point of failure as in the case of the traditional load
      balancer approach.
    - Reduced cost as the need for server-side load balancer goes away.
    - Less network latency as the client can directly invoke the backend
      servers removing an extra hop for the load balancer.
  - Algorithms
    - Round Robin (i = (i + 1) mod n)
    - ...
  - Examples:
    - Netflix Ribbon (Default algorithm is Round Robin)
    - ...
- Server-side load balancing
  - Advantages:
    - Simple client configuration: only need to know the load-balancer address.
    - Clients can be untrusted: all traffic goes through the load-balancer where
      it can be looked at.
    - Clients are not aware of the backend servers.
  - Examples:
    - Nginx
    - AWS ELB
