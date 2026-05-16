---
layout: post
title: The Handbook of Software Engineering Documentation
subtitle: The ultimate master guide to the alphabet soup of product and engineering documentation.
author: Jeffrey Tse
banner:
  image: https://i.postimg.cc/8k78Y0zF/image.png
  opacity: 0.6
categories:
  - computer
tags:
  - software
  - documentation
  - note
---

When it comes to software development, documentation is often overlooked but is
crucial for the success of any project. Here is the ultimate master guide to the
alphabet soup of product and engineering documentation. Think of these documents
as a waterfall (or a funnel) that starts at **30,000 feet (Business)** and ends
in the **trenches (Code)**. Each document hands off a more refined set of
instructions to the next team in line.

---

## Software Documentation Types

In the world of software development, there are several key documents that teams
use to communicate requirements, design, and implementation details. Each
document serves a specific purpose and is targeted at different audiences.

Here’s a breakdown of the most common types:

### MRD

- **Full Name:** Market Requirements Document
- **What It is:** A document that captures the market needs, customer pain
  points, and competitive landscape. It is often created before the BRD to justify
  the business case.
- **Scope:** Focuses on the "market" and customer insights, not the business
  goals or technical details.
- **The Core Question It Answers:** **What market problem** are we solving?
- **Who Writes It:** Market Research Analyst / Product Manager
- **Who Reads It:** Executives, Product Managers, Marketing Teams
- **What it Contains:** Market analysis, customer personas, competitive
  analysis, and high-level product opportunities.
- **Example:** "Our research shows that 60% of small businesses struggle with
  inventory management, and our product will target this pain point."

### BRD

- **Full Name:** Business Requirements Document
- **What It is:** A high-level document that captures the business goals and
  objectives behind a project or feature.
- **Scope:** Focuses on the "why" and the business value, not the technical
  details.
- **The Core Question It Answers:** **Why** are we doing this?
- **Who Writes It:** Business Analyst / Stakeholder
- **Who Reads It:** Executives, Product Managers
- **What it Contains:** Business goals, ROI, market problems, success metrics.
- **Example:** "We need to increase user retention by 15% and capture the
  European market."

### PRD

- **Full Name:** Product Requirements Document
- **What It is:** A document that translates the business goals from the BRD into
  specific features and user stories that the product team will build.
- **Scope:** Focuses on the "what" from the user's perspective, not the "how."
- **The Core Question It Answers:** **What** are we building for the end user?
- **Who Writes It:** Product Manager (PM)
- **Who Reads It:** Designers, Tech Leads, Developers
- **What it Contains:** User personas, features, user stories, high-level UX.
- **Example:** "As a user, I want to log in using my Google account."

### FRD

- **Full Name:** Functional Requirements Document
- **What It is:** A detailed document that specifies the exact behavior of each
  feature from a functional perspective.
- **Scope:** Focuses on the logic and user flows of specific features.
- **The Core Question It Answers:** **How** should the feature behave dynamically?
- **Who Writes It:** PM / Business Analyst
- **Who Reads It:** Developers, QA Engineers
- **What it Contains:** Logic, step-by-step system responses, user flows.
- **Example:** "If the user inputs an invalid password 3 times, lock the account
  for 10 minutes."

### SyRD

- **Full Name:** System Requirements Document
- **What It is:** A top-level document that translates broad stakeholder
  business goals into technical requirements allocated across the whole system.
- **Scope:** Focuses on the entire system environment, including hardware,
  software, and infrastructure requirements.
- **The Core Question It Answers:** **What environment** does it need?
- **Who Writes It:** Hardware/Systems Engineer
- **Who Reads It:** Systems Engineers, Hardware Engineers, DevOps
- **What it Contains:** Hardware, software, and infrastructure requirements.
- **Example:** "The software must run on Ubuntu 22.04 with minimum 8GB RAM."

### SRS or SRD

- **Full Name:** Software Requirements Specification/Document
- **What It is:** A detailed document that specifies the software-specific
  requirements, including technical constraints, performance metrics, and
  security requirements.
- **Scope:** Derived directly from the SyRS, this document zooms in entirely on
  the software product (Only the software, not the hardware or infrastructure).
- **The Core Question It Answers:** **What constraints** must the software meet?
- **Who Writes It:** Technical Lead / Architect
- **Who Reads It:** Developers, QA
- **What it Contains:** Technical specs, APIs, security, scale constraints.
- **Example:** "The system must handle 5,000 concurrent users and have a response
  time under 200ms."

