# 🧪 Testing the API

This document details how to test the API using **Postman**, **cURL**, and **automated tests with xUnit**.

## 📌 1. Testing with Postman

1. Open Postman and create a **New Request**.
2. Set the API URL: `http://localhost:5000/v1/customers`
3. Choose the **GET**, **POST**, **PUT**, or **DELETE** method.
4. For **POST/PUT**, define the **Body** as JSON:
```json
{
  "name": "Test",
  "email": "test@example.com",
  "phone": "99999-9999",
  "cpf": "123.456.789-00"
}
```
5. Click **Send** and check the response.

## 📌 2. Testing with cURL
You can test the API directly from the terminal:

```sh
# Testing GET
curl -X GET http://localhost:5000/v1/customers

# Testing POST
curl -X POST http://localhost:5000/v1/customers -H "Content-Type: application/json" -d '{"name":"John","email":"john@example.com","phone":"9999-9999","cpf":"12345678900"}'
```

## 📌 3. Automated Testing with xUnit
Create a **Tests** folder and add a test project:
```sh
dotnet new xunit -o CustomerAPI.Tests
cd CustomerAPI.Tests
dotnet add reference ../ClientesAPI/ClientesAPI.csproj
```

Example test for **CustomerController**:
```csharp
using Xunit;
using ClientesAPI.Controllers;
using Microsoft.AspNetCore.Mvc;

public class CustomerControllerTests
{
    [Fact]
    public void Get_ReturnsOkResult()
    {
        var controller = new CustomerController(null);
        var result = controller.Get();
        Assert.IsType<OkObjectResult>(result.Result);
    }
}
```
Run the tests:
```sh
dotnet test
```