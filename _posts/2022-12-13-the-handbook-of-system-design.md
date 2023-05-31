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

## Basic

All design decisions are based on below 4 factors:

- Scalability
- Reliability
- Availability
- Maintainability

Do remember: Everything is a trade-off.

> The right architecture = Coming up potential solutions + Managing trade-offs

About trade-off:

- All architectures start from requirements. When one person maintains several
  microservices, you will go crazy.
- Under the premise of meeting the requirements, the simpler the implementation,
  the better.
- Execution performance and development efficiency are a pair of contradictions
  in software development.
  - Performance issues are troubles after success, while development efficiency
    is a problem that is faced on the first day of the project.
  - Most projects die before they encounter performance problems.
  - The moment the product faces the user, you may only begin to know exactly
    what the user needs, so let’s launch it as soon as possible.
  - The cost of people is always the highest, leave the thinking time to
    yourself, and leave the hard work to the machine.
  - The main problems faced at different stages are different. It is the right
    choice to seek a quick solution to the problem. No application architecture
    is ever the same.
  - Don't optimize prematurely. In actual projects, you can find the most
    time-consuming places to optimize.
- Consistency, sometimes not so important, can be sacrificed in exchange for
  performance.
  - If it is a stateless service, such as a general API service, you don’t need
    to consider CAP. The consistency is generally guaranteed by the later
    storage. For very critical places, you can deal with it according to the
    specific situation.

Approaching a Design Problem:

- Breaking down the problem
- Communicating your ideas
- Assumptions that make sense

## Approaching

Approaching a System Design (Mainly according to the Software Engineering),
there are 4 steps of the framework:

- Understand the problem and establish design scope (10%)
- Propose high-level deign and get buy-in (30%)
- Design deep dive (25%)
- Wrap up (10%)
  - Summarize the design, here we should focus on the parts that are unique to
    the particular situation, and keep this short and sweet.
  - Ask some questions about the company.

### Requirements Analysis/Clarifications

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
    - What's the format of the input data?
    - ...
- Non-functional Requirements (Constraints, restrict the system design through
  different qualities)
  - The more senior the role is, the more important it is for us to demonstrate
    our ability to handle non-functional requirements.
  - Include performance, security, reliability, scalability, maintainability,
    availability, consistency, freshness, accuracy, etc.
    - Focusing on scale and performance
  - Mainly identify **traffic and data handling** constraints at scale.
  - Scale of the system such as requests per second, requests types, data
    written per second, data read per second)
  - Special system requirements such as multi-threading, read or write oriented.
  - Examples
    - High availability
      - 99.999%
    - Consistency
      - Strong consistency
      - Weak consistency
      - Eventual consistency
    - A latency of around 300ms for timeline generation
    - Scale
      - Serves 10 million users
      - 150 million of DAU (Daily Active Users)
    - ...
  - Assumptions (Estimation of important parts, do some rough
    back-of-the-envelope calculation here)
    - Storage
      - How many files would be upload daily?
      - Examples
        - Videos 5MB per video \* 2 = 10MB/day/user
        - Users meta data 1K/user/day
    - Bandwidth
      - Ingress
        - QPS(Queries per second) = 150 millions \* 0.2
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
            - MongoDB
            - Amazon DocumentDB
            - Apache Cassandra (Started by Facebook in 2008)
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
      - A hight-performance block storage for both throughput and transaction-
        intensive workloads at scale
      - Products
        - Amazon Elastic Block Store (EBS)
    - File storage
      - A file system for you to share file data without managing storage
      - Products
        - Amazon Elastic File System (EFS)
    - Object storage
      - A storage for you to store and retrieve any amount of data from anywhere
      - Products
        - Amazon Simple Storage Service (S3)
    - Redundant Disk Arrays (RAID)
  - File systems
    - Google File System (GFS)
    - Hadoop Distributed File System (HDFS)
  - Message queues (Pub/Sub)
    - RabbitMQ
    - Kafka (a messaging system for LinkedIn but has since grown to become a
      popular distributed event streaming platform)
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

