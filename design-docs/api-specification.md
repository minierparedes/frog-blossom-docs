# API Specification

This API specification provides endpoints for creating, retrieving, updating, and deleting users and articles in the CMS application. Each endpoint follows RESTful conventions and uses appropriate HTTP methods and request/response formats.

1. **Create User**
   - `POST /api/users`
   - Request Body:

     ```json
     {
         "username": "string",
         "email": "string",
         "password": "string",
         "role": "string"
     }
     ```

   - Response:
     - Status Code: 201 Created
     - Body: The created user object

2. **Get User by ID**
   - `GET /api/users/{userId}`
   - Response:
     - Status Code: 200 OK
     - Body: The user object with the specified ID

3. **Create Article**
   - `POST /api/articles`
   - Request Body:

     ```json
     {
         "title": "string",
         "content": "string",
         "author": "string",
         "createdAt": "date",
         "updatedAt": "date"
     }
     ```

   - Response:
     - Status Code: 201 Created
     - Body: The created article object

4. **Get Article by ID**
   - `GET /api/articles/{articleId}`
   - Response:
     - Status Code: 200 OK
     - Body: The article object with the specified ID

5. **Update Article**
   - `PUT /api/articles/{articleId}`
   - Request Body:

     ```json
     {
         "title": "string",
         "content": "string",
         "updatedAt": "date"
     }
     ```

   - Response:
     - Status Code: 200 OK
     - Body: The updated article object

6. **Delete Article**
   - `DELETE /api/articles/{articleId}`
   - Response:
     - Status Code: 204 No Content
