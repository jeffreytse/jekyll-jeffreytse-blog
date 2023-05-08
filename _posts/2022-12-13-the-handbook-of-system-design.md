---
layout: post
title: The Handbook of System Design
subtitle: The right architecture = Coming up potential solutions + Managing trade-offs
author: Jeffrey Tse
categories:
  - computer
tags:
  - software
  - architecture
  - note
---

System design is the process of defining the architecture, interfaces, and
data for a system that satisfies specific business requirements. A good system
design requires engineers to think about everything in an infrastructure, from
the hardware/software, down to the data and how it’s stored.

As a senior software engineer, you are demanded a better understanding
of how you solve a particular design problem, how you respond when
there is more than expected traffic on your system, how you design the
database of your system and many more.

All design decisions are based on below 4 factors:

- Scalability
- Reliability
- Availability
- Maintainability

Do remember: Everything is a trade-off.

> The right architecture = Coming up potential solutions + Managing trade-offs

Approaching a Design Problem:

- Breaking down the problem
- Communicating your ideas
- Assumptions that make sense

Approaching a System Design (Mainly according to the Software Engineering):

**1. Requirements Analysis/Clarifications**

Outline the scope of the system, and come out SRS (Software Requirements
Specification). This includes gathering information about the problem space,
performance requirements, scalability needs, and security concerns.

- Background
  - Why do we need to build the system?
  - What kind of problems does the system solve?
  - ...
- Functional Requirements (Use cases, systems exist to solve specific problems)
  - Include business rules, authentication, administrative functions,
    authorization levels, etc.
  - Examples
    - Who is going to use it?
    - How are they going to use it?
    - What does the system do?
    - ...
- Non-functional Requirements (Constraints, restrict the system design through
  different qualities)
  - Include performance, security, reliability, scalability, maintainability,
    availability, etc.
  - Mainly identify **traffic and data handling** constraints at scale.
  - Scale of the system such as requests per second, requests types, data
    written per second, data read per second)
  - Special system requirements such as multi-threading, read or write oriented.
  - Examples
    - High availability
    - Consistency
    - A latency of around 300ms for timeline generation
    - Scale: serves 10 million users
    - ...
  - Assumptions (Estimation of important parts)
    - Storage
      - How many files would be upload daily?
    - Bandwidth
      - Ingress
      - Egress
    - ...
- Data Flows (Data models and data flows between them)
  - Database (Choose database system is also part of this)
    - Relational DB (SQL DB)
      - You’re building the first version of your system and aren’t
        completely sure about the data access patterns
      - You want to maintain zero data redundancy
      - Products
        - Amazon RDS
    - Non-relational DB (NoSQL DB)
      - This is a good option if your data model has no fixed schema
      - Types
        - Key-value DB
          - Products
            - Amazon DynamoDB
        - Document DB
          - Products
            - Amazon DocumentDB
        - Graph DB
          - Graph databases are a good idea when you have many many-to-many
            relationships.
          - Products
            - Amazon Neptune
        - In-memory DB
          - Products
            - Redis
            - Amazon MemoryDB
        - Time-series DB
        - Search DB
    - Trade-off
      - Measures
        - What type of data are we going to be storing?
        - Do we need normalization and joins to reduce data redundancy?
        - ...
      - For choosing SQL
      - For choosing NoSQL
        - Consistency is not as important as availability : Netflix is not a
          banking application so this is a huge factor. ACID is also not as
          important.
        - Normalization is not that complex in systems like Netflix. They're
          not Online Transaction Processing (OLTP) apps like banking apps,
          NoSQL scale immensely with static models that don't change much.
        - If models DO require that rare change -> SQL involves some sort of
          downtime. NoSQL has a distinct advantage here. (This was cited as
          one of the reasons for moving away from SQL)
  - Storage
    - Block storage
    - File storage
    - Object storage
    - Redundant Disk Arrays (RAID)
  - File systems
    - Google File System (GFS)
    - Hadoop Distributed File System (HDFS)
  - Message queues (Pub/Sub)
    - RabbitMQ
    - Kafka
  - ...

Related Tools:

- Data Flow Diagram (DFD)
- Data Dictionary (DD)
- Decision Trees
- Decision Tables
- ...

Related Constraints/Bottleneck:

- The average QPS of a single machine can reach 800-1000.
- The average R/W speed of HDD is 60-80MB/s.
- ...

**2. High-Level Design (HLD, known as General Design) **

Outline a high level architecture design, such as identifying the major system
components, choosing appropriate technology route.