### High-Level Design (HLD, known as General Design)

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
- Scale the design (Scale problems)
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
    - Database scaling
      - Database sharding (Scale Database)
        - What type of sharding key are we going to be using?
    - High Concurrency
    - Failure Scenarios
    - Request Rate Limiter
    - Circuit Breaker
- Justify your ideas

### Detail design (LLD, Low Level Design)

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

#### API Design

1. What APIs would we need? It should be clear after gathering the requirements.

Return all bookshops on a user's location.

|          API          | Remark |
| :-------------------: | :----: |
| GET /v1/search/nearby |        |

Bookshop owner can add, delete or update a bookshop.

| API                      | Remark                                       |
| :----------------------- | :------------------------------------------- |
| GET /v1/bookshops/:id    | Return detailed information about a bookshop |
| POST /v1/bookshops       | Add a bookshop                               |
| PUT /v1/bookshops/:id    | Update details of a bookshop                 |
| DELETE /v1/bookshops/:id | Delete a bookshop                            |

2. Define the input parameters and output responses carefully.

Input parameters:

| Field       | Description               | Type   |
| :---------- | :------------------------ | :----- |
| Name        | ABC                       | String |
| Author      | Foo                       | String |
| Description | An interesting story book | String |
| Price       | The book price            | Float  |

Output Response:

```json
{
    "total": 100,
    "books": [
       {
           "name": "ABC",
           "author": "Foo",
           "price": 100.0
       },
       {
           "name": "DFG",
           "author": "Bar",
           "price": 50.0
       },
       ...
    ]
}
```

#### Database Schema Design

To hash out the data model and schema

### Implementation

#### SOLID Design Principles

The SOLID principles were introduced by Robert C. Martin in his 2000 paper "
Design Principles and Design Patterns". These design principles encourage us to
create more maintainable, understandable, and flexible software.

SOLID is an acronym that stands for five key design principles:

- Single Responsibility Principle (SRP)
  - Testing – A class with one responsibility will have far fewer test cases.
  - Lower coupling – Less functionality in a single class will have fewer
    dependencies.
  - Organization – Smaller, well-organized classes are easier to search than
    monolithic ones.
- Open-closed Principle
  - By extending the class, we can be sure that our existing application won't
    be affected.
- Liskov Substitution Principle
  - It states that a subclass should be replaceable by its base class.
  - Because inheritance assumes that subclasses inherit everything from their
    parent class, subclasses can extend behavior but not narrow it down.
    Therefore, when a class violates this principle, it can lead to some nasty
    bugs that are hard to find.
  - For example, a square inherits a rectangle, and the function to calculate
    the area will indirectly violate this principle. Because it violates the
    characteristics of the square, you can change the width and height to be
    unequal.
- Interface Segregation Principle
  - It means interfaces remain separate, A specific interface is better than a
    general-purpose interface. The class shouldn't be forced to implement
    functions they don't need.
- Dependency Inversion Principle
  - Our class should depend on interfaces and abstract classes instead of
    concrete classes and functions.
  - We rely on interfaces rather than concrete classes.

All five are commonly used by software engineers and provide some important
benefits for developers, which also are used to Object-Oriented class design.

#### Performance Optimization

- Utilize resource pools to reduce the cost of creating and recycling reusable
  objects.
  - Common cases:
    - Thread pool
    - Connection pool
- Sequential read and write, reduce random IO, reduce cache miss.
  - The performance of memory sequential read and write is much better than
    random read and write.
  - Disk sequential read and write performance is much better than random read
    and write.
  - Ordered list, a dictionary structure based on ordered arrays.
  - In Java, everything is an object, so in an array, seemingly continuous
    objects are actually discrete in physical memory, so the traversal effect
    will be much worse.
  - For languages such as C, C++ and so on, they all support `struct`. When the
    object is defined as a `struct`, the memory occupied by an array of this
    type is continuous, and the traversal effect will be much better than that
    of Java.
  - Why kafka is faster, because it reads and writes disks sequentially.
