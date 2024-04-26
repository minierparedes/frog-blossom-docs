# Frog Blossom CMS Architectual plan

## 1. Introduction

### 1.1 Purpose

This document outlines the architectual plan for the minimun viable product (MVP) of the Frog Blossom CMS application. <br>
It's intended for Dev team. <br>
It is to be used as an initial guide for the development and future enhancements


### 1.2 Scope
The scope of the Frog Blossom CMS Architectural Plan encompasses the following areas:

- Core Functionality
- User Management
- Content Management
- Media Management
- Version Control
- Publishing Workflow
- User Experience
- Scalability and Extensibility
- Security

### 1.3 Definitions, Acronyms, and Abbreviations
Provide definitions for any terms and acronyms used throughout the document.

### 1.4 References
List any other documents, websites, or materials referenced in this document.

- [The Ultimate Guide to Headless CMS](https://www.enonic.com/headless-cms-ultimate-guide#challenges)
- [Structured Content](https://www.enonic.com/blog/what-is-structured-content)
- [Content Modeling 101](https://www.enonic.com/resources/guides/healthcare-content-modeling-101)
- [Clean Architecture and DDD](https://medium.com/bimar-teknoloji/understanding-clean-architecture-and-domain-driven-design-ddd-24e89caabc40)
- [Nuxt](https://nuxt.com/docs/getting-started/introduction)
- [Expressjs](https://expressjs.com/)
- [GO](https://go.dev/doc/)
- [PostgresSQL](https://www.postgresql.org/docs/current/)
- [Docker](https://docs.docker.com/)


### 2. Architectural Representation

#### 2.1 Architectural Style and Rationale

**Architectural Style:** Clean Architecture and Microservices

**Rationale:**

1. **Clean Architecture for Backend**:
   - The choice of Clean Architecture for the backend is based on its effectiveness in promoting separation of concerns, maintainability, and testability of the codebase. 
   - Clean Architecture organizes the codebase into layers (Entities, Use Cases, Interface Adapters, and Frameworks/Drivers), with clear boundaries and dependencies flowing inward. <br>
    This architectural style facilitates decoupling of business logic from external dependencies, such as databases, frameworks, and user interfaces.
   - With Clean Architecture, the core business logic (Use Cases) is at the center of the architecture, independent of the infrastructure.

2. **Microservices**:
   - The choice of Microservices architecture complements Clean Architecture by providing a scalable approach to building distributed systems.
   - Microservices architecture decomposes the system into a set of independently deployable services, each responsible for a specific business capability. <br> 
   This allows for better scalability, fault isolation, and flexibility in technology choice for individual services.
   - By adopting a Microservices approach, we aim to address potential scalability and maintainability challenges, allowing for more efficient development, deployment, and management of the CMS application.
   - Microservices architecture aligns with industry best practices and standards for building modern, cloud-native applications, making it a suitable choice for the Frog Blossom CMS application.

## 3. System Stakeholders and Concerns

### 3.1 Stakeholders
List the stakeholders of the system and their interests/concerns.

### 3.2 System Concerns
Describe the concerns of the system, such as performance, scalability, and security.

## 4. System Overview

### 4.1 High-Level Description
Provide a high-level description of the system's functionality and components.

## 5. Architectural Strategies

### 5.1 Key Strategies
Describe the key architectural strategies and how they address specific stakeholder concerns.

## 6. System Architecture

### 6.1 Overview of Layers/Modules
Provide an overview of the system's layers or modules.

### 6.2 Component Diagrams
Include any relevant component diagrams that illustrate significant parts of the system.

### 6.3 Database Design
Outline the database design and structure.

## 7. Key Architectural Decisions

### 7.1 Decision Log
Record key architectural decisions made and the rationale behind them.

## 8. Quality Attributes

### 8.1 Performance
Describe the performance requirements and how the architecture supports them.

### 8.2 Scalability
Discuss scalability considerations and strategies.

### 8.3 Security
Outline the security measures and considerations within the architecture.

### 8.4 Maintainability
Discuss how the system is designed for ease of maintenance.

## 9. Risks and Technical Debt

### 9.1 Identified Risks
List any identified risks and their potential impact on the project.

### 9.2 Technical Debt
Discuss any areas of technical debt and plans for resolution.

## 10. Appendices

### 10.1 Glossary
Provide a glossary of terms used throughout the document.

### 10.2 Index
Include an index of terms and sections for easy navigation.

### 10.3 Revision History
Document the revision history of this document.