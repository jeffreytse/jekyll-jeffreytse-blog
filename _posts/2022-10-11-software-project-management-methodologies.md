---
layout: post
title: Software Project Management Methodologies
author: Jeffrey Tse
banner:
  image: https://i.postimg.cc/Y0Gf2ZX5/image.png
  opacity: 0.70
categories:
  - computer
tags:
  - software
  - management
  - methodology
  - note
---

As we all know, software development is a complex process that requires
careful planning, execution, and monitoring. To ensure that software projects
are completed on time, within budget, and to the required quality standards,
software project management methodologies have been developed. These
methodologies provide a structured approach to software development, helping
teams to manage the various aspects of the project, including requirements
gathering, design, implementation, testing, and deployment.

## What is SDLC?

Software Development and Management Models of Software Engineering:

- Plan
- Design
- Build
- Test
- Release
- Monitor

The goal is to produce software of the highest quality and lowest cost in the
shortest possible time.

## What is DTAP?

**Development, testing, acceptance and production (DTAP)** is a phased approach
to software testing and deployment. The four letters in DTAP denote the
following common steps:

- **Development:** The program or component is developed on a development system.
  This development environment might have no testing capabilities.
- **Testing:** Once the software developer thinks it is ready, the product is
  copied to a test environment, to verify it works as expected. This test
  environment is supposedly standardized and in close alignment with the
  target environment.
- **Acceptance:** If the test is successful, the product is copied to an
  acceptance test environment. During the acceptance test, the customer will
  test the product in this environment to verify whether it meets their
  expectations.
- **Production:** If the customer accepts the product, it is deployed to a
  production environment, making it available to all users of the system.

DTAP is a software development and deployment methodology that emphasizes the
importance of separating the different stages of software development to ensure
that software is developed, tested, and deployed in a controlled and systematic
manner. The DTAP methodology is commonly used in software development projects
to ensure that software is developed and deployed in a way that minimizes
risks and maximizes quality.

Project Environment:

- DEV (Development)
  - The environment where developers write and test their code.
  - It is typically a local or isolated environment where developers can work
    without affecting other environments.
- SIT (System Integrate Test)
  - The environment where the software is integrated and tested as a whole.
  - It is used to verify that different components of the software work
    together as expected.
- UAT (User Acceptance Test)
  - The environment where end-users test the software to ensure it meets their
    requirements and expectations.
  - It is typically the final stage before the software is deployed to
    production.
- STG (Staging/Pre-Production)
  - The environment that closely resembles the production environment.
  - It is used for final testing and verification before the software is
    deployed to production.
- PROD (Production)
  - The live environment where the software is used by end-users.
  - It is the final stage of the software development lifecycle, and any issues
    in this environment can have a significant impact on users.

## Software Development Approaches

There are three main approaches to software development:

- **Iterative development:** refining the product through repeated cycles
- **Incremental development:** building the product in small, functional parts
- **Hybrid development:** combined iterative and incremental development, the
  standard in most Agile methodologies

