# 🧪 Testando a API

Este documento detalha como testar a API usando **Postman**, **cURL** e **testes automatizados com xUnit**.

## 📌 1. Testando com Postman

1. Abra o Postman e crie uma **Nova Requisição**.
2. Configure a URL da API: `http://localhost:5000/v1/customers`
3. Escolha o método **GET**, **POST**, **PUT** ou **DELETE**.
4. Para **POST/PUT**, defina o **Body** como JSON:
```json
{
  "name": "Teste",
  "email": "teste@example.com",
  "phone": "99999-9999",
  "cpf": "123.456.789-00"
}
```
5. Clique em **Send** e veja a resposta.

## 📌 2. Testando com cURL
Você pode testar a API diretamente pelo terminal:

```sh
# Testando GET
curl -X GET http://localhost:5000/v1/customers

# Testando POST
curl -X POST http://localhost:5000/v1/customers -H "Content-Type: application/json" -d '{"name":"João","email":"joao@example.com","phone":"9999-9999","cpf":"12345678900"}'
```

## 📌 3. Testes Automatizados com xUnit
Crie uma pasta **Tests** e adicione um projeto de teste:
```sh
dotnet new xunit -o CustomerAPI.Tests
cd CustomerAPI.Tests
dotnet add reference ../ClientesAPI/ClientesAPI.csproj
```

Exemplo de teste para o **CustomerController**:
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
Execute os testes:
```sh
dotnet test
```