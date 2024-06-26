# Design Document: frog-blossom CMS

## 1. Introduction

Development for frog-blossom content management system (CMS) for managing articles and blog posts. The frog-blossom CMS will provide basic functionality for creating, editing, and deleting content, as well as user authentication and authorization.

## 2. Architectural Overview

The frog-blossom CMS will follow a Hexagonal architecture and microservice, with a single backend server responsible for handling HTTP requests, managing data storage, and serving content to users. The frontend will be implemented using Nuxtjs.

## 3. Functional Requirements

### 3.1 Website Management

- Users can create new websites.
- Users can select and customize website templates.
- Users can customize website layouts.
- Users can integrate content into their websites.
- Users can manage domain settings.
- Users can optimize websites for SEO.

### 3.2 User Management

- Users should register new accounts.
- Users should log in to their accounts.
- Users should update their profile information.
- Admin users should manage user accounts (CRUD operations).

### 3.3 Content Management

- Authenticated users can create new content.
- Authenticated users can edit existing content.
- Authenticated users can delete content they own.
- Admin users can manage all content (CRUD operations).

## 4. Non-Functional Requirements

- Performance: The system should handle concurrent requests to minimize serve latency.
- Security: User authentication should be secure and protect against security threats such as cross-site scripting (XSS) and SQL injection.

## 5. System Design

### 5.1 Backend

- The backend will be implemented using GO.
- Data storage will be handled using PostgresSQL.
- Authentication will be implemented using JSON Web Tokens (JWT).
- RESTful API endpoints will be exposed for user and content management.

### 5.2 Frontend

- The frontend will be implemented using NuxtJs.
- User interface components will be styled using CSS and Sass.
- API requests will be made to the backend using Express.

## 6. Data Model

simplified!!

### 6.1 Website

- `name: String (required)`
- `domain: String (required)`
- `owner_id: String (required)`
- `password: String`
- `template_id: String`
- `pages: Array`
  - `page_id: String`
  - `title: String`
  - `content: String`
  - `url: String`

### 6.2 User

- `username: String (required)`
- `email: String (required)`
- `password: String (required, hashed)`
- `role: String (default: "user" or "admin")`

### 6.3 Content

- `title: String (required)`
- `content: Object (required)`
- `author: ObjectId (referring to User)`
- `meta_tags: Array`
  - `name: String`
  - `content: String`
- `createdAt: Date (default: current timestamp)`
- `updatedAt: Date`

## 7. Technical Specifications

- Backend: `GO v1.22, PostgresSQL v15`
- Frontend: `Nuxtjs v3.11.2, sass v1.75.0, Express v4.19.2`

## 8. API Specifications

[documentation](/design-docs/api-specification.md)

## 9. Security Considerations

- User passwords should be securely hashed using crypt hashing algorithm.
- JWT tokens should be signed using a strong cryptographic key.
- Input validation and sanitization should be performed on all user-supplied data to prevent injection attacks.

## 10. Deployment and Infrastructure

- The system will be deployed to : CloudFlare?, AWS?.
- Continuous integration and deployment (CI/CD) pipelines will be set up using tools such as GitHub Actions.

## 11. Testing Strategy

- Unit tests will be written.
- Integration tests will be for the frontend and backend components.

---

### Revision History

| Date       | Version | Description of Changes              | Author |
|------------|---------|------------------------------------|--------|
| 2024-04-26 | 1.0     | Initial draft of document          | @minierparedes    |
| 2024-05-01 | 1.1     | Added data model management section| @minierparedes     |