- Any large-scale data problem can be settled by splitting
  - Such as batching, framing, paging, time-sharing, slicing, partitioning,
    database sharding.
  - Routing schemes can be simply divided into two categories
    - Non-deterministic routing
      - The same key can be mapped to different computing units for multiple
        routes
      - It's mostly used for distributed systems between stateless nodes
      - Common solutions
        - Round Robin
        - Random
    - Deterministic routing
      - The same key must be mapped to the same computing unit no matter how
        many times it passes through the route
      - It's mostly used for distributed systems between stateful nodes
      - Common solutions
        - Range
        - Hash
        - Configuration table (e.g. MySQL's List in partitioning types)
  - Batching
    - There will be differences in capacity and performance in the IO of
      different components in the system.
    - Read optimization relies on caching, writing optimization relies on
      buffering, and batching ≈ caching + buffering. A cache is a piece of
      memory for reading, and a buffer is a piece of memory for writing.
    - The disadvantage of batching is that the data consistency is poor, whether
      it is caching or buffering, the same problem exists.
    - Batching is one of the most important IO optimization methods whenever IO
      performance bottlenecks are encountered, as it has simple logic, does not
      involve multi-thread concurrency, has no special requirements for data
      structures, and has low system transformation costs.
  - Framing
    - Operations that will take a long time also need to be distributed to
      multiple frames for execution, thereby reducing the waiting time for
      blocking.
    - The single-threaded nature of UI rendering
    - The single-threaded nature of Redis
  - Paging
    - It can be regarded as an alternative framing operation, which can avoid
      the DB loading pressure and network transmission pressure caused by
      one-time data acquisition.
  - Time-sharing
    - It refers to the technology that multiple objects use the same hardware
      in turn, and it is more common in the underlying software that deals with
      hardware.
    - time-sharing operating system
    - time-sharing network
    - I/O multiplexing
  - Slicing
  - Partitioning
    - When only some tables in the database have a large amount of data, use the
      table partitioning in the same database.
  - Database sharding
    - The entire database has a large amount of data and high access pressure,
      use the database sharding
- Separation
  - It's the SRP (Single responsibility principle) of SOLID principle.
  - It can reduce development and maintenance costs while increasing reusability\
    of functional units.
  - Common designs
    - Read-write separation (Separate by functions)
      - In a broad sense, the focus of read-write separation is: the read does
        not care about writing, and the write path does not care about reading.
        Both focus on their own function realization without making any
        sacrifices or concessions for the other.
    - Storage-computing separation (Separate by resources)
      - Cloud Native Database Architecture. In essence, it's Microservice
        Architecture
      - Computing nodes are stateless, storage nodes are non-computing;
        computing nodes scale out, storage nodes scale up.
      - Although the functions were separated, but as the words in The Duck
        Test: If it looks like a duck, swims like a duck, and quacks like a
        duck, then it probably is a duck.
- Reducing
  - Do not optimize prematurely, because in the initial stage of most
    businesses, the amount of data is very small, and performance problems are
    unlikely to occur in any design.
  - Faster realization of business has higher priority than business running
    faster.
  - Reduce the amount of data per processing unit, algorithmically reduced and
    physically reduced.
  - Common solutions
    - Optimizing data structures and algorithms
    - Clipping data
      - Java GC
      - DB Archive
- Concurrency
  - The utilization rate of a single machine can be improved through
    concurrency, and the upper limit of the overall processing capacity can be
    expanded through multi-machine concurrency.
  - The introduction of concurrency will greatly increase the complexity of the
    code and increase the difficulty of maintaining data consistency. It's often
    only used as the ultimate optimization method.

### Testing (Validate the design)

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
