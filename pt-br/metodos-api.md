# 📌 Métodos da API

Este documento detalha os métodos disponíveis da **Customer API**, incluindo seus endpoints, descrições e exemplos de uso.

---

## 🎯 **Resumo dos Endpoints da API**

| **Método**  | **Endpoint**         | **Descrição**                 |
|------------|----------------------|------------------------------|
| **GET**    | `/v1/customers`      | Retorna todos os clientes    |
| **GET**    | `/v1/customers/{id}` | Retorna um cliente pelo ID   |
| **POST**   | `/v1/customers`      | Cria um novo cliente         |
| **PUT**    | `/v1/customers/{id}` | Atualiza um cliente existente |
| **DELETE** | `/v1/customers/{id}` | Exclui um cliente            |

---

## 📌 **1. Obter Todos os Clientes**
### **Endpoint:** `GET /v1/customers`
### **Descrição:**
Retorna a lista de todos os clientes cadastrados.

### **Exemplo de Requisição:**
```http
GET /v1/customers HTTP/1.1
Host: localhost:5000
Content-Type: application/json
```

### **Exemplo de Resposta:**

```json
[
    {
        "id": 1,
        "name": "João Silva",
        "email": "joao@example.com",
        "phone": "123-456-7890",
        "cpf": "123.456.789-00"
    },
    {
        "id": 2,
        "name": "Maria Souza",
        "email": "maria@example.com",
        "phone": "987-654-3210",
        "cpf": "987.654.321-00"
    }
]
```

---

## 📌 **2. Obter Cliente por ID**
### **Endpoint:** GET /v1/customers/{id}
### **Descrição:**

Retorna um cliente específico pelo ID.

### **Exemplo de Requisição:**

```http
GET /v1/customers/1 HTTP/1.1
Host: localhost:5000
Content-Type: application/json
```

### **Exemplo de Resposta (Sucesso 200 OK):**

```json
{
    "id": 1,
    "name": "João Silva",
    "email": "joao@example.com",
    "phone": "123-456-7890",
    "cpf": "123.456.789-00"
}
```

### **Exemplo de Resposta (404 Não Encontrado):**

```json
{
    "message": "Cliente não encontrado"
}
```

---

## 📌 **3. Criar um Novo Cliente**
### **Endpoint:** POST /v1/customers
### **Descrição:**

Cria um novo cliente no sistema.

### **Exemplo de Requisição:**

```http
POST /v1/customers HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
    "name": "Alice Pereira",
    "email": "alice@example.com",
    "phone": "555-555-5555",
    "cpf": "111.222.333-44"
}
```

### **Exemplo de Resposta (201 Criado):**

```json
{
    "id": 3,
    "name": "Alice Pereira",
    "email": "alice@example.com",
    "phone": "555-555-5555",
    "cpf": "111.222.333-44"
}
```

---

## 📌 **4. Atualizar um Cliente Existente**
### **Endpoint:** PUT /v1/customers/{id}
### **Descrição:**

Atualiza as informações de um cliente existente pelo ID.

### **Exemplo de Requisição:**

```http
PUT /v1/customers/3 HTTP/1.1
Host: localhost:5000
Content-Type: application/json

{
    "name": "Alice Pereira",
    "email": "alice.novo@example.com",
    "phone": "555-123-4567",
    "cpf": "111.222.333-44"
}
```

## **Exemplo de Resposta (200 OK):**

```json
{
    "id": 3,
    "name": "Alice Pereira",
    "email": "alice.novo@example.com",
    "phone": "555-123-4567",
    "cpf": "111.222.333-44"
}
```

---

## 📌 **5. Excluir um Cliente**
### **Endpoint:** DELETE /v1/customers/{id}
### **Descrição:**

Exclui um cliente do sistema pelo ID.

### **Exemplo de Requisição:**

```http
DELETE /v1/customers/3 HTTP/1.1
Host: localhost:5000
```

### **Exemplo de Resposta (200 OK):**

```json
{
    "message": "Cliente excluído com sucesso"
}
```

---

### 📌 **[English Version](../en-gb/api-methods.md)**