![Iterative development Approach](https://i.postimg.cc/Z0znSHKq/image.png)

**Iteration Development** is the process of constantly enriching details. With
each iteration, we should make the project clearer and the details more perfect
step by step.

![Incremental development Approach](https://i.postimg.cc/y8Xn365f/image.png)

**Increment Development** has no overall outline. It starts with a complete part
in detail, and is completed piece by piece until a complete product is finally
formed.

- The focus is on "**increment**": the system is divided into multiple modules, and
  each module is gradually built as a functional increment.
- Each increment is an independently usable function.
- The goal is **to deliver a part of the operational system as early as
  possible**, and gradually increase the complete functionality.

![Iterative & Incremental Approaches](https://i.postimg.cc/D0ryW3xR/image.png)

**Iterative and Incremental Development** contains two core ideas:

- **Incremental:** Like above, gradually increase system functions.
- **Iterative:** Each increment/module can be gradually improved through multiple
  "iterations" instead of being done all at once.

For example:

- **Incremental Development:**
  - The first delivery is the login function;
  - The second delivery is the user profile function;
  - The third delivery is the order management function;
  - New functions are delivered each time, and the delivered functions are
    rarely modified.
- **Iterative and Incremental Development:**
  - The first delivery is the login function V0.1;
  - The second delivery is the login function UI + adding user profile V0.2;
  - The third delivery is the user profile + adding order management V0.3;
  - Each iteration improves the delivered functions and adds new functions.

Table below summarizes the differences:

| Features                  | Incremental Development         | Iterative and Incremental Development      |
| ------------------------- | ------------------------------- | ------------------------------------------ |
| Core                      | Incremental                     | Incremental + Iterative                    |
| Modify existing features? | Usually not modified            | Frequent iterative optimization            |
| Delivery method           | One new feature block at a time | New features + improvement of old features |
| Compatibility with Agile  | High                            | Higher (in line with the spirit of Agile)  |

> Note: Iteration and increment are two types of images that correspond to two
> forms of display in Web applications. I wonder if you have any impression that
> when the Internet speed is not good, some websites open large images piece by
> piece, while some websites open large images that are blurry first and then
> clear step by step. Students who are interested can search and find out the
> role of the continuous function when exporting to WEB format in PhotoShop.

## Waterfall Model

Developed in the 1950s for manufacturing and construction industries, the
Waterfall model is a linear sequential process where progress flows steadily
from one step to the next (like a waterfall). Because no formal software
methodologies existed at the time, this hardware-oriented model was adapted
(and officially dubbed the "waterfall model") in the 1970s for application
development. Each phase in Waterfall is completed before the next begins,
and changes made during one phase typically won’t be revisited in later stages.

![Waterfall Model](https://i.postimg.cc/zGcrSVYr/image.png)

Waterfall is favored in environments with regulatory compliance that require
meticulous planning and documentation — healthcare, defense, and similar
industries.

The Waterfall model consists of the following phases:

- Requirements
- Design
- Implementation
- Verification
- Maintenance

![Waterfall Phases](https://i.postimg.cc/HxMPMLdB/image.png)

Advantages of the Waterfall Model:

- **Clear Structure & Scope:** The Waterfall model has a clear and structured
  approach, making it easy to understand and manage.
- **Detailed Documentation:** Each phase of the Waterfall model requires
  detailed documentation, which helps in maintaining a clear record of the
  project.
- **Simplified Mangement:** The linear nature of the Waterfall model makes it
  easier to manage and track progress, as each phase has specific deliverables
  and timelines.
- **Early Design Decisions:** The Waterfall model requires all design decisions
  to be made upfront, which can help in avoiding scope creep and ensuring that
  the project stays on track.

## Incremental Build Model

The Incremental Build Model is a software development methodology that focuses
on delivering functional components in parts, rather than delivering the entire
software product at once. It is an iterative approach that allows teams to
develop and deliver software in small, manageable increments, which can be
tested and validated before moving on to the next increment.

![Incremental Build Model](https://i.postimg.cc/VkCMsZPW/image.png)

The Incremental Build Model is a software development model whose core idea is:

- Divide the system into multiple small modules (increments)
- Each module can be developed, tested and deployed independently
- Each increment is a working function, which is eventually combined into a
  complete system
- Each delivery brings a "usable version"

Although the Incremental Build Model is not an Agile method (such as Scrum, XP,
Kanban, etc.), it is:

- **One of the core technical means for Agile to be implemented**
- Agile's core value of "**delivering working software**" relies on incremental
  construction
- Almost all Agile methods (Scrum, XP, SAFe) adopt the **incremental +
  iterative** development method.

Why can't we say it is an Agile method?

- Agile is a development concept centered on values and principles (see [Agile
  Manifesto](https://agilemanifesto.org/)), which emphasizes "how to organize
  a team", "how to collaborate with customers", and "how to respond to changes"
- The Incremental Build Model is more like an **engineering method** or **process
  model**, not an Agile methodology

That why Incremental Build Model is not an Agile methodology itself, but it is
a fundamental development approach widely used in Agile practices.

## Agile Model

The implementation of the agile model mainly includes SCRUM, XP (Extreme
Programming), Crystal Methods, FDD (Feature Driven Development) and so on.
Among them, SCRUM and XP are the most popular.

![Popularity Diagram](https://user-images.githubusercontent.com/9413601/219058022-7280d4b3-92c4-4caf-b2a4-21f434f09e63.png)

The characteristics of Agile Development can be summed up in the following four
statements:

- **Individuals and interactions** over **processes and tools**
- **Working software** over **comprehensive documentation**
- **Customer collaboration** over **contract negotiation**
- **Responding to change** over **following a plan**

Stages in Agile SDLC:

- **Planning:** Creating a product backlog and prioritizing user stories.
- **Design:** Defining the architecture and design of the software.
- **Development/Iteration:** Building and testing the software in short sprints.
- **Testing/Integration:** Continuous testing throughout the sprint to ensure quality.
- **Deployment/Release:** Releasing working software to users.
- **Operations/Feedback:** Gathering feedback from users and planning for the
  next iteration.

![Stages in Agile SDLC](https://i.postimg.cc/NFxQq43B/image.png)

Waterfall vs Agile:

![Waterfall vs Agile](https://i.postimg.cc/brb0gGS7/image.png)

### Scrum

Scrum is an approach for managing projects with more speed, flexibility and
energy. Instead of relying on plans, documentation and meetings, you work with a
dedicated team in short sprints towards your end result, using feedback from
stakeholders along the way. Scrum is a flexible way of working, made for a
rapidly changing world.

Scrum is widely used in software development, but is suitable for almost all
projects and organizations.

Origin of Scrum:

The term '**Scrum**' was **first introduced by professors Hirotaka Takeuchi and
Ikujiro Nonaka** in 1986 in their article "The New New Product Development Game"
at Harvard Business Review.

They borrowed the name 'Scrum' from the **game of rugby**, to stress the
importance of teamwork to deal with a complex problem.

Scrum Workflow:

![Scrum Workflow](https://i.postimg.cc/wvz9MZcD/image.png)

Scrum 3 Roles:

- **Product Owner**
  - The key stakeholders with a vision who provides direction to the team
    for each sprint
- **Team**
  - Five to nine professionals in various disciplines who are jointly
    responsible for the results
- **Scrum Master**
  - A facilitator who focuses completely on the process then there are scrum
    lists

Scrum 3 Lists:

- **Product backlog**
  - list your ambitions and express how you intend to achieve them
- **Sprint backlog**
  - the shopping list of products you want to produce in the next sprint
  - the definitions of done by the end of the sprint
- **Scrum board**
  - all of the members tasks
  - task status
    - to do
    - busy
    - done

Scrum 4 Meetings:

- **Sprint planning**
  - What exactly are we going to achieve during this sprint and who's doing what
- **Stand-up**
  - Everything going according to the plan and are we going to make it
- **Review**
  - During which you deliver your results and receive feedback
- **Retrospective**
  - You look back on the process and reflect what you can improve as a team for
    the next sprint

Definition of Ready (DoR) and Definition of Done (DoD):

- **DoR:** It's the standard for a requirement to be accepted by the team. It is
  considered that the requirement is ready and can flow into the research and
  development task queue. It is the standard for requirement admission.
- **DoD:** The purpose of DoD is to give everyone a unified understanding of the
  "completion" standard and prevent misunderstandings. It can be divided into
  different dimensions to define.

Story Points:

Story points are a way to estimate the amount of effort required to complete a
user story in your product backlog. You’ll usually estimate story points before
a sprint planning meeting, since that’s when your team determines how much work
they can carry out in an upcoming sprint.

![Story Point Matrix](https://i.postimg.cc/d1WwKpd8/image.png)

Typically, story points take into account three factors that can impact a task’s
scope and effort, and the story point’s value increases accordingly. Since story
points are relative, you find their value by factoring in these details and
comparing similar tasks to each other.

- **Risk** is the amount of total risk or uncertainty associated with the task. For
  example, if the task involves third parties, contractors, or project
  stakeholders, it can increase the amount of risk.
- **Repetition** is the team’s experience with similar tasks.
- **Complexity** is the task’s level of difficulty (and how clear the objectives
  of the task are).

One important thing to know is that story points are relative—meaning that their
relative value and ratios to each other are what matter, not their actual
numerical value.

Stand-up Meeting:

A stand-up meeting is a short daily meeting that helps teams to synchronize
their activities and create a plan for the next 24 hours. The name comes from
the fact that participants usually stand up during the meeting to keep it short
and focused. Stand-up meetings are also known as daily scrums, daily huddles,
or daily check-ins.

Work Breakdown Structure (WBS):

A work breakdown structure (WBS) is a hierarchical decomposition of a project
into smaller, more manageable components. It helps to organize the team's work
into manageable sections, making it easier to plan, execute, and monitor the
project. A WBS is typically represented as a tree structure, with the project
goal at the top and the individual tasks or deliverables at the bottom.

![Work Breakdown Structure](https://i.postimg.cc/v8v5LN3m/image.png)

![WBS Example](https://i.postimg.cc/L6HRgSkB/image.png)

WBS Level:

![WBS Level](https://i.postimg.cc/fWPPcCC1/image.png)

- **First level:** The project goal or objective. It corresponds to Epic in Agile.
- **Second level:** Major deliverables or milestones. It corresponds to Features
  in Agile.
- **Third level:** Sub-deliverables or tasks. It corresponds to User Stories in
  Agile.

Converting WBS to Gantt Chart:

![Work Breakdown Structure to Gantt](https://i.postimg.cc/6QNdhxJy/image.png)

### eXtreme Programming (XP)

eXtreme Programming (XP) is an iterative agile methodology based on highly
disciplined software engineering practices such as pair programming.

XP emphasizes customer satisfaction, continuous feedback, and rapid iterations.
It encourages frequent releases of small, functional increments of software,
allowing teams to respond quickly to changing requirements and deliver value to
the customer.

![XP Principles](https://i.postimg.cc/rFKPkgtS/image.png)

XP practices include:

- **Pair Programming:** Two developers work together at one workstation, with one
  writing code and the other reviewing it in real-time.
- **Test-Driven Development (TDD):** Writing tests before writing the actual code
  to ensure that the code meets the requirements and is of high quality.
- **Continuous Integration:** Integrating code changes into a shared repository
  frequently to detect and fix issues early.
- **Refactoring:** Continuously improving the codebase by restructuring it
  without changing its external behavior.
- **Small Releases:** Delivering small, functional increments of software
  frequently to gather feedback and make adjustments as needed.
- **Planning Game:** A collaborative planning session where the team and
  stakeholders prioritize features and estimate effort.
- **Simple Design:** Keeping the design simple and avoiding unnecessary complexity
  to make it easier to understand and maintain.
- **Collective Code Ownership:** All team members are responsible for the code,
  allowing anyone to make changes to any part of the codebase.
- **On-Site Customer:** Having a customer representative available to provide
  feedback and clarify requirements throughout the development process.
- **Sustainable Pace/40-Hour Work Week:** Promoting a sustainable work pace to
  avoid burnout and maintain productivity.

![XP Practices](https://i.postimg.cc/fyXFdRzL/image.png)

### Crystal Method

Crystal Method is a family of agile methodologies that focuses on the
importance of people and their interactions in the software development process.

Crystal Method emphasizes the need for flexibility and adaptability, allowing
teams to choose the practices and tools that best suit their project and
organization. It is based on the principle that there is no one-size-fits-all
approach to software development, and that teams should be empowered to
choose the practices that work best for them.

Crystal Method consists of several methodologies, each tailored to different
project sizes and complexities. Some of the most common Crystal Method
methodologies include:

- **Crystal Clear:** For small teams (up to 8 people) working on non-critical
  projects.
- **Crystal Yellow:** For small to medium-sized teams (up to 20 people) working
  on projects with moderate complexity.
- **Crystal Orange:** For medium-sized teams (up to 50 people) working on
  projects with higher complexity.
- **Crystal Red:** For larger teams (up to 100 people) working on complex
  projects.
- **Crystal Maroon:** For very large teams (over 100 people) working on
  extremely complex projects.

Crystal Method practices include:

- **Frequent Delivery:** Delivering working software frequently to gather
  feedback and make adjustments as needed.
- **Reflective Improvement:** Regularly reflecting on the team's processes and
  practices to identify areas for improvement.
- **Osmotic Communication:** Encouraging open communication and collaboration
  among team members to share knowledge and ideas.
- **Personal Safety:** Creating a safe and supportive environment for team
  members to express their ideas and concerns.
- **Focus:** Focusing on delivering value to the customer and ensuring that the
  software meets their needs and expectations.
- **Easy Access to Expert Users:** Ensuring that team members have easy access to
  expert users or stakeholders to clarify requirements and gather feedback.
- **Technical Excellence:** Promoting technical excellence and high-quality code
  through practices such as pair programming, test-driven development, and
  continuous integration.

### FDD

Feature Driven Development (FDD) is an agile methodology that focuses on
delivering working software in a feature-driven manner. It is based on the
principle of delivering small, incremental features that provide value to the
customer.

FDD emphasizes the importance of modeling and design, and it uses a feature
list to prioritize and manage the development process. FDD is particularly
suitable for large-scale projects with complex requirements, as it provides a
structured approach to managing the development process while still allowing for
flexibility and adaptability.

Core practices of FDD include:

- **Domain Object Modeling:** Creating a model of the domain to understand the
  requirements and design the software.
- **Developing by Feature:** Breaking down the project into small, manageable
  features that can be developed and delivered incrementally.
- **Individual Class(Code) Ownership:** Assigning ownership of individual classes
  to specific developers, allowing them to take responsibility for the code they
  write.
- **Feature Teams:** Forming small, cross-functional teams that are responsible
  for delivering specific features.
- **Inspections**: Conducting regular inspections of the code to ensure quality and
  adherence to standards.
- **Regular Builds:** Building the software regularly to ensure that it is
  always in a working state and to detect issues early.
- **Configuration Management:** Managing the configuration of the software to
  ensure that it is consistent and reliable.
- **Reporting/Visibility of Results:** Providing visibility into the progress
  of the project and the status of the features being developed.

Additional practices of FDD include:

- **Start Small:** Starting with a small, manageable project to gain experience
  and build confidence in the methodology.
- **Keep Features Short and Sweet:** Developing features that are small and
  focused, making it easier to deliver value quickly and gather feedback.
- **Automate Testing and Integration:** Automating the testing and integration
  processes to ensure that the software is always in a working state and to
  reduce manual effort.
- **Use Collaborative Tools:** Using collaborative tools to facilitate
  communication and collaboration among team members.
- **Regularly Revisit the Domain Model:** Regularly reviewing and updating the
  domain model to ensure that it remains relevant and accurate as the project
  evolves.
- **Encourage Continuous Feedback:** Encouraging continuous feedback from
  stakeholders and users to ensure that the software meets their needs and
  expectations.
- **Prioritize Features:** Prioritizing features based on their value to the
  customer and the business, ensuring that the most important features are
  developed first.

### Kanban

One of the simplest agile methodology frameworks, Kanban has been around for
almost a century. It was originally developed by Toyota in the 1940s to improve
manufacturing efficiency, but has since been adapted for software development.

Kanban focuses on visualizing the flow of work, limiting work in progress, and
managing flow. It uses a Kanban board to visualize the work items and their
status, allowing teams to see what work is in progress, what work is completed,
and what work is yet to be done. The Kanban board typically consists of columns
representing different stages of the workflow, such as "To Do," "In Progress,"
"Testing," and "Done." Work items are represented by cards that move across the
board as they progress through the workflow.

![Kanban Board Example](https://i.postimg.cc/cHfhk8p8/image.png)

Kanban vs Lean:

Kanban and Lean are related methodologies focused on improving efficiency
and reducing waste in processes, particularly in manufacturing and software
development. Lean is a broader philosophy focused on maximizing value for
the customer while minimizing waste, and Kanban is a visual system that helps
manage workflow within a Lean environment. Essentially, Kanban is a tool that
can be used to implement Lean principles.

## Hybrid Models

There are many different Hybrid methodologies that integrate feedback mechanisms
into the traditional Waterfall model. This mitigates technical and functional
shortcomings in the original design that are discovered during development and
can be more quickly incorporated. Some of the more popular Hybrid models include:

- V-Model
- Spiral Model
- Iterative and Incremental Model

### V-Model Model

The V-Model is an extension of the Waterfall Model that emphasizes the
importance of verification and validation at each stage of the software
development lifecycle. It is called the V-Model because the development process
is represented as a V-shape, with the left side representing the stages of
development and the right side representing the stages of testing and
validation.

![V-Model](https://i.postimg.cc/YCfnfSGS/image.png)

### Spiral Model

Spiral Model is a risk-driven process model that combines the iterative nature
of the Incremental Model with the systematic aspects of the Waterfall Model.

![Spiral Model](https://i.postimg.cc/j5h3cFn7/image.png)

The Spiral Model is designed to address the limitations of the Waterfall Model
by allowing for iterative development and risk management. It is particularly
suitable for large, complex projects where requirements may change over time.

The Spiral Model consists of the following phases:

- **Planning:** Identify objectives, constraints, and risks for the project.
- **Risk Analysis:** Identify and analyze risks associated with the project.
- **Engineering:** Develop and implement the software based on the requirements
  and design.
- **Evaluation:** Evaluate the software against the requirements and gather
  feedback from stakeholders.

The iterative nature of the Spiral model makes it an early example of a Hybrid
Waterfall-Agile methodology and follows many characteristics (prototypes,
experiments/spike solutions) that exist in other more recent pure Agile
methodologies such as Scrum, XP, and AUP.

### Iterative and Incremental Model

The Iterative and Incremental Model is a software development methodology that
combines the principles of iterative development and incremental delivery. It
focuses on delivering small, functional increments of software in a series of
iterations, allowing teams to gather feedback and make adjustments as needed.

![Iterative and Incremental Model](https://i.postimg.cc/3xQH2HCy/image.png)

**Incremental Build Model** focuses on delivering functional components in parts,
while **Iterative and Incremental Model** combines that with continuous refinement
of existing components. They are related but not equivalent — the latter better
reflects Agile practices.

## References

- [Scrum in under 5 minutes](https://www.youtube.com/watch?v=2Vt7Ik8Ublw)
- [Solutions Methodologies](https://www.inflectra.com/Solutions/Methodologies/)
- [Story points: Estimation guide for user stories in Agile](https://asana.com/resources/story-points)
- [Development, testing, acceptance and production](https://www.wikiwand.com/en/articles/Development,_testing,_acceptance_and_production)
- [The Workstream](https://www.atlassian.com/work-management)
- [Agile Manifesto](https://agilemanifesto.org/)