### SDD

- **Full Name:** Software Design Document
- **What It is:** A detailed blueprint that translates the requirements from the
  SRS into a concrete architecture and design plan for developers to follow.
- **Scope:** The actual engineering blueprint for how the software will be built.
- **The Core Question It Answers:** **How** will we code and architect it?
- **Who Writes It:** Software Architect
- **Who Reads It:** Tech Leads, Senior Developers
- **What it Contains:** High-level system architecture diagrams, microservices
  boundaries, database choices.
- **Example:** "We will deploy a lightweight Python object-detection model on the
  cart's Edge computer. The backend will use a Node.js microservice architecture
  hosted on AWS. Here is the PostgreSQL database schema for the cart state..."

### TSD

- **Full Name:** Technical Specification Document
- **What It is:** A more modern, often less formal document that serves the same
  purpose as the SDD. It is a living document that evolves with the project.
- **Scope:** Similar to SDD, but often more focused on the technical implementation
  details rather than high-level design.
- **The Core Question It Answers:** **How** do we write the actual code?
- **Who Writes It:** Tech Leads / Senior Developer
- **Who Reads It:** Developers
- **What it Contains:** Detailed technical instructions, class diagrams,
  database schemas, API endpoints, error-handling logic.
- **Example:** Class diagrams, database schemas, API endpoints, error-handling
  logic.

### The Document Hierarchy

From a high-level perspective, these documents can be visualized as a hierarchy
that flows from the business goals down to the technical implementation:

```
[MRD] Market Requirements    -> "What market problem are we solving?"
  ↓
[BRD] Business Requirements  -> "Why are we building this and how do we make money?"
  ↓
[PRD] Product Requirements   -> "What features are we building for the user?"
  ↓
[FRD] Functional Specs       -> "How should those features behave step-by-step?"
  ↓
[SRS] System/Software Specs  -> "What are the technical and performance constraints?"
  ↓
[SDD / TSD] Design & Tech    -> "How do we structurally code and architect it?"
```

### Key Nuances & Modern Reality

In fast-moving tech companies, you will rarely see all six of these documents
existing separately.

1. **The Overlap:** In modern Agile environments, **nobody writes all of these
   separately**. Doing so would result in a mountain of outdated paperwork.
2. **The Agile Merge:** Today, the **PRD and FRD** are usually merged directly
   into **Jira tickets or User Stories**.
3. **SRS vs. SDD/TSD:** People often mistake the SRS for a design document.
   Remember: The **SRS** is a list of _rules and requirements_ (the target). The
   **SDD/TSD** is the _engineering blueprint_ built to hit that target.
4. **The Tech Hand-off:** The **SRS and SDD** are frequently blended into a
   single "Technical Design Doc" (TDD) or "RFC" (Request for Comments) created
   by the engineering team before they start a sprint.
5. **The Industry Split:** You will primarily see **SRSs** in heavy engineering,
   aerospace, robotics, or IoT, where hardware and software are deeply
   interdependent. Pure software SaaS companies rarely use an SRS.

If you are working in a fast-paced startup, you will likely only ever see a
**PRD** (written by a PM) and a **TSD/Architecture doc** (written by the
engineering team).

---

## Documents in SDLC Stages & Team Collaboration

In a standard Software Development Life Cycle (SDLC), these documents act as a
relay race. One document hands off its information to the next, guiding the
project from a vague business idea to a fully deployed system.

Here is how these documents map to each stage of the development workflow and
how the different teams collaborate around them.

### 1. The Mapping: Documents by SDLC Stage

Stage 0: Market Research & Validation (The "What Market Problem")

- **Document used:** **MRD** (Market Requirements Document)
- **Who collaborates:** Market Research Analysts, Product Managers, and
  Executives.
- **What happens:** The team identifies a market problem or opportunity. The MRD
  captures customer pain points and competitive analysis to justify the business
  case.

Stage 1: Initiation & Strategy (The "Why")

- **Document used:** **BRD** (Business Requirements Document)
- **Who collaborates:** Executives, Product Directors, Business Analysts, and
  Sales/Marketing leads.
- **What happens:** The business identifies a market problem or revenue
  opportunity. They align on the financial objectives and project viability before
  any engineering resources are spent.

Stage 2: Product Discovery & Definition (The "What")

- **Document used:** **PRD** (Product Requirements Document)
- **Who collaborates:** Product Managers (PMs), UX/UI Designers, and Engineering
  Leads.
