# 📚 Library Management API Documentation

## Overview
The Library Management API is designed to handle user authentication, registration, and book management, including adding and updating books and their authors. It uses Slim Framework for routing and Firebase JWT for authentication.

---

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

**b. Success Response (200):**  
```json
{
    "status": "success",
    "data": null
}
```