- Sketch the system architecture
  - Fundamentals
    - Architecture Patterns
      - Monolithic Architecture (Traditional)
      - Service-Oriented Architecture (SOA)
      - Micro-services Architecture (MSA)
        - An architectural style that structures an application using loosely
          coupled services
      - Event-driven Architecture (EDA)
      - Cloud Native (Utilize cloud services such as EC2, S3, AWS Lambda, etc.)
    - System Design patterns
      - Bloom filters
      - Consistent hashing
      - Quorum
      - Checksum
      - Merkle trees
      - Leader election
  - Components
    - High cohesion and low coupling for the independence of components
    - Divide by functions
    - Divide by domains
  - Relationship of components
    - Horizontal Relationship
    - Vertical Relationship
- Scale the design
  - Scalability refers to an application’s ability to handle and withstand an
    increased workload without sacrificing latency
  - Identify bottlenecks
    - Types
      - Traffic
      - Data
      - Storage
      - Availability
      - Redundancy
      - Back-up
      - ...
    - Examples
      - Too many user requests
      - The data is too huge
      - Is there a single point of failure in this system? How do we remove it?
      - Do you have enough data replicas to serve the user in case you lose a
        few servers?
      - Do we have enough copies of our services to prevent shutdown?
  - Resolve bottlenecks
    - Caching
      - Types
        - Application Caching
        - Database Caching
        - In-memory Caches
      - Cache invalidation
        - Write-through cache
        - Write-around cache
        - Write-back cache
      - Cache Eviction
        - First in first out (FIFO)
        - Last in first out (LIFO)
        - Least recently used (LRU)
        - Most recently used (MRU)
        - Least frequently used (LFU)
        - Random replacement (RR)
    - Content Delivery Network (CDN)
      - CloudFlare
      - Fastly
    - Load balancing
    - Horizontal scaling (or scaling out)
      - Means adding more machines into your pool of resources.
    - Vertical scaling (or scaling up)
      - Means adding more power (CPU, RAM) to your existing machine, it
        increases the power of the hardware running the application.
    - Database optimization
    - Database sharding (Scale Database)
      - What type of sharding key are we going to be using?
- Justify your ideas

**3. Detail design (LLD, Low Level Design)**

Dive into details for each component, such as interface, algorithm, process,
state transition, etc.

- Define the interface
- Design the data model

Related Tools:

- Program Flow Chart
- N-S Structure Diagram
- Problem Analysis Diagram (PAD)
- ...

With the detailed design done, do remember to keep your design simple, things
will not always go your way, so you may have to come back and make some changes
on the go, as in the real-world, everything is evolving and changing.

**4. Implementation**

**5. Testing (Validate the design)**

Software testing is the process of executing a program in order to find bugs, so
that we can verify whether the software meets various requirements. When writing
a test, consider what types of defects the test needs to catch.

4 stages of V model:

- Unit Testing
- Integration Testing
- System Testing
- Acceptance Testing (Validation Testing)

Others:

- Black-box Testing
  - Also known as functional testing, data-driven testing, or specification-based
    testing.
  - Mainly to test the function of the application.
  - for most software tests, such as integration testing, system testing, etc.
- White-box Testing
  - Also known as glass box testing, structural testing, logic-driven testing
    or testing based on the program itself.
  - Mainly to test the internal structure or operation of the application.
  - For unit testing, integration testing.

The philosophy of testing:

- Unit Testing: To test the smallest independent piece of code to prevent
  regressions.
- Integration Testing: The outside world is a messy place, things usually go
  wrong on the edge, as the place of interaction is usually where the unexpected
  happens.

**Integration testing** and **unit testing** are the cornerstones of robust
software. When considering adding unit testing to existing software, there
are costs and benefits to consider. If your code is working, if the code rarely
needs to be modified, and if the code is not easily unit-testable, then the
benefits of incorporating unit tests may not justify the cost. In these cases,
integration tests can be relied upon to prevent defects in this area.

Testing Pyramid:

![Testing Pyramid](https://user-images.githubusercontent.com/9413601/208030915-5b7dfd23-4d49-4bfd-a5b0-b263a9276345.png)

Key concepts:

- Write tests at different granularities
- The higher the level, the fewer tests you should write

## Conclusion

It’s important to keep in mind that system design is an iterative process, and
the design may change as new information is gathered and requirements evolve.
Additionally, it’s important to communicate the design effectively to all
stakeholders, including developers, users, and stakeholders, to ensure that the
system meets their needs and expectations.

## References

- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [System Design Tutorial](https://www.geeksforgeeks.org/system-design-tutorial/)
- [System Design Cheatsheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
- [The complete guide to System Design in 2023](https://www.educative.io/blog/complete-guide-to-system-design)
- [What are NoSQL Databases](https://aws.amazon.com/nosql/)