- **What happens:** The PM takes the business goals from the BRD and translates
  them into user-centric features. Designers use the PRD to start creating user
  flows and wireframes, while engineering leads review it to ensure the scope is
  realistic.

Stage 3: System & Technical Specification (The "Constraints")

- **Documents used:** **FRD** (Functional Requirements), **SRD** (System
  Requirements), **SRS** (Software Requirements Specification)
- **Who collaborates:** PMs, Systems Engineers (if hardware is involved),
  Technical Architects, and QA Leads.
- **What happens:** The team maps out exactly how the system must behave to
  fulfill the PRD. The QA team uses these documents to start writing test plans,
  while the architects use them to define technical and performance
  boundaries (e.g., system latency, security protocols).

Stage 4: Architecture & Engineering Design (The "How")

- **Document used:** **SDD** (Software Design Document / Technical Design Doc)
- **Who collaborates:** Software Architects, Lead Developers, and DevOps Engineers.
- **What happens:** Engineers turn the requirements into a technical blueprint.
  They design the database schemas, choose design patterns, define API contracts,
  and map out the infrastructure. **No code is written yet**, but the exact
  implementation plan is finalized.

Stage 5: Execution (Implementation & Testing)

- **Documents used:** **Jira Tickets / User Stories** (derived from the PRD/FRD)
  and **Test Cases** (derived from the SRS/FRD).
- **Who collaborates:** Developers and QA Engineers.
- **What happens:** The SDD serves as the guide for developers writing the code,
  while the QA team uses the SRS/FRD to verify that the built software
  actually meets the original requirements.

### 2. How They Collaborate Together (The Feedback Loops)

Documentation is rarely a strict one-way street. The magic lies in the
collaborative feedback loops between stages:

```
[BRD] ──> [PRD] ──> [SRS/FRD] ──> [SDD/TCD] ──> [Code/Testing]
  ▲         ▲           ▲             │
  │         │           └─────────────┤ (Technical constraints found)
  │         └─────────────────────────┤ (Scope adjustments needed)
  └───────────────────────────────────┘ (Budget/Timeline shifts)

```

