# 📚 Library Management API Documentation

## Overview
The Library Management API is designed to handle user authentication, registration, and book management, including adding and updating books and their authors. It uses Slim Framework for routing and Firebase JWT for authentication.

---

## Technologies Used
- **PHP**: Programming language for backend development.
- **Slim Framework**: Lightweight PHP framework for building APIs.
- **Firebase JWT**: Library for JSON Web Token (JWT) authentication.
- **Composer**: Dependency management for PHP projects.

---

## Setup Instructions

### Prerequisites
Ensure the following are installed on your system:
- PHP (version 7.4 or higher)
- Composer
- A web server (e.g., Apache or Nginx)

### Installation Steps
1. **Clone the Repository**
```bash
git clone <repository_url>
cd <project_directory>
```

2. **Install Slim Framework**
```bash
composer require slim/slim:3.*
```    
        
3. **Install Firebase JWT**
```bash
composer require firebase/php-jwt
```  

4. **Set Up the Application**
    - Navigate to the src folder and configure your application settings, such as database credentials and JWT secret keys.

5. **Start the Development Server**
```bash
php -S localhost:8000 -t public
```  

6 **Test the API**
    - Use tools like Thunder Client or Postman to test the API Endpoints.

## Endpoints

---

### 1. User Registration
**Endpoint:**  
`POST /user/register`  

**Description:**  
Registers a new user by creating a record in the `users` table.

**Request Payload:**  
```json
{
    "username": "exampleUser",
    "password": "examplePassword"
}
```
**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "data": null
}
```

**b. Error (400): If the username already exists:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Username already exists"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```


### 2. User Authentication
**Endpoint:**  
`POST /user/Authenticate`  

**Description:**  
Authenticates a user based on the provided credentials and generates a JWT token upon successful login.

**Request Payload:**  
```json
{
    "username": "User",
    "password": "Password"
}
```
**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "token": "generatedJWTToken",
    "data": null
}
```

**b. Error (401): If authentication fails:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Authentication Failed"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```

### 3. User Update
**Endpoint:**  
`PUT /user/update`  

**Description:**  
Updates the username and password for an authenticated user. Requires a valid JWT token in the `Authorization` header. 

**Request Payload:**  
```json
{
    "username": "newUsername",
    "password": "newPassword"
}
```

**Authorization:**  
Requires a Bearer Token in the Authorization header:
```makefile
Authorization: Bearer <JWT_TOKEN>
```

**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "new_token": "newJWTToken",
    "data": null
}
```

**b. Error (401)**  
```json
{
    "status": "fail",
    "data": {
        "title": "No token provided"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```


### 4.  Add New Book
**Endpoint:**  
`POST /books/add`

**Description:**  
This endpoint is used for adding a new book to the library system. It allows specifying multiple authors for the book. A valid JWT token is required for authentication.

**Request Payload:**  
```json
{
    "title": "Book Title",
    "authors": ["Author 1", "Author 2"]
}
```

**Authorization:**  
Requires a Bearer Token in the Authorization header:
```makefile
Authorization: Bearer <JWT_TOKEN>
```

**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "new_token": "newGeneratedJWTToken",
    "data": {
        "bookid": 123
    }
}
```

**b. Error (401)**  
```json
{
    "status": "fail",
    "data": {
        "title": "No token provided"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```

### 5.  Update an Existing Book
**Endpoint:**  
`PUT /books/update`

**Description:**  
This endpoint allows updating the details of an existing book, including its title and authors. A valid JWT token must be provided for authentication. Upon successful update, a new token is generated and returned.

**Request Payload:**  
```json
{
    "bookId": 123,
    "title": "Updated Book Title",
    "authors": ["Author 1", "Author 2"]
}
```

**Authorization:**  
Requires a Bearer Token in the Authorization header:
```makefile
Authorization: Bearer <JWT_TOKEN>
```

**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "new_token": "newGeneratedJWTToken",
    "data": {
        "bookid": 123
    }
}
```

**b. Error (401)**  
```json
{
    "status": "fail",
    "data": {
        "title": "No token provided"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```


### 6.  Delete an Existing Book
**Endpoint:**  
`DELETE /books/delete`

**Description:**  
This endpoint allows for deleting a book from the database, including its associated authors. A valid JWT token is required for authentication. After the operation, a new token is generated and returned to the user.

**Request Payload:**  
```json
{
    "bookId": 123
}
```

**Authorization:**  
Requires a Bearer Token in the Authorization header:
```makefile
Authorization: Bearer <JWT_TOKEN>
```

**Response:**

**a. Success(200):**  
```json
{
    "status": "success",
    "new_token": "newGeneratedJWTToken",
    "data": {
        "message": "Book deleted successfully"
    }
}
```

**b. Error (401)**  
```json
{
    "status": "fail",
    "data": {
        "title": "No token provided"
    }
}
```

**c. Error (500): If there is a database error:**  
```json
{
    "status": "fail",
    "data": {
        "title": "Error message from server"
    }
}
```


