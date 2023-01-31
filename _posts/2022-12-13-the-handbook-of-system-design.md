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

**1. Requirements Analysis**

Outline the scope of the system, and come out SRS (Software Requirements Specification).

- Use cases (Systems exist to solve specific problems)
  - Who is going to use it?
  - How are they going to use it?
  - What does the system do?
  - ...
- Constraints
  - Mainly identify **traffic and data handling** constraints at scale.
  - Scale of the system such as requests per second, requests types, data written
    per second, data read per second)
  - Special system requirements such as multi-threading, read or write oriented.
- Assumptions

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

**2. High Level Design (HLD, known as General Design) **

Outline a high level architecture design, such as system module and technical route.

- Sketch the system architecture
  - Components
    - High cohesion and low coupling for the independence of components
    - Divide by functions
    - Divide by domains
  - Relationship of components
    - Horizontal Relationship
    - Vertical Relationship
- Scale the design
  - Understanding Bottlenecks
    - Too many user requests
    - The data is too huge
  - Solutions
    - Caching
      - Application Caching
      - Database Caching
      - In-memory Caches
    - Load balancer
    - Vertical scaling
      - Scale by adding more power (CPU, RAM) to your existing machine.
    - Horizontal scaling
      - Scale by adding more machines into your pool of resources.
    - Database sharding
- Justify your ideas

**3. Design components (LLD, Low Level Design, or Detail design)**

Dive into details for each component, such as interface, algorithm, process,
state transition, etc.

Related Tools:

- Program Flow Chart
- N-S Structure Diagram
- Problem Analysis Diagram (PAD)
- ...

**4. Implementation**

**5. Testing**

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

- Unit Testing: To test the smallest independent piece of code to prevent regressions.
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

## References

- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [System Design Tutorial](https://www.geeksforgeeks.org/system-design-tutorial/)
- [System Design Cheatsheet](https://gist.github.com/vasanthk/485d1c25737e8e72759f)
