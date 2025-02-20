# 📌 API Methods

This document details the available **Customer API** methods, including their endpoints, descriptions, and usage examples.

---

## 🎯 **API Endpoints Summary**

| **Method**  | **Endpoint**         | **Description**               |
|------------|----------------------|-------------------------------|
| **GET**    | `/v1/customers`      | Retrieves all customers      |
| **GET**    | `/v1/customers/{id}` | Retrieves a customer by ID   |
| **POST**   | `/v1/customers`      | Creates a new customer       |
| **PUT**    | `/v1/customers/{id}` | Updates an existing customer |
| **DELETE** | `/v1/customers/{id}` | Deletes a customer           |

---

## 📌 **1. Get All Customers**
### **Endpoint:** `GET /v1/customers`
### **Description:**
Retrieves a list of all registered customers.

### **Example Request:**

```http
GET /v1/customers HTTP/1.1
Host: localhost:5000
Content-Type: application/json
```

### **Example Response:**

```json
[
    {
        "id": 1,
        "name": "John Doe",
        "email": "john@example.com",
        "phone": "123-456-7890",
        "cpf": "123.456.789-00"
    },
    {
        "id": 2,
        "name": "Jane Doe",
        "email": "jane@example.com",
        "phone": "987-654-3210",
        "cpf": "987.654.321-00"
    }
]
```

---

## 📌 **2. Get Customer by ID**
### **Endpoint:** GET /v1/customers/{id}
### **Description:**

Retrieves a specific customer by ID.

### **Example Request:**

```http
GET /v1/customers/1 HTTP/1.1
Host: localhost:5000
Content-Type: application/json
```

### **Example Response (Success 200 OK):**

```json
{
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "phone": "123-456-7890",
    "cpf": "123.456.789-00"
}
```

### **Example Response (404 Not Found):**

```json
{
    "message": "Customer not found"
}
```

---

## 📌 **3. Create a New Customer**
### **Endpoint:** POST /v1/customers
### **Description:**

Creates a new customer.

### **Example Request:**

```http
POST /v1/customers HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "phone": "555-555-5555",
    "cpf": "111.222.333-44"
}
```

### **Example Response (201 Created):**

```json
{
    "id": 3,
    "name": "Alice Johnson",
    "email": "alice@example.com",
    "phone": "555-555-5555",
    "cpf": "111.222.333-44"
}
```

---

## 📌 **4. Update an Existing Customer**
### **Endpoint: PUT /v1/customers/{id}**
### **Description:**

Updates customer information by ID.

### **Example Request:**

```http
PUT /v1/customers/3 HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
    "name": "Alice Johnson",
    "email": "alice.new@example.com",
    "phone": "555-123-4567",
    "cpf": "111.222.333-44"
}
```

### **Example Response (200 OK):**

```json
{
    "id": 3,
    "name": "Alice Johnson",
    "email": "alice.new@example.com",
    "phone": "555-123-4567",
    "cpf": "111.222.333-44"
}
```

---

## 📌 **5. Delete a Customer**
### **Endpoint:** DELETE /v1/customers/{id}
### **Description:**

Deletes a customer by ID.

### **Example Request:**

```http
DELETE /v1/customers/3 HTTP/1.1
Host: localhost:5000
```

### **Example Response (200 OK):**

```json
{
    "message": "Customer deleted successfully"
}
```

---

### 📌 **[Versão em Português](../pt-br/metodos-api.md)**