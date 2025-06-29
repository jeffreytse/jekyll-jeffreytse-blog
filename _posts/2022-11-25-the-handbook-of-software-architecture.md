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
  - If an old monolithic application wants to move forward and expand, there is
    another cost-effective way, which is the modular monolith. It first divides
    the single application itself into modules and establishes boundaries, which
    can not only reduce the burden on new engineers to understand business
    knowledge, but also reuse the existing architecture.
- Service-Oriented Architecture (SOA)
  - ESB is one of the main technologies to realize SOA
- Microservice
  - Microservice is an implementation methodology to implement SOA.
  - Design Patterns
    - Decomposition Design Patterns
      - Decompose by Business Capability
      - Decompose by Subdomain
      - Decompose by Strangler
    - Integration Design Patterns
      - API Gateway
      - Aggregator
      - Proxy
      - Client Side UI Composition
      - Chain Of Responsibilities
      - Branch
    - Database Design Patterns
      - Database per Service
      - Shared Database per Service
      - Command Query Responsibility Segregator (CQRS)
      - Saga
      - Asynchronous Messaging
      - Event Sourcing
    - Observability Design Patterns
      - Log Aggregation
      - Performance Metrics
      - Distributed Tracing
      - Health Check
    - Cross Cutting Concern Design Patterns
      - External Configuration
      - Service Discovery
      - Circuit Breaker
      - Blue Green Deployment
        - Blue Environment: The old application running in the production is
          called blue environment.
        - Green Environment: The new services deployed which replicates the
          given part of old application is called the green environment.
  - Categories
    - API Gateway
    - Service Mesh
      - Data Plane
      - Control Plane

Others:

- Event-driven Architectures (EDA)
  - **Event Producer** -> **Event Router** -> **Event Consumer**
  - Event Router can be Kafka, etc.
- Cloud Native (Utilize cloud services such as EC2, S3, AWS Lambda, etc.)

## Communication between Different Architecture

Network protocols, also known as API architecture styles:

- SOAP = HTTP + XML
- RESTful = Resource = HTTP + JSON
- GraphQL
  - It's more difficult to cache as a single point of entry and using HTTP POST
    by default, this prevent the full use of HTTP caching. But it could be
    configured to better leverage HTTP caching
- RPC = SOCKET + CUSTOM
- Websocket
  - Primarily used for two-way communication between a client and server
  - Make the server stateful as it now contains the active connection, and
    therefore more difficult to scale
  - Examples
    - A web document editing service that allows multiple people to edit and
      update a document in real-time via their browsers
- Webhook (Async callback)
  - Primarily used for one-way communication
  - It's event-driven compared with HTTP/RESTful (poll, time-driven)
  - Inherently stateless as they don’t need to keep an open connection, so
    scaling them is far easier
  - Examples
    - A service that regularly publish updates to many different consumers
    - GitHub
      - New Branch
      - Code Push
      - Pull Request
    - Slack
      - New Message
      - @ Mention
      - App Notification
    - Stripe
      - New Payment
      - Payment Dispute
      - New Subscription
- FTP = SOCKET

![Architectural API Patterns](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/a1e47bda-3df2-4356-9c20-a03eea8afcd3)

![API Patterns History](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/80188e2f-2660-47db-9997-b6ce1a4d5585)

Classic examples:

- CXF is a SOAP/RESTful framework
- Dubbo is a RPC framework
- SpringCloud is a RESTful eco-system

Moving from monolithic applications to microservice faces several problems:

- Management of microservices.
- Microservice direct access.
- Load balancing of the microservices themselves.
- Microservices are broken and downgraded.
- Distributed transaction tracing for microservices.
- Microservice log collection and analysis.

## Distributed System

Nowadays, it's already the norm for the ordinary PC-level servers to reach tens
of thousands of TPS on a standalone machine with an average latency of 500ms or
less in distributed systems.

Some problems for Internet business:

