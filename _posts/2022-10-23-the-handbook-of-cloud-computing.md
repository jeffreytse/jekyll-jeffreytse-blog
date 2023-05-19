---
layout: post
title: The Handbook of Cloud Computing
author: Jeffrey Tse
banner:
  image: https://user-images.githubusercontent.com/9413601/225839062-684f6f8c-2dd8-4d75-ad42-877c91cf3114.png
  opacity: 0.80
categories:
  - computer
tags:
  - software
  - cloud
  - note
---

## What's Cloud Computing?

Cloud computing is the practice of using network of remote servers hosted on the
Internet to store, manage, and process data, rather than a local server or a
personal computer.

- On-Premise
- Cloud-Providers

Different cloud system architectures include:

- Multi-cloud
- Hybrid cloud
- Single cloud
- Public cloud
- Private cloud

## Cloud Computing Technologies

- Compute
- Network
- Storage

## Cloud Computing Services

### Global Infrastructure

- Steadily expanding global infrastructure to help customers achieve lower
  latency and higher throughput
- Categories
  - Region
    - A physical location in the world with multiple Availability Zones
  - Availability Zone
    - One or more discrete data centers
  - Edge Location
    - A data center own by a trusted partner of Cloud Service Provider

### Computing Layers

- Application
- Data
- Runtime Environment
- Middleware
- OS
- Virtualization
- Server
- Storage
- Network

### Service Models for Cloud Computing

- Traditional IT (On-Premises)
- Cloud Services
  - IaaS (Infrastructure as a Service)
    - The basic building blocks for cloud IT. Provides access to networking
      features, computers and data storage space.
    - Don't worry about IT staff, data centers and hardware.
    - Examples
      - AWS
      - Google Cloud Platform
      - Microsoft Azure
      - Huawei Cloud
      - ...
    - For Architects/Admins
  - PaaS (Platform as a Service)
    - Removes the need for your organization to manage the underlying
      infrastructure. Focus on the development and management of your
      applications.
    - Don't worry about provisioning, configuring or understanding the
      hardware or OS.
    - Examples
      - Heroku
      - ...
    - For Developers
  - SaaS (Software as a Service)
    - A completed product that is run and managed by the server provider.
    - Don't worry about how the service is maintained, it just works and
      remains available.
    - Examples
      - Salesforce
      - Office 365
      - GMail
      - ...
    - For End Users/Customers

![Cloud Services](https://user-images.githubusercontent.com/9413601/226162679-51ef4c8d-7730-4e03-ac55-2b950a59a1b7.png)

![Cloud Service Comparisons](https://user-images.githubusercontent.com/9413601/226164550-96df4ea2-b461-4f93-a9f0-7f7170529b04.png)

### Deployment Models for Cloud Computing

- On-Premise (Private Cloud)
  - Deploying resources on-premises, using virtualization and resource
    management tools, is sometimes called "private cloud".
- Cloud (Public Cloud)
  - Fully utilizing cloud computing
  - Virtual Private Cloud (VPC)
- Hybrid
  - Using both Cloud and On-Premise

### Elastic Computing (EC) Pricing Models

- On-Demand
  - Lease commitment
- Reserved Instances (RI)
  - Best long-term value
  - Reduced Pricing = Term × Class Offering × Payment Option
  - Terms
    - 1 Year
    - 3 Year
    - ...
  - Class Offering
    - Standard
      - Cannot change RI Attributes
    - Convertible
      - Allow you to change RI Attributes if greater or equal in value
    - Scheduled
      - You reserve instances for specific time periods e.g. once a week for a
        few hours
- Spot Pricing
  - Biggest Saving
  - Request spare computing capacity
  - Flexible start and end times
- Dedicated Hosting
  - Most Expensive
  - Dedicated servers
  - Isolate hardware (enterprise requirements)
    - Single Tenant (Physical Isolation)
    - Multi-Tenant (Virtual Isolation)
  - Can be on-demand or reserved

## Cloud Network Services

- Virtual Networks
  - Bridge
  - Network Address Translation (NAT)
  - Virtual Switch
    - Open vSwitch (OVS)
    - Enhance vSwitch (EVS)
    - Distributed Virtual Switch (DVS)
- Cloud Network Services
  - Virtual Private Cloud (VPC)
  - NAT Gateway
  - Elastic IP (EIP)

![AWS Networking](https://user-images.githubusercontent.com/9413601/226179279-5986b703-7661-4b67-8835-92906b72e4d4.png)

## Cloud Storage Services

- Mainstream Storage Types
  - Block Storage
  - File Storage
    - CIFS
    - NFS
  - Object Storage
- Cloud Storage Services
  - EVS: Elastic Volume Service
  - SFS: Scalable File Service
  - OBS: Object Storage Service

## Organizations and Accounts

- Organizations
- Root Account User
  - A single sign-in identity that has complete access to all AWS services and
    resources in an account
  - Each account has a root account user
- Organization Units
  - A group of AWS accounts within an organization which can also contain other
    organizational units, creating a hierarchy
- Service Control Policies
  - Gives central control over the allowed permissions for all accounts in your
    organization, helping to ensure your account stay within your organization's
    guidelines

## Acronyms and Abbreviations

- APP: Application
- AS: Auto Scaling
- CPU: Central Processing Unit
- CCE: Cloud Container Engine
- CCI: Cloud Container Instance
- CIFS: Common Internet File System
- ECS: Elastic Cloud Server
- EIP: Elastic IP
- EVS: Elastic Volume Service
- GPU: Graphics Processing Unit
- ICT: Information and Communications Technology
- I/O: Input/Output
- IaaS: Infrastructure as a Service
- IBM: International Business Machines Corporation
- KVM: Kernel-based Virtual Machine
- IMS: Image Management Service
- LXC: Linux Container
- LVM: Logical Volume Manager
- NAT: Network Address Translation
- NFS: Network File System
- NIC: Network Interface Card
- NIST: National Institute of Standards and Technology
- OS: Operation System
- OBS: Object Storage Service
- PC: Personal Computer
- PaaS: Platform as a Service
- RAID: Redundant Arrays of Independent Disks
- SFS: Scalable File Service
- SWR: Software Repository for Container
- SOAP: Simple Object Access Protocol
- SaaS: Software as a Service
- TCO: Total Cost of Ownership
- TAP: Test Access Point
- VM: Virtual Machine
- VLAN: Virtual Local Area Network
- VPC: Virtual Private Cloud