- **The Reality Check Loop (SDD to PRD/SRS):** While writing the SDD, a software
  architect might realize that a feature requested in the PRD (e.g., "Real-time
  global data syncing in under 10 milliseconds") is architecturally impossible
  or too expensive. They push back, forcing an update to the SRS or PRD to
  adjust the scope.
- **The Parallel Work Loop (QA and Dev):** The moment the **SRS and FRD** are
  finalized, collaboration splits into two parallel tracks. Developers use
  the **SDD** to build the feature, while QA engineers simultaneously use
  the **SRS** to write automated test scripts. Because they are working
  from the same source of truth, QA is ready to test the moment developers
  finish writing code.
- **The Living Document Transition:** In modern Agile setups, the PRD, FRD, and
  SRS often live in a shared space like Confluence. Instead of handing off
  static PDFs, teams actively comment, tag each other, and link directly to
  Jira tasks and Figma prototypes, keeping the documentation dynamic.

### 3. The Critical Role of System Design

System Design takes place during **Stage 4: Architecture & Engineering Design**.
It sits squarely between the **Requirements Phase** (what the system needs to
do) and the **Implementation/Coding Phase** (writing the actual code).

If you try to do System Design too early, you end up designing a solution for a
problem you don’t fully understand yet. If you do it too late, developers are
already writing messy, uncoordinated code that will inevitably require massive
refactoring.

#### The Two Sub-Stages of System Design

In practice, System Design is broken down into two distinct sub-stages within
the design phase:

1. High-Level Design (HLD) / System Architecture

This happens the moment the **SRS (Software Requirements Specification)** is finalized.

- **The Focus:** The macro view of the system.
- **Key Decisions:**
  - What architecture pattern will we use? (e.g., Microservices, Monolith, Serverless).
  - Where will the data live? (e.g., SQL vs. NoSQL, caching layers like Redis).
  - How will services talk to each other? (e.g., REST APIs, GraphQL, or message brokers like Kafka).
  - What cloud infrastructure is needed? (AWS, Azure, GCP setup).

2. Low-Level Design (LLD) / Object-Oriented Design

This happens immediately after the HLD is approved, right before developers open their IDEs to write code.

- **The Focus:** The micro view of the system.
- **Key Decisions:**
  - Defining database schemas, table relationships, and indexes.
  - Mapping out exact class diagrams, design patterns (e.g., Singleton, Factory), and code modules.
  - Writing the exact API contracts (request/response payloads) so frontend and backend teams can work in parallel.

#### Inputs vs. Outputs of the System Design Stage

To visualize how it acts as a transition point, look at what goes into this stage and what comes out:

| Inputs (What the Designer Reads)                                                                            | The System Design Stage                                                    | Outputs (What the Developer Reads)                                  |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **PRD / User Stories:** To understand the user behavior.                                                    | Architects & Lead Devs map out components, data flows, and infrastructure. | **SDD (Software Design Document):** The blueprint.                  |
| **SRS / Non-Functional Specs:** To understand scale requirements (e.g., "Must handle 10,000 requests/sec"). |                                                                            | **API Contracts:** Swagger/OpenAPI specs.                           |
|                                                                                                             |                                                                            | **Architecture Diagrams:** Visual maps of the cloud infrastructure. |

#### Why This Sequence Matters

Skipping straight from the PRD/SRS to coding without a dedicated System Design
stage is the leading cause of "technical debt." System Design is your
opportunity to break the problem down, stress-test your architecture against
scalability and security requirements on paper, and ensure that every developer
is building toward the exact same structural vision.

---

## The Blueprint to Streamline Documentation

Trying to juggle all of these documents usually leads to "documentation
fatigue"—where teams spend more time updating files than actual coding or
shipping products. The secret to streamlining is ruthlessly cutting down the
number of documents based on your team's size while clearly defining who owns
what.

Here is a blueprint to establish scope and streamline the process.

### 1. The Ownership & Scope Matrix

To prevent people from stepping on each other's toes or leaving gaps, define
clear boundaries for who **owns** (writes) and who **consumes** (reads) the
documentation:

| Document Group                        | What it Covers                                                          | Owner                 | Primary Consumers                   |
| ------------------------------------- | ----------------------------------------------------------------------- | --------------------- | ----------------------------------- |
| **The Product Brief** (BRD/PRD)       | Business goals, user problems, features, and success metrics.           | Product Manager (PM)  | Designers, Tech Leads, Stakeholders |
| **The Technical Blueprint** (SRS/SDD) | System architecture, database schemas, APIs, and technical constraints. | Tech Lead / Architect | Software Engineers, QA Engineers    |

### 2. Streamlining Frameworks by Team Size

Find the tier that fits your current team structure to see what you can safely eliminate.

Tier 1: The Lean Team (1 to 15 people)

- **The Problem:** PMs wear many hats; developers need to move fast. Writing
  five separate documents will ground your momentum to a halt.
- **The Streamlined Approach:** Collapse everything into just **two living
  documents**.

1. **The "1-Pager" PRD:** Combines the BRD and PRD. It states the business goal,
   user persona, and feature list in a brief, scannable format.
2. **The RFC / Tech Design Doc (TDD):** Combines the SRS and SDD. The lead
   engineer writes a quick breakdown of the database changes and API endpoints
   directly linked to the PRD.

Tier 2: The Mid-Sized Team (15 to 50 people, multiple squads)

- **The Problem:** Communication gaps appear. QA needs clear criteria, and
  frontend/backend teams need to build in parallel without breaking things.
- **The Streamlined Approach:** Use **three distinct documents**.

1. **PRD:** Purely user and feature-focused.
2. **FRD / User Stories:** Handled via Jira/Linear tickets. The functional logic
   lives inside the ticketing system, not a static document.
3. **SDD (Software Design Document):** A dedicated technical blueprint ensuring
   the architecture scales and the team is aligned before sprints start.

Tier 3: The Enterprise Team (50+ people)

- **The Problem:** High bureaucracy, compliance requirements, and siloed
  departments (e.g., separate business, product, engineering, and QA teams).
- **The Streamlined Approach:** You likely need the full stack (**BRD
  $\rightarrow$ PRD $\rightarrow$ SRS $\rightarrow$ SDD**), but you
  streamline by automating the pipeline. The BRD mandates the PRD, which
  auto-generates Jira epic templates, which link directly to the engineering
  team's SDD in Confluence or Notion.

### 3. Best Practices for "No-Chaos" Documentation

- **Ban the PDF:** Keep documentation in a collaborative workspace (Notion,
  Confluence, Basecamp). If a document isn't searchable or editable, it's dead.
- **The "Definition of Ready":** Establish a rule that a feature cannot enter a
  development sprint unless the technical blueprint (SDD/TDD) has been reviewed
  and signed off by at least one peer engineer.
- **Embed Logic in Tickets:** Stop writing massive FRDs. Write a clean PRD for
  context, and put the hyper-specific functional logic ("If user clicks X, then Y
  happens") directly into the description of the relevant Jira/Linear
  ticket.

---

## Documentation Frameworks

There are several excellent frameworks exist that bring order to documentation
chaos. Rather than reinventing the wheel, you can adopt a framework based on
_what_ part of the documentation pipeline you are trying to fix.

Here are the four most widely adopted frameworks in modern software development,
categorized by the problem they solve.

### 1. For Architecture & System Design: **arc42**

If your engineering team struggles with how to structure an **SDD (Software
Design Document)** or **SRS**, **arc42** is the gold standard. It provides a
lightweight, 12-part template for documenting software architecture.

- **How it works:** It breaks system design down into logical parts, starting
  with the big picture and drilling down into technical details.
- **The Cheat Code:** You don't have to use all 12 sections. For smaller teams,
  you can ruthlessly pare it down to the core 4:

1. **Context and Context Constraints:** What is the system interacting with?
2. **Architecture Decisions:** _Why_ did we choose this tech stack or pattern?
3. **Building Block View:** What are the main components/modules?
4. **Runtime View:** How do these components talk to each other when a user
   triggers an action?

### 2. For Visualizing System Design: **The C4 Model**

Textual documentation of system architecture is notoriously hard to read. The
**C4 Model** is a framework specifically for creating architecture diagrams that
people can actually understand.

- **How it works:** It treats software architecture like Google Maps. You zoom
  in and out through 4 levels of detail:
- **Level 1: Context:** The absolute highest level (Users, the system, and
  external dependencies). Anyone can read this.
- **Level 2: Containers:** Zooming in to show applications, databases, and
  microservices.
- **Level 3: Components:** Zooming into a single container to show internal
  modules or controllers.
- **Level 4: Code:** Zooming into the actual class diagrams (rarely documented,
  usually auto-generated).

- **Why it helps:** It ensures that every diagram in your SDD follows the same
  visual vocabulary, making it easy for new developers to parse.

### 3. For Technical & Product Docs: **Diátaxis**

If your team is struggling with user-facing, API, or internal developer
documentation being messy and unorganized, **Diátaxis** is the modern framework
used by organizations like Canonical, Django, and Cloudflare.

- **How it works:** It divides all documentation into four distinct quadrants
  based on the reader's intent and whether they are working or learning:

|                       | Practical (Action-oriented)                                                 | Theoretical (Knowledge-oriented)                                                          |
| --------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Learning-oriented** | **Tutorials:** Lessons that guide a beginner through a learning experience. | **Explanation:** Discussion/context that clarifies a topic or architectural choice.       |
| **Goal-oriented**     | **How-To Guides:** Practical steps to solve a specific, real-world problem. | **Reference:** Technical descriptions of the machinery (e.g., API schemas, CLI commands). |

- **Why it helps:** It prevents "doc pollution," where a single page tries to be
  an introduction, an API reference, and a tutorial all at once.

### 4. For Workflow Integration: **Docs-as-Code**

This is less about document structure and more about a **process framework**. If
your developers hate going to Notion or Confluence to update documents, you
bring the documentation to them.

- **How it works:** Documentation is treated exactly like software code:
- Written in Markdown (`.md`).
- Stored in the same **Git repository** as the codebase.
- Reviewed via **Pull Requests** (a senior dev reviews code changes and doc
  changes at the same time).
- Deployed automatically to an internal site (like Backstage, MkDocs, or
  Docusaurus) via CI/CD pipelines.

- **Why it helps:** It integrates documentation seamlessly into the developer’s
  daily routine, dramatically increasing the likelihood that technical docs
  actually stay up to date.

### Which one should you pick?

- If your developers complain that **"we don't know how to structure our
  technical design notes,"** adopt a stripped-down version of **arc42** alongside
  the **C4 Model** for diagrams.
- If your team says **"our internal wiki is a chaotic mess where everything is
  buried,"** reorganize your workspace categories using the **Diátaxis**
  quadrants.

## Conclusion

Documentation is the often-overlooked backbone of successful software projects.
By understanding the different types of documents (BRD, PRD, FRD, SRD, SRS, SDD)
and how they interact across the SDLC, you can create a streamlined
documentation process that actually gets read and used. Whether you choose
to adopt frameworks like arc42 for system design or Diátaxis for product
docs, the key is to find the right balance between thoroughness and agility.
With the right documentation strategy, your team can move faster, reduce
technical debt, and ultimately build better software that meets both
business goals and user needs.
