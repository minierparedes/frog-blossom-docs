# Frog Blossom CMS

<img src="image.png" alt="frog-blossom" style="display: block; margin:auto; width:50%;">

A web-based CMS (content management system) system that allows users to create websites, manage, and publish digital content without needing extensive technical knowledge.
Users can create websites and edit content through a user-friendly interface, and the system manages the storage, retrieval, and presentation of content on the website.

## Application Features

### Website Creation

- Website builder
- Interface
  - Contact form (curretly one, plans on creating several types of forms)
- Page
  - included meta tags
- Templates
- Flexible layout options

### Content Management

- Content creation
  - article
    - included meta tags
  - categories
  - author
    - for meta `<meta name="author" content="John Doe">`
- Editing
- Organization
- Publishing

### User Management

- User authentication
- User roles and permissions
- Account management

---

## Table of contents

- [Frog Blossom CMS](#frog-blossom-cms)
  - [Application Features](#application-features)
    - [Website Creation](#website-creation)
    - [Content Management](#content-management)
    - [User Management](#user-management)
  - [Table of contents](#table-of-contents)
    - [docs](#docs)
  - [Tech Stack](#tech-stack)
  - [Application architecture](#application-architecture)
    - [Project Structure](#project-structure)
  - [Running Locally](#running-locally)
    - [Run with Docker](#run-with-docker)
  - [Diagrams](#diagrams)
    - [System Context](#system-context)
    - [Container](#container)
    - [Revision History](#revision-history)

### docs

1. [Application requirements](/frog-blossom-cms/application-requirements.md)
2. [Design documents](/design-docs/)
3. [API specification](/design-docs/api-specification.md)

## Tech Stack

Frontend:

1. Nuxtjs
2. CSS/Sass
3. Expressjs

Backend:

1. GO

Database:

1. PostgreSQL

Container:

1. Docker

---

## Application architecture

Go application following the Hexagonal Architecture with a structure similar to Spring Boot's layers

### Project Structure

```bash
├── cmd
│   └── main.go
├── internal
│   ├── application
│   │   ├── service.go
│   ├── adapter
│   │   ├── inbound
│   │   │   ├── http
│   │   │   │   └── handler.go (Equivalent to Controller)
│   │   ├── outbound
│   │   │   └── persistence
│   │   │       └── repository.go (Equivalent to Repository)
│   ├── domain
│   │   └── model.go (Equivalent to Model)
│   └── config
│       └── appconfig.go
└── test
    ├── unit_tests
    └── end_to_end_tests
```

In this structure:

- `cmd`: Contains the main executable code (`main.go`) for the application.
- `internal`: Contains internal packages/modules that are not intended to be used by external packages. This includes `application`, `adapter`, `domain`, and `config`.
  - `application`: Contains business logic or services (`service.go`).
  - `adapter`: Contains adapters for inbound and outbound communication.
    - `inbound`: Contains adapters for handling incoming requests, such as HTTP handlers (`handler.go`, equivalent to Controller).
    - `outbound`: Contains adapters for external systems, such as database repositories (`repository.go`, equivalent to Repository).
  - `domain`: Contains domain-specific logic and models (`model.go`, equivalent to Model).
  - `config`: Contains configuration files or structures (`appconfig.go`).
- `test`: Contains test-related code, including unit tests, integration tests, and test utilities.
  - `unit_tests`: Testing individual components or units of code in isolation.
  - `end_to_end_tests`: Testing the application's behavior across multiple components or systems. Tests user scenarios and interactions with the entire application.

## Running Locally

### Run with Docker

## Diagrams

### System Context

![systen context diagram](/design-docs/sys-context-diagram.png)

### Container

![container diagram](/design-docs/containers-diagram.png)

### Revision History

| Date       | Version | Description of Changes              | Author |
|------------|---------|------------------------------------|--------|
| 2024-04-26 | 1.0     | Initial draft of document          | @minierparedes    |
| 2024-04-30 | 1.1     | Creat C4 Model Diagrams            | @minierparedes    |
| 2024-04-30 | 1.1     | Create API specification/project structure  | @minierparedes    |
| 2024-05-01 | 1.2     | TODO: [website creation: static vs SPA](https://reflectionizm.slack.com/archives/D06FJ2S89FC/p1714530340845169)  | @minierparedes    |
| 2024-05-01 | 1.2     | TODO: C4 Model Diagrams: sequence | @minierparedes    |
| 2024-05-02 | 1.2     |scenario walkthough | @minierparedes    |
| 2024-05-10 | 1.2     |frog-blossom-db schema v.4 | @minierparedes    |

