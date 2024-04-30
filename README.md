# Frog Blossom CMS

web-based platform that allows users to create, manage, and publish digital content without needing extensive technical knowledge.
Users can create and edit content through a user-friendly interface, and the system manages the storage, retrieval, and presentation of content on the website.

## application features

- content creation
- editing
- organization
- and publishing
- user management
- user authentication

---

## Table of contents

- [Frog Blossom CMS](#frog-blossom-cms)
  - [application features](#application-features)
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
3. [Architectual plan](/design-docs/)
4. [API specification](/design-docs/api-specification.md)

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

```go

📁 project-name
  📁 cmd
    📁 myapp
      📄 main.go
  📁 internal
    📁 application
      📄 service.go
    📁 adapter
      📁 inbound
        📁 http
          📄 handler.go (Equivalent to Controller)
      📁 outbound
        📁 persistence
          📄 repository.go (Equivalent to Repository)
    📁 domain
      📄 model.go (Equivalent to Model)
    📁 config
      📄 appconfig.go
```

- `cmd`: Contains the main executable code (`main.go`) for the application.
- `internal`: Contains internal packages/modules that are not intended to be used by external packages. This includes `application`, `adapter`, `domain`, and `config`.
  - `application`: Contains business logic or services (`service.go`).
  - `adapter`: Contains adapters for inbound and outbound communication.
    - `inbound`: Contains adapters for handling incoming requests, such as HTTP handlers (`handler.go`, equivalent to Controller).
    - `outbound`: Contains adapters for external systems, such as database repositories (`repository.go`, equivalent to Repository).
  - `domain`: Contains domain-specific logic and models (`model.go`, equivalent to Model).
  - `config`: Contains configuration files or structures (`appconfig.go`).

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
