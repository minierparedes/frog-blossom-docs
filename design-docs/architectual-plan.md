# Frog Blossom CMS Architectual plan

## 1. Introduction

### 1.1 Purpose

This document outlines the architectual plan for the minimun viable product (MVP) of the Frog Blossom CMS application.

It's intended for Dev team.

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
- [Hexagonal Architecture in Go](https://dev.to/bagashiz/building-restful-api-with-hexagonal-architecture-in-go-1mij)
- [Github: Hexagonal Architecture in Go](https://github.com/felipewom/go-hexagonal)
- [Github: go-hexagonal-api](https://github.com/sergicanet9/go-hexagonal-api)
- [Nuxt](https://nuxt.com/docs/getting-started/introduction)
- [Expressjs](https://expressjs.com/)
- [GO](https://go.dev/doc/)
- [PostgresSQL](https://www.postgresql.org/docs/current/)
- [Docker](https://docs.docker.com/)

### 2. Architectural Representation

#### 2.1 Architectural Style and Rationale

**Architectural Style:** Hexagonal architecture and Microservices

**Rationale:**

**Hexagonal architecture & Microservice for Backend**:

**Hexagonal:**

1. **Consistent:** The Hexagonal architecture and Microservices approach ensure a consistent structure and design throughout the application, making it easier to maintain and enhance over time.

2. **Easy to understand, navigate, and reason about:** The architecture's clear separation of concerns and modular design make it intuitive to comprehend, navigate, and reason about the codebase, facilitating efficient development and troubleshooting.

3. **Easy to change, loosely-coupled:** By decoupling components and defining clear interfaces, the architecture allows for changes to be made in one part of the system without affecting others. This loose coupling enhances flexibility, enabling rapid adaptation to evolving requirements.

4. **Easy to test:** The architecture's modularity and clear boundaries between components facilitate unit testing, integration testing, and end-to-end testing. This ease of testing ensures that the system's behavior can be verified reliably, leading to improved quality and stability of the application.

**Microservices:**

1. The choice of Microservices architecture complements Hexagonal Architecture by providing a scalable approach to building distributed systems.

2. Microservices architecture decomposes the system into a set of independently deployable services, each responsible for a specific business capability.

### Hexagonal architecture layer structure:

- **Domain Layer:** Contains the core business logic and domain models.
- **Application Layer:** Orchestrates use cases and interacts with the domain layer.
- **Infrastructure Layer:** Provides implementations for external dependencies.
- **Interface Layer:** Defines interfaces for external communication.

1. **Domain Layer:** This layer contains the core business logic and domain models of the application. It defines the entities, value objects, business rules, and domain services that represent the business domain.

2. **Application Layer:** Also known as the use case layer, this layer orchestrates the interactions between the domain layer and the external interfaces (such as HTTP handlers or CLI commands). It contains the application-specific use cases or operations that are performed by the system.

3. **Infrastructure Layer:** This layer provides implementations for external dependencies and interfaces required by the application, such as databases, external services, or frameworks. It includes repositories, adapters, and drivers that interact with external systems.

4. **Interface Layer:** This layer defines the interfaces through which the application communicates with external systems or users. It includes handlers, controllers, or CLI interfaces that translate incoming requests into application use cases and outgoing responses.

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
4. **Search Engine**?[optional/Elastic Search]:
    - A search engine component indexes and searches content to provide users with fast and relevant search results.
    - Full-text search capabilities and faceted search options may be implemented to enhance search functionality.

## 5. Architectural Strategies

### 5.1 Key Strategies

The Frog Blossom CMS application adopts several key architectural strategies to address specific stakeholder concerns and achieve the desired system objectives.

- Frontend: Nuxt, expressjs, css, sass
- Backend: GO, Docker
- Database: Postgressql

1. **Modularization and Separation of Concerns**:
    - **Strategy**: The system is designed using Hexagonal architecture principles, which promote modularization and separation of concerns. Each component of the system (Domain Layer, Application Layer, Infrastructure Layer, and Interface Layer) has well-defined responsibilities and boundaries, allowing for easy maintenance, scalability, and testability.
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

Front-End Layer: Handles the user interface and client-side logic.
Back-End Layer: Manages server-side logic, API requests, and database interactions.
Database Layer: Stores and retrieves all application data.

### Backend

The Frog Blossom CMS application is structured using Hexagonal architecture principles the following is an overview of the system's layers/modules:

1. **Entities Layer**:
    - The Entities layer represents the core domain models and business entities of the system.
    - Entities encapsulate the essential data and behavior of the application, defining the fundamental building blocks of the domain.
    - Examples of entities include User, ContentItem, Category, Tag, MediaFile, etc.
2. **Use Cases Layer**:
    - The Use Cases layer contains the application's business logic and use cases, representing the operations and workflows performed by the system.
    - Use cases orchestrate interactions between entities and interface adapters to fulfill user requests and achieve system objectives.
    - Use cases are independent of external dependencies and infrastructure details, ensuring flexibility and testability.
    - Examples of use cases include CreateContent, EditContent, PublishContent, DeleteContent, AuthenticateUser, AuthorizeUser, etc.
3. **Interface Adapters Layer**:
    - The Interface Adapters layer serves as a bridge between the application's core business logic and external interfaces, such as the user interface (UI), databases, and third-party services.
    - Interface adapters translate data and requests between different formats and protocols, ensuring compatibility and interoperability.
    - Interface adapters include presenters, controllers, gateways, repositories, and data mappers.
    - Examples of interface adapters include REST API controllers, database repositories, authentication gateways, view models, etc.
4. **Frameworks/Drivers Layer**:
    - The Frameworks/Drivers layer represents external frameworks, libraries, and infrastructure components used by the application.
    - Frameworks and drivers provide essential services and resources needed to run the application, such as web servers, databases, logging frameworks, authentication libraries, etc.
    - Frameworks/drivers encapsulate implementation details and infrastructure dependencies, allowing the application to remain agnostic to specific technologies.
    - Examples of frameworks/drivers include Spring Boot, Hibernate, PostgreSQL, Docker, Kubernetes, etc.

The modular architecture of the Frog Blossom CMS application facilitates loose coupling, high cohesion, and ease of maintenance. Each layer/module has well-defined responsibilities and dependencies, enabling independent development, testing, and deployment of components.

### Frontend

- PENDING

### 6.2 Component Diagrams

[View on canvas](https://app.eraser.io/workspace/toYCWH32PtHug7boDCpu?elements=uLJZYCk-993brxu0T6YIeQ)

### 6.3 Database Design

#### Database Tables

1. **Users Table**:
    - Stores user information such as username, email, password (hashed), role, and permissions.
    - Primary Key: user_id
2. **Content Table**:
    - Contains details about content items such as articles, blog posts, pages, etc.
    - Includes fields for title, content body, author, publication date, status (draft/published), category, tags, etc.
    - Primary Key: content_id
    - Foreign Key: author_id (references Users table)
3. **Categories Table**:
    - Stores categories for organizing content.
    - Includes fields for category name and description.
    - Primary Key: category_id
4. **Tags Table**:
    - Stores tags associated with content items.
    - Includes fields for tag name and description.
    - Primary Key: tag_id
5. **Media Files Table**:
    - Stores metadata about uploaded media files (images, videos, documents, etc.).
    - Includes fields for file name, file type, file size, upload date, etc.
    - Primary Key: media_id
6. **Content-Category Mapping Table**:
    - Represents a many-to-many relationship between content items and categories.
    - Associates content items with one or more categories.
    - Foreign Keys: content_id (references Content table), category_id (references Categories table)
7. **Content-Tag Mapping Table**:
    - Represents a many-to-many relationship between content items and tags.
    - Associates content items with one or more tags.
    - Foreign Keys: content_id (references Content table), tag_id (references Tags table)

#### Database Relationships

- One-to-Many Relationship:
  - Users can have multiple content items (articles, blog posts, etc.).
  - Categories can have multiple content items.
  - Tags can be associated with multiple content items.
- Many-to-Many Relationship:
  - Content items can belong to multiple categories.
  - Content items can have multiple tags.

#### Database Indexes

- Indexes can be added on frequently queried columns such as username, email, category name, tag name, etc., to optimize query performance.

#### Database Constraints

- Foreign key constraints ensure data integrity by enforcing referential integrity between related tables.
- Check constraints can be applied to ensure data validity and consistency (e.g., ensuring publication date is not in the future).

## 7. Appendices

### 7.1 Revision History

### Revision History

| Date | Version | Description of Changes | Author |
| ----- | ----- | ----- | ----- |
| 2024-04-26 | 1.0 | Initial draft of document | @minierparedes   |
| 2024-04-30 | 1.1   | chage to hexagonal architecture | @minierparedes   |
