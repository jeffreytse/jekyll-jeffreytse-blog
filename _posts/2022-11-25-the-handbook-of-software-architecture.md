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

### Basic Theories

#### CAP Theorem

In theoretical computer science, the CAP theorem, also named Brewer's theorem
after computer scientist Eric Brewer, states that any distributed data store
can provide only two of the following three guarantees:

- Consistency
  - Every read receives the most recent write or an error.
- Availability
  - Every request receives a (non-error) response, without the guarantee that
  it contains the most recent write.
- Partition Tolerance
  - The system continues to operate despite an arbitrary number of messages
  being dropped (or delayed) by the network between nodes.

![CAP Theorem](https://user-images.githubusercontent.com/9413601/233882737-6f5cfce3-d5dd-4c6c-8657-af872a5daee9.png)

#### Consensus Algorithm

**Paxos Algorithm**

Paxos is a distributed consensus algorithm. An algorithm that ensures that a
change you make on one object is propagated to all of its replicas over an
asynchronous network, is called a consensus algorithm.

**Raft Algorithm**

Raft is a consensus algorithm designed as an alternative to the Paxos family
of algorithms. It was meant to be more understandable than Paxos by means of
separation of logic, but it is also formally proven safe and offers some
additional features.

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
