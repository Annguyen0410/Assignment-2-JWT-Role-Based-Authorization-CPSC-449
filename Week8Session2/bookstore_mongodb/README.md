# Bookstore API - JWT Authentication & Role-Based Authorization

This project is an extension of the Bookstore API built with Spring Boot and MongoDB. It implements secure access using JWT (JSON Web Token) and role-based authorization to protect specific endpoints.

## Assignment Overview
The goal of this assignment was to implement role-based access control (RBAC) for the `DELETE` operation:
- **`GET /api/books`**: Publicly accessible.
- **`POST /api/books`**: Restricted to users with the `USER` role.
- **`DELETE /api/books/{id}`**: Restricted to users with the **`ADMIN`** role.

## Implementation Details

### 1. Delete Endpoint
Added a `DELETE` endpoint in `BookController.java` that:
- Accepts a book ID as a path variable.
- Returns `200 OK` with a success message if deleted.
- Returns `404 Not Found` if the ID does not exist.

### 2. Security Configuration
Updated `SecurityConfig.java` to:
- Define access rules for different HTTP methods.
- Require `ADMIN` authority specifically for `DELETE` requests.
- Added a custom `AccessDeniedHandler` to return a `403 Forbidden` status with a descriptive JSON body when an unauthorized user attempts a restricted operation.

### 3. Service Layer
Extended `BookService.java` with logic to verify book existence and perform deletion using the `BookRepository`.

## Getting Started

### Prerequisites
- Java 21
- MongoDB (running on `localhost:27017`)
- Maven (included wrapper `./mvnw`)

### Running the Application
1. Start your MongoDB server.
2. Run the application using Maven:
   ```bash
   ./mvnw spring-boot:run
   ```

## Testing with Postman

### Scenario 1: ADMIN Authorization
1. **Register** a user with `["USER", "ADMIN"]` roles at `/api/auth/register`.
2. **Login** at `/api/auth/login` to retrieve the JWT token.
3. **DELETE** a book at `/api/books/{id}` using the token in the `Authorization: Bearer <token>` header.
4. Result: `200 OK`.

### Scenario 2: USER Authorization (Forbidden)
1. **Register** a user with only `["USER"]` role.
2. **Login** to retrieve the token.
3. **DELETE** a book using this token.
4. Result: `403 Forbidden` with "Access Denied" message.