- C10K problem (Concurrent 10K connections)
- C1000K problem (Concurrent 1000K connections)

Some ideas for distributed systems for massive data on the Internet:

- Hot/cold separation
- Load balancing
- Parallel scaling
- Parallel Processing
- Split repository and split table
- Service clustering
- Tiered design
  - Access layer
    - Load balancing and flexible route distribution based on various policies
  - Service layer
    - It can be grouped by function
  - Data layer
    - Spread data across different database instances based on rules such as
      business types
  - ...
- Performance expansion approaches
  - Parallel expansion
  - Elastic expansion
  - 3D expansion

### Basic Theories

The transformation of computer systems from centralized to distributed, along
with a series of problems and challenges including distributed networks,
distributed transactions, and distributed data consistency, has also led to the
rapid development of a large number of classic theories, such as ACID, CAP and
BASE, etc.

#### CAP Theorem

In theoretical computer science, the CAP theorem, also named Brewer's theorem
after computer scientist Eric Brewer, states that any distributed data store
can provide only two of the following three guarantees:

- Consistency
  - This refers to strong consistency. All the servers in the system will have
    the same data so users will get the same copy regardless of which server
    answers their request.
- Availability
  - The system will always respond to a request (even if it's not the latest
    data or consistent across the system or just a message saying the system
    isn't working).
- Partition Tolerance
  - The system continues to operate as a whole even if individual servers fail
    or can't be reached.
  - If the system cannot achieve data consistency within the time limit, it
    means that a partition has occurred, and a choice must be made between C and
    A for the current operation.

![CAP Theorem](https://user-images.githubusercontent.com/9413601/233882737-6f5cfce3-d5dd-4c6c-8657-af872a5daee9.png)

The CAP theorem provides a tool to make design choices while building a
distributed system.

Cassandra is an AP system, distributed Redis is AP system, etcd is CP system,
Mongo DB is CP. MySQL is a CA system, but it’s not distributed.

![Some Examples](https://github.com/jeffreytse/jekyll-jeffreytse-blog/assets/9413601/6124bfa7-4ecc-4d38-8014-f403c465f3f2)

Before designing the architecture, do consider whether the business is an AP
model or a CP model.

#### ACID Theorem

Transactions have four properties: atomicity, consistency, isolation, and
persistence. These four properties are commonly referred to as ACID
characteristics. ACID compliance guarantees the validity of data in events of
errors, hardware, or power failures.

- Atomicity
  - All the changes which are part of a single transaction are performed or
    everything is rolled back and none of these changes take effect.
- Consistency
  - It refers to guarantee that all data that is written to the database will
    confirm to defined schema and constraints at the time of saving the data.
  - 2 Categories
    - Transaction Consistency (i.e. ACID)
    - Data Consistency
      - Distributed storage of data is the only reason for consistency
      - In distributed systems, consistency refers to data consistency in
        multi-replica problems.
- Isolation
  - It refers to the ability of a database to isolate data among transactions
    providing an independent view of the data.
  - Thus if multiple transactions are executed concurrently, these should not
    interfere or see intermediate or incorrect data and the result should be the
    same as if they were run sequentially.
  - Isolation levels are configurable in most DBMS, providing control to
    Database Administrators to decide the level of isolation.
  - Most DBMS provides the following levels of Isolation:
    - Serializable
    - Repeatable reads
    - Read committed
    - Read uncommitted
- Durability
  - It refers to the permanent nature of the data that was stored as a part of
    the transaction once it is successful.
  - Once the transaction is complete the subsequent reads should fetch the last
    written data.

#### BASE Theorem

BASE is the result of the trade-off between consistency and availability in CAP.
It comes from the conclusion of the distributed practice of large-scale Internet
systems. It is gradually evolved based on the CAP theorem. Its core idea is that
even if strong consistency cannot be achieved (Strong Consistency), but each
application can use an appropriate method according to its own business
characteristics to make the system achieve eventual consistency.

- Basically Available
  - It means the system is mostly available and every working node responds to
    requests in a reasonable amount of time.
- Soft State
  - It refers that the state of a system might vary over time, even without any
    new input.
- Eventually Consistent
  - It refers to the ability of all nodes of a system to become consistent,
    given enough time.
  - The data across different nodes will reflect the same value.

BASE model isn’t suitable for all types of systems: For example, systems that
require strict consistency, such as financial systems, or real-time data
processing applications, may be unable to tolerate eventual consistency.

The variants of eventual consistency model:

- Causal consistency
  - If process A has communicated to process B that it has updated a data item,
    a subsequent access by process B will return the updated value, and a write
    is guaranteed to supersede the earlier write. Access by process C that has
    no causal relationship to process A is subject to the normal eventual
    consistency rules.
- Read-your-writes consistency
  - This is an important model where process A, after it has updated a data
    item, always accesses the updated value and will never see an older value.
    This is a special case of the causal consistency model.
- Session consistency
  - This is a practical version of the previous model, where a process accesses
    the storage system in the context of a session. As long as the session
    exists, the system guarantees read-your-writes consistency. If the session
    terminates because of a certain failure scenario, a new session needs to be
    created and the guarantees do not overlap the sessions.
- Monotonic read consistency
  - If a process has seen a particular value for the object, any subsequent
    accesses will never return any previous values.
- Monotonic write consistency
  - In this case the system guarantees to serialize the writes by the same
    process. Systems that do not guarantee this level of consistency are
    notoriously hard to program.

In actual practice, these variants are often used in combination to build a
distributed system with eventual consistency.

ACID is a commonly used design concept in traditional databases, pursuing a
strong consistency model. BASE supports large-scale distributed systems, and
proposes to obtain high availability by sacrificing strong consistency. ACID and
BASE represent two diametrically opposed design philosophies. In the scenario of
distributed system design, system components have different requirements for
consistency, so ACID and BASE will be used in combination.

#### Consensus Algorithm

Strong consistency aims to provide a higher level of consistency. Unlike
eventual consistency, strong consistency ensures that all nodes see the same
data without any temporary inconsistencies.

Strong consistency guarantees that every read operation returns the latest write
operation’s result, regardless of the node on which the read operation is
executed. This is typically achieved using consensus algorithms.

**Paxos Algorithm**

Paxos is a distributed consensus algorithm. An algorithm that ensures that a
change you make on one object is propagated to all of its replicas over an
asynchronous network, is called a consensus algorithm.

**Raft Algorithm**

Raft is a consensus algorithm designed as an alternative to the Paxos family
of algorithms. It was meant to be more understandable than Paxos by means of
separation of logic, but it is also formally proven safe and offers some
additional features.

#### Distributed Memberships Algorithm

In distributed systems, failures are the norm rather than the exception. This is
because members (or processes) of a group communicate among themselves over an
unreliable network and members can crash at some point. The purpose of every
Membership Protocol is to provide to each member of a group an updated list with
their peers alive. Most modern systems use this peer-to-peer protocol to
disseminate information to all the members in a network or cluster.

**SWIM membership protocol**

SWIM is the acronym of Scalable Weakly-consistent Infection-style Process Group
Membership Protocol. A membership protocol ensures that each process of a group
updates a local list of non-faulty members of the group. When a new process
joins or leaves the group, every local list has to be updated.

There are four key properties that any membership protocol needs to ensure
efficiency and scalability:

- Strong Completeness
  - Each failure in the system is detected
- Accuracy
  - No mistakes when detecting failures. In real life this is not 100%
    guarantee, so we need to reduce false positives
- Speed of failure detection
  - Time to detect a failure
- Scale
  - The network load is generated and distributed equally between processes

**Gossip Protocol**

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

### Typical Applications

Distributed system is a very broad concept. It must be implemented to solve
practical problems. Different problems have different methods and architectures.

- A type of application based on leader election (e.g. paxos, viewstamp)
  - Zookeeper
  - Chuby
- A type of applications for distributed transactions
  - Distributed database manager
- A type of applications based on weak consistency
  - Cassandra's W, R, N adjustable consistency
- A type of application based on leasing mechanism
  - It is mainly the concept of some distributed locks
- A type of applications based on failure detection
  - Gossip failure detection algorithms
  - Phi failure detection algorithms
  - Simple heartbeat
- A type of applications based on weak consistency, causal consistency, and
  sequential consistency
- A type of applications based on asynchronous decoupling
  - Various types of queues

## Microservice Architecture

The main features of microservice architecture:

- Microservices are an architecture in themselves, and each microservice can be
  implemented in a suitable language.
- Each microservice should be as cohesive as possible to avoid external
  transfers and cross-service transactions.

The main components of microservice architecture:

### Service Discovery

Types:

- Server-side Discovery
- Client-side Discovery

Products:

- ZooKeeper
  - ZK satisfies the CP principle. ZK must contain a master-slave
    relationship, one master and many slaves. When the cluster has no master,
    it does not provide external services
  - ZK adopts the pub/sub mode. When ZK is started for the first time, it
    subscribes to the service information it needs and caches it locally
- HashiCorp Consul
- Spring Cloud Consul
  - Service governance component based on Hashicorp Consul
- Netflix Eureka
  - Eureka satisfies the AP principle. All nodes in the Eureka cluster are
    equal and there is no master-slave relationship, so data inconsistency
    may occur.
  - Eureka adopts the service active pull strategy, and consumers go to
    pull at a fixed frequency (default 30 seconds) and cache them locally
- SkyDNS
- etcd
- Alibaba Nacos
- Ctripcorp Apollo
- Kubernates

### Service Calling

Protocols:

- protobuf (Based on RPC)
- Triple (Based on HTTP/2)
- Dubbo2
- gRPC
- RESTful (Based on HTTP)
- Thrift (Based on RPC)
- ...

Products:

- OpenFeign
  - HTTP + RESTful
- Dubbo
  - TCP + Custom (Serialization)

### Service Monitoring

We also call it APM (Application Performance Management), which belongs to the
category of ITOM (IT operation and maintenance management).

Products:

- Dubbo Monitoring
- Spring Admin

### API Gateway

Functions:

- Authentication (Front Desk Design)
  - Pros:
    – Easy to iterate on
    – Easy to develop quickly
    – Shortens go-to-market time
  - Cons:
    – Single point of failure
    – Potentially costly
    – Rigid architectural constraints
- Filtering
- QPS Limitation
- Downgrade
- Load Balancing
- Analytics
- Performance Monitoring
- Special Use Cases
  - Grayscale Releases
  - Canary Releases
  - A/B Tests
  - ....

Products:

- Zuul
- Orange
- Kong
- Tyk (GoLang and Open Source)

### Load Balancing

Products:

- Ribbon
- Nginx

### Circuit Breaker

Isolate access to remote services and third-party libraries to prevent cascading
failures.

Common fault tolerance approaches:

- Thread Isolation
- service Fusing

Products:

- Alibaba Sentinel
- Netflix Hystrix
- Resilience4j
- Envoy

### Distributed Configuration

Products:

- Spring Cloud Config
  - By default, Git is used to store configuration, which can support client
    configuration refresh, encryption and decryption operations
- Consul
- Alibaba Nacos
- Ctripcorp Apollo

### Distributed Tracing

The relationship between microservice calls is complex, and it is necessary to
use this type of component for monitoring and troubleshooting.

Goals:

- Performance monitoring
- Full Link Tracking
  - Certain code
  - Certain sql
  - CPU Operation Status
  - Link Operation time-consuming
  - ...

Products:

- Zipkin
- Sky Walking
- Jaeger
- HTrace
- Pinpoint

### Distributed Transactions

Use Cases:

- Distributed ID generator

Solutions:

- AT
- 2PC (Two Phase Commit)
  - Strong consistency
- TCC (Try Confirm Cancel)
  - Eventual consistency
- Saga
  - Advantages
    - Long lived transaction
  - Execution strategies
    - Forward recovery (The premise is that each sub-transaction will eventually succeed.)
    - Backward recovery (Rollback via per-subtransaction compensation mechanism)
  - Transaction Coordination
    - Choreography
    - Orchestration
- XA Specification
- Local-Message-Based Distributed Transactions
- Transactional-Message-Based Distributed Transactions

### Distributed Batch Task

Products:

- Spring Cloud Task

### Distributed Cache

Products:

- Redis
- ETCD

### Distributed Message Queue

A message queue consists of publishers and consumers, and delivers messages to
one or more consumers on first-in-first-out (FIFO).

Products:

- RabbitMQ
  - Based on AMQP, supports to JMS
  - Written by Erlang
  - High stability, high consistency
- Kafka
  - Distributed Message System
  - High throughput
- ActiveMQ
  - Based on JMS
- AmazonSQS
- RocketMQ
  - Based on JMS
  - Alibaba's product, and hosted by Apache Foundation now
- IronMQ
- Pulsar
- Redis
  - Supports to JMS

Because the production and consumption of messages are asynchronous, and only
care about the sending and receiving of messages, without the intrusion of
business logic, the decoupling of producers and consumers is achieved.

MQ is a message communication model, not a specific implementation. The
mainstream ways to implement MQ are as following:

- AMQP (Advanced Message Queuing Protocol)
  - Basic
    - Just a protocol of data exchange
    - No limit in programming languages, and has various kinds of message models
  - Concepts
    - Producer
    - Consumer
    - vHost
    - Channel
    - Broker
      - Durability
        - Location
          - Disk
          - RAM
        - Types
          - Exchange
          - Queue
          - Message
      - Components
        - Exchange
          - Direct (Routing, by default)
          - Fanout (Publish/Subscribe)
          - Headers
          - Topic
          - Dead Letter
        - Queue
- JMS (Java Message Service)
  - Basic
    - Actually refers to JMS API for Java, including create, send and receive
    - Limited in Java, and has only 2 kinds of message models

### Message Bus

The message bus does not guarantee first-in-first-out (FIFO). Subscribers to a
message bus can receive published messages without knowing the publisher. These
modes are also known as pub/sub.

Messages are published to the bus by the sending API, and any receiving API
subscribed to a message of any type will then receive the corresponding message.

Use Cases:

- Used to propagate cluster state changes

Products:

- Microsoft Azure Service Bus
- Oracle Enterprise Service Bus
- RabbitMQ (MassTransit)

### Log Monitoring (Collect and Analyze)

Products:

- ELK Stack
  - Elasticsearch
  - Logstash
  - Kibana
- GrayLog

### Security

Authentication and Authorization Solutions:

- SSO
- Distributed Session
- Client-side Token
  - JWT (JSON Web Tokens)
- Combination of Client-side Token and API Gateway

Products:

- Spring Security
- Apache Shiro

## Microservice Stacks

### Spring Cloud Official

- Dynamic Configuration
  - Spring Cloud Config (SCC)
  - SCC Client/Server
- Service Calling
  - OpenFeign
  - RestTemplate
- API Gateway
  - Spring Cloud Gateway
- Load Balancing
  - Spring Cloud LoadBalancer
- Circuit Breaker
  - Spring Cloud Circuit Breaker
- Service Monitoring
  - Spring Boot Admin
- Distributed Tracing
  - Spring Cloud Sleuth
- Distributed Transactions
  - NA
- Distributed Message
  - Spring Cloud Stream (SCS)
  - SCS RabbitMQ/Kafka
- Message Bus
  - Spring Cloud Bus

### Spring Cloud Netflix

- Dynamic Configuration
  - Netflix Archaius
- Service Discovery
  - Netflix Eureka
- Service Calling
  - Feign
- API Gateway
  - Netflix Zuul
- Load Balancing
  - Netflix Ribbon
- Circuit Breaker(Fault Tolerance)
  - Netflix Hystrix
- Distributed Tracing
  - NA
- Distributed Transactions
  - NA
- Distributed Messages
  - NA
- Message Bus
  - NA

### Spring Cloud Alibaba

- Dynamic Configuration
  - Alibaba Nacos Configuration
- Service Discovery
  - Alibaba Nacos Service Registry
- Service Calling
  - Dubbo RPC
- API Gateway
  - Spring Cloud Gateway (Spring Cloud official support, after Finchley
    version)
  - Dubbo + Servlet
- Load Balancing
  - Spring Cloud LoadBalancer (Spring Cloud official support, after Hoxton
    version)
  - Dubbo LB
- Circuit Breaker
  - Alibaba Sentinel
- Distributed Tracing
  - NA
- Distributed Transactions
  - Seata
- Distributed Message
  - SCS RocketMQ
- Message Bus
  - Spring Cloud Bus (SCB)

### Service Orchestration

Products:

- Docker
- OpenStack
- Kubernates (K8S)

### API Gateway

### Service Mesh

#### Data Plane

#### Control Plane

## Architecture Principles

Three Principles of Architecture Design:

- Suitability Principle (Suitability over Completeness)
- Simplicity Principle (Simplicity over Complexity)
- Evolution Principle (Evolution over One-time Perfection)

### JIT-JEA

> Just In Time, Just Enough Architecture

### DRY

> Don't Repeat Yourself

### KISS

> Keep It Simple, Stupid

### SOLID

- Single Responsibility
- Open-Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

### YAGNI

> You Aren't Gonna Need It

### Progressive Optimization

> Premature optimization is the root of all evil. - Donald Knuth

Don't think about possible optimizations when writing a program, but focus on
making sure the code is clean, correct, readable, and easy to understand. If you
find it's too big or too slow after you've written it, then think about how to
optimize it.

In many areas, you can get 80% of the results with 20% of the effort (sometimes
it can be the 10/90 rule). Whenever you want to optimize code, first use a
profiling tool to find out where 80% of the execution time is spent, so you
know where to focus your optimization efforts.

Do remember that the slight performance improvement is not worth sacrificing
the clarity, cleanliness, readability and understanding of the code.

### Expose Problem As Soon As Possible

> A dead program is usually less harmful than a sick program.

One of the benefits of detecting problems early is that you can crash sooner.

When your code discovers that something that was supposedly impossible has
happened, your program is no longer viable, and everything it does from that
point on becomes suspect, so terminate it as quickly as possible.


### Contract-Oriented Design

Writing "shy code" is beneficial, shyness works in two ways:

- Do not exposing yourself to others.
- Do not interacting with too many people.

#### Orthogonality

> Orthogonality is a property of a system that allows its components to be
> developed, tested, and maintained independently of each other.

"Orthogonality" is a concept in software design, which means that the various
parts of the system should be independent of each other and not interfere with
each other. Modifying one part should not affect other parts; adding a function
should not make the system more complex or more difficult to maintain.

When introducing third-party toolkits and libraries, make sure they do not
destroy the independence and clear boundaries between parts of the system.

Organize your code into minimal organizational units (modules) and limit the
interactions between them so that if one module must be replaced later due to
a compromise, the other modules will continue to work.

The Law of Demeter:

The Law of Demeter, also known as the "Law of Demeter" or the "Principle of
Least Knowledge", is a guiding principle of object-oriented design. It
emphasizes that an object should know as little as possible about other objects,
interact only with its direct friends (classes), and avoid direct communication
with unfamiliar objects.

#### Assertive Programming

> Don't assume, prove. If it can't happen, use assertions to ensure it doesn't
> happen.

Assertive programming is a programming practice that uses assertions to 
ensure that certain conditions hold true at runtime. Assertions are used to
check for conditions that should never happen, such as invalid input or
application state. If an assertion fails, it indicates a bug in the code that
needs to be fixed. Assertions are typically used during development and testing
phases, and can be disabled in production environments to improve performance.

Implicit assumptions:

> Don't program by accident and assumption, program by deliberation.

> Don't use wizard code you don't understand, it make you regress to programming
> by coincidence.

People at all levels work with many assumptions in their heads - but these
assumptions are rarely documented and often conflict between different
developers. Assumptions that are not based on clear facts are the bane of
all projects.

Assertive programming helps to catch bugs early in the development process and
that the code behaves as expected.

__In addition to adding assertions, please keep them turned on__. Because your
first line of defense is to check for any possible errors, and your second line
of defense is to use assertions to try to detect errors you missed. Although
earlier assertions come with some performance cost, don't turn them off.

#### Defensive Programming

> It's a kind of contract-oriented programming in essence.

Defensive programming is a programming practice intended to ensure the continuing
function of a piece of software under unforeseen or unpredictable circumstances.

### Configuration-oriented Design

> Put abstractions in code and details in metadata.

> Postpone definition of most details until the last possible moment, and keep
details as “soft” as possible—as easy to change as possible.

It's also called "Metadata-oriented Design", which is a design principle that
emphasizes the separation of configuration and code. The idea is to put
abstractions in code and details in metadata, allowing for greater flexibility
and maintainability. This approach allows developers to change the behavior of
the system without modifying the code itself, making it easier to adapt to
changing requirements and environments.


### IoC (Inversion of Control)

### High cohesion & Low coupling

### GoF Design Patterns

## Architecture Patterns

### CQRS (Command and Query Responsibility Segregation)

CQRS is a software architectural pattern that separates the read and write
models of a system. The write model is responsible for handling commands and is
a representation of the current state of the system. The read model is
responsible for handling queries and is a representation of the data that is to
be displayed to the user. CQRS allows for the read and write models to be
specialized for their respective tasks, which can lead to better performance and
scalability.

### TDD (Test-Driven Development)

TDD is an agile software development process where developers write automated
tests before writing the code. The idea behind TDD is that if you write the
tests first, you will have a better understanding of what the code should do.
The tests act as a specification for the code. TDD ensures that the code is
testable, maintainable, and extensible.

- Tests act as documentation for the code
- Ensures that the code is testable, maintainable, and extensible
- Helps catch bugs early in the development process
- Provides a safety net for refactoring the code

### BDD (Behavior-Driven Development)

BDD is a software development process that focuses on the behavior of the
software. BDD is an extension of TDD, where tests are written in a more
natural language that stakeholders can understand. BDD ensures that the
software is developed based on the user’s needs and behaviors.

- Helps ensure that the software is developed based on the user’s needs and
  behaviors
- Provides a common language for developers, testers, and stakeholders
- Improves communication and collaboration between stakeholders
- Helps identify potential issues early in the development process

### DDD (Domain-Driven Design)

DDD is an approach to software development that focuses on the domain of
the software. The domain is the problem space that the software is intended
to solve. DDD ensures that the software is built around the domain and that
it solves the problem in the best possible way.

- Ensures that the software solves the problem in the best possible way
- Improves the understanding of the domain of the software
- Provides a common language for developers and domain experts
- Helps identify potential issues early in the development process

#### EBI (Entity-Boundary-Interactor)

![EBI](https://github.com/user-attachments/assets/2a59fc1b-48b6-4c11-a67f-a35ffe80a853)

#### Hexagonal Architecture (Ports & Adapters Architecture)

![Hexagonal Architecture](https://github.com/user-attachments/assets/db5a0668-fc6a-47eb-92a1-dd01c29708a1)

#### Onion Architecture

Onion Architecture is built on top of the Port & Adapter Architecture (also
known as Hexagonal Architecture), which mentions only 2 layers:

- Outer Layer - Represents the transport (communication) mechanism and infrastructure
- Inner Layer - Business Logic

![Onion Architecture](https://github.com/user-attachments/assets/323f4313-80fa-4825-8aea-f4ac3e9a3edd)

Onion Architecture, based on DDD, further divides the inner layer (Business
Logic Layer) into:

- Adapters, which correspond to the Adapter layer in Hexagonal Architecture
  - User Interface, Infrastructure, Tests
- Application Core, which is the core of the application, also the original
  Business Logic layer in Hexagonal Architecture
  - Application Services
  - Domain Services
  - Domain Model

And it clarifies the direction of dependencies:

- Outer layers depend on inner layers
- Inner layers are unaware of outer layers
- Without breaking the dependency direction, outer layers can directly call
  any inner layer (not necessarily adjacent layers), as seen in CQRS where
  Application Services directly call DAO in Query implementation

#### Clean Architecture

Compared to Onion Architecture, Clean Architecture adjusts as follows:

- Application Services are adjusted to Use Cases Domain Services
- Domain Model is adjusted to Entities

![The Clean Architecture](https://github.com/user-attachments/assets/cf25278e-f6c1-456e-8704-2dec7b4d7888)

Clean Architecture does not bring breakthrough concepts or patterns, but:

- It uncovers some concepts, rules, and patterns that were somewhat forgotten
- It clarifies some practical and important concepts, rules, and patterns
- It tells us how to integrate all the concepts, rules, and patterns to form
  a standard approach for building complex applications while maintaining
  maintainability

![The Clean Architecture Cone](https://github.com/user-attachments/assets/d358ecaa-99ef-4ac1-8c9c-2764b1558559)

> The technology stack and technology debt are directly proportional.

The more technology stacks you stack, the more debt you borrow and the more you
need to repay in the future. Therefore, you need to weigh the amount of
technology stack.

- If the introduction of a new technology can replace multiple old technologies,
  then it is particularly valuable.
- If a mature technology can be applied to as many different scenarios as
  possible to solve multiple types of problems, it will also become valuable.
  E.g. PostgreSQL to replace MySQL, Redis, MongoDB, etc.

### Explicit Architecture

In 2017, Herberto Graca proposed Explicit Architecture in his series of articles
on the chronicles of software architecture, which integrates DDD, Hexagonal,
Onion, Clean, CQRS, and other architectures.

![Explicit Architecture](https://github.com/user-attachments/assets/f1068278-2c2a-4ec3-97f9-66566d9830ea)

### Event-Driven

### Micro Services

### Micro Frontend

## Documentation

### C4 Model

The idea is to use 4 different granularity (or zoom) levels for documenting
software architecture:

- Level 1: System Context diagram
- Level 2: Container diagram
- Level 3: Component diagram
- Level 4: Code diagram

## Refactoring

When should you refactor?

You should consider refactoring your code whenever it has any of the following
characteristics:

- Repetition. You found a violation of the DRY principle.
- Non-orthogonal design.
- Outdated knowledge.
- Performance.

## References

- [Principles of Transaction-Oriented Database Recovery](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.87.2812&rep=rep1&type=pdf)
- [Eventual Consistency vs. Strong Eventual Consistency vs. Strong Consistency](https://www.baeldung.com/cs/eventual-consistency-vs-strong-eventual-consistency-vs-strong-consistency)
- [An In-Depth Analysis of Distributed Transaction Solutions](https://www.alibabacloud.com/blog/an-in-depth-analysis-of-distributed-transaction-solutions_597232)
- [Token Design for a Better API Architecture](https://nordicapis.com/token-design-better-api-architecture/)
- [Microservices Design Patterns Tutorial](https://www.tutorialspoint.com/microservices_design_patterns/index.htm)
- [ddd-hexagonal-cqrs-es-eda](https://github.com/bitloops/ddd-hexagonal-cqrs-es-eda)
