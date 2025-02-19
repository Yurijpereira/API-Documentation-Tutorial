# 🌍 Customer API Documentation (English & Portuguese)

Welcome to the **Customer API** documentation! This project provides a RESTful API built with **.NET 7** and **Entity Framework** to manage customer records efficiently.

## 📌 Language Selection | Seleção de Idioma

- 🇬🇧 **[English Version](docs/en/README.md)**
- 🇧🇷 **[Versão em Português](docs/pt/README.md)**

---

## 📖 About this API

### ✅ Features:
- RESTful API supporting **CRUD operations**
- **SQL Server** integration using **Entity Framework**
- Built with **.NET 7** for high performance
- Follows **best practices** for maintainability

This API allows developers to **create, retrieve, update, and delete** customer records in a structured database. You can follow the installation and configuration steps in the documentation.

---

## 🚀 Getting Started

### 📌 1. Clone this repository:
```bash
git clone https://github.com/SEU_USUARIO/NOME_REPOSITORIO.git
cd NOME_REPOSITORIO
```

### 📌 2. Install .NET 7 SDK:
[Download .NET 7](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)

### 📌 3. Set up the project:
```bash
dotnet new web -o CustomersAPI -f net7.0
cd CustomersAPI
```

### 📌 4. Install dependencies:
```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
```

### 📌 5. Configure and apply database migrations:
```bash
dotnet ef migrations add InitialCreation
dotnet ef database update
```

### 📌 6. Run the API:
```bash
dotnet watch run
For a complete guide, check out the documentation.
```

## 📌 API Endpoints Overview
| Method  | Endpoint             | Description         |
|---------|----------------------|---------------------|
| **GET**  | `/v1/customers`      | Get all customers  |
| **GET**  | `/v1/customers/{id}` | Get customer by ID |
| **POST** | `/v1/customers`      | Create a new customer |
| **PUT**  | `/v1/customers/{id}` | Update a customer  |
| **DELETE** | `/v1/customers/{id}` | Delete a customer  |


For detailed API usage, check the documentation:

- 🇬🇧 [English API Guide](en/README.md)
- 🇧🇷 [Guia da API em Português](pt/README.md)

## 📄 License
This project is licensed under the MIT License. See the LICENSE file for details.

## 🤝 Contributing
Contributions are welcome! If you find any issues or have suggestions, feel free to:

- Open an Issue 💬
- Submit a Pull Request 🚀

## 🔗 Useful Links
- [Official .NET 7 Documentation](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)
- [Entity Framework Core Docs](https://learn.microsoft.com/en-us/ef/core/)
- [GitHub Repository](https://github.com/Yurijpereira/API-Documentation-Tutorial)
- [Live Documentation on GitHub Pages](https://yurijpereira.github.io/API-Documentation-Tutorial/)