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

## Testing Results (Postman Screenshots)

### 1. Register ADMIN User
Registering a new user with both `USER` and `ADMIN` roles.
![Register as Admin](<Image/Register as Admin.png>)

### 2. Login as ADMIN
Logging in as the admin user to retrieve the JWT token.
![Login as Admin](<Image/Login as Admin.png>)

### 3. Scenario 1: ADMIN can delete
Making a `DELETE` request with an ADMIN token returns `200 OK`.
![Delete Book With Admin Permission](<Image/Delete Book With Admin Permission.png>)

### 4. Scenario 2: USER cannot delete
Making a `DELETE` request with a regular USER token returns `403 Forbidden` (Access Denied).
![Delete Book With User Permission](<Image/Delete Book With User Permission.png>)

---

## Getting Started

### Prerequisites
- Java 21
- MongoDB (running on `localhost:27017`)
- Maven (included wrapper `./mvnw` inside the `bookstore_mongodb` folder)

### Running the Application
1. Start your MongoDB server.
2. Navigate to the project folder: `cd bookstore_mongodb`
3. Run the application using Maven:
   ```bash
   ./mvnw spring-boot:run
   ```



## Student:
An Nguyen -  AnNguyen0410@csu.fullerton.edu -  885598904
