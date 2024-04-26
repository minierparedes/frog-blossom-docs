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

Dev team:

- [sharray2918](https://github.com/sharray2918)
- [minierparedes](https://github.com/minierparedes)

## 4. System Overview

### 4.1 High-Level Description

The Frog Blossom CMS is a content management system designed to empower users to create, manage, and publish digital content effectively.

At its core, the system provides a user-friendly interface for content creation, organization, and publication, catering to the needs of content creators, editors, administrators, and website visitors.

#### Functionality

1. **Content Creation and Editing**:
   - Users can create various types of content, including articles, blog posts, pages, and multimedia content.
   - Content creation interfaces support rich text formatting, media embedding, and metadata management.

2. **Content Management**:
   - Content is organized using categories, tags, and custom taxonomies for easy navigation and retrieval.
   - Users can search, filter, and sort content based on criteria such as publication date, author, and topic.

3. **Media Management**:
   - Users can upload, store, and manage media files, such as images, videos, and documents, within the system.
   - Media files can be embedded into content and reused across multiple pages or posts.

4. **Version Control and Revision History**:
   - The system maintains a revision history of content changes, allowing users to track and revert to previous versions if needed.
   - Version control mechanisms ensure data integrity and facilitate collaboration among multiple users.

5. **Publishing Workflow**:
   - Users can schedule content publication, preview changes before publishing, and collaborate on content creation and review.
   - Role-based access control allows administrators to define user roles and permissions for content publishing and management.

6. **User Management**:
   - The system supports user registration, authentication, and role-based access control, allowing administrators to manage user accounts and permissions.

7. **SEO Optimization**:
   - Users can optimize content for search engines by setting metadata, such as titles, descriptions, and keywords, for each piece of content.
   - Clean URLs, canonical tags, and SEO-friendly markup are employed to improve search engine rankings and visibility.

#### Components

1. **Frontend**:
   - The frontend component provides an interface for interacting with the CMS, allowing users to create, edit, and manage content.

2. **Backend**:
   - The backend component implements the core business logic of the CMS, including content management, user authentication, and access control.

3. **Database**:
   - The database component stores and manages content data, user information, and system configurations.

4. **Media Storage**:
   - Media files uploaded by users are stored in a dedicated storage component, such as a file system or cloud storage service, for efficient retrieval and management.

5. **Search Engine**:
   - A search engine component indexes and searches content to provide users with fast and relevant search results.
   - Full-text search capabilities and faceted search options may be implemented to enhance search functionality.

## 5. Architectural Strategies

### 5.1 Key Strategies

The Frog Blossom CMS application adopts several key architectural strategies to address specific stakeholder concerns and achieve the desired system objectives.

1. **Modularization and Separation of Concerns**:
   - **Strategy**: The system is designed using Clean Architecture principles, which promote modularization and separation of concerns. Each component of the system (Entities, Use Cases, Interface Adapters, and Frameworks/Drivers) has well-defined responsibilities and boundaries, allowing for easy maintenance, scalability, and testability.
   - **Addressing Stakeholder Concerns**:
     - **Developers**: Clear separation of concerns facilitates code maintenance, reduces complexity, and promotes code reuse, enhancing developer productivity.

2. **Microservices Architecture**:
   - **Strategy**: The system adopts a Microservices architecture, decomposing complex functionalities into smaller, independently deployable services. Each microservice is responsible for a specific business capability, enabling scalability, fault isolation, and technological flexibility.
   - **Addressing Stakeholder Concerns**:
     - **Developers**: Microservices architecture promotes agility, allowing developers to work on smaller, focused components independently. It also facilitates technology heterogeneity, enabling the use of different programming languages, frameworks, and databases for individual microservices.

3. **Containerization and Orchestration**:
   - **Strategy**: The system leverages containerization technologies, such as Docker, to package and deploy microservices as lightweight, portable containers. Container orchestration platforms, such as Kubernetes, are used to automate deployment, scaling, and management of containerized applications.
   - **Addressing Stakeholder Concerns**:
     - **Developers**: Containerization streamlines the development and deployment process, providing consistency across different environments (development, testing, production). It also facilitates continuous integration and continuous deployment (CI/CD) pipelines, enabling faster delivery of features and updates.

4. **Security by Design**:
   - **Strategy**: Security considerations are embedded into the architecture and design of the system from the outset. Security best practices, such as encryption, authentication, authorization, and data validation, are implemented at every layer of the application to protect against unauthorized access, data breaches, and other security threats.

## 6. System Architecture

### 6.1 Overview of Layers/Modules

Provide an overview of the system's layers or modules.

### 6.2 Component Diagrams

Include any relevant component diagrams that illustrate significant parts of the system.

### 6.3 Database Design

Outline the database design and structure.

## 7. Quality Attributes

### 7.1 Performance

Describe the performance requirements and how the architecture supports them.

### 7.2 Scalability

Discuss scalability considerations and strategies.

### 7.3 Security

Outline the security measures and considerations within the architecture.

### 7.4 Maintainability

Discuss how the system is designed for ease of maintenance.

## 8. Appendices

### 8.1 Revision History

Document the revision history of this document.
