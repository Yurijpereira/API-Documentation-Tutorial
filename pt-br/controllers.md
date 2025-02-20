# 📌 Criando Controllers

Este guia explica como criar os **controllers** da API para manipular requisições HTTP.

---

## 📖 1. O que é um Controller?

Os **Controllers** são responsáveis por gerenciar as requisições HTTP (GET, POST, PUT, DELETE) e processar os dados antes de enviá-los como resposta.

Na estrutura de uma API em **ASP.NET Core**, um controller deve:

- **Receber a requisição HTTP** e processá-la.
- **Interagir com o banco de dados** para buscar, salvar, atualizar ou excluir dados.
- **Retornar respostas adequadas** como `200 OK`, `201 Created`, `400 Bad Request`, etc.

---

## 📖 2. Criando o Controller `CustomerController`

No diretório **`Controllers`**, crie a classe `CustomerController`:

```csharp
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("v1/customers")]
public class CustomerController : ControllerBase
{
    private readonly AppDbContext _context;

    public CustomerController(AppDbContext context)
    {
        _context = context;
    }
}
```

**Explicação:**
- [ApiController]: Indica que esta classe é um controller de API.
- [Route("v1/customers")]: Define a rota base para esse controller.
- ControllerBase: Classe base que fornece funcionalidades para um controller sem suporte a views.
- Injeção de Dependência: O AppDbContext é injetado no construtor para permitir interações com o banco de dados.

---

## 📖 3. Criando o Método GET (Listar todos os clientes)

```csharp
[HttpGet]
public async Task<IActionResult> Get()
{
    var customers = await _context.Customers.AsNoTracking().ToListAsync();
    return Ok(customers);
}
```

- [HttpGet]: Especifica que este método lida com requisições GET.
- AsNoTracking(): Melhora o desempenho ao evitar que o Entity Framework rastreie alterações.
- ToListAsync(): Recupera a lista de clientes de forma assíncrona.
- Ok(customers): Retorna uma resposta 200 OK com a lista de clientes.

---

## 📖 4. Criando o Método GET por ID (Buscar um cliente específico)

```csharp
[HttpGet("{id}")]
public async Task<IActionResult> GetByIdAsync([FromRoute] int id)
{
    var customer = await _context.Customers.AsNoTracking().FirstOrDefaultAsync(x => x.Id == id);
    
    if (customer == null)
        return NotFound();
    
    return Ok(customer);
}
```

- [HttpGet("{id}")]: Especifica que este método lida com requisições GET com um parâmetro ID.
- [FromRoute] int id: Extrai o ID da URL da requisição.
- FirstOrDefaultAsync(): Recupera o primeiro registro que corresponde ao ID fornecido.
- NotFound(): Retorna uma resposta 404 Not Found se o cliente não existir.
- Ok(customer): Retorna uma resposta 200 OK com os detalhes do cliente.

---

## 📖 5. Criando o Método POST (Criar um novo cliente)

```csharp
[HttpPost]
public async Task<IActionResult> PostAsync([FromBody] CreateCustomerViewModel model)
{
    if (!ModelState.IsValid)
        return BadRequest(ModelState);

    var customer = new Customer
    {
        Name = model.Name,
        Email = model.Email,
        Phone = model.Phone,
        Cpf = model.Cpf,
    };

    await _context.Customers.AddAsync(customer);
    await _context.SaveChangesAsync();

    return Created($"v1/customers/{customer.Id}", customer);
}
```

- [HttpPost]: Especifica que este método lida com requisições POST.
- [FromBody] CreateCustomerViewModel model: O corpo da requisição deve conter um objeto de cliente válido.
- ModelState.IsValid: Valida os dados da requisição.
- AddAsync(): Adiciona o novo cliente ao banco de dados de forma assíncrona.
- SaveChangesAsync(): Salva as alterações no banco de dados.
- Created(): Retorna uma resposta 201 Created com o cliente recém-criado.


---

## 📖 6. Criando o Método PUT (Atualizar um cliente existente)

```csharp
[HttpPut("{id}")]
public async Task<IActionResult> PutAsync([FromRoute] int id, [FromBody] CreateCustomerViewModel model)
{
    if (!ModelState.IsValid)
        return BadRequest();

    var customer = await _context.Customers.FirstOrDefaultAsync(x => x.Id == id);
    
    if (customer == null)
        return NotFound();

    customer.Name = model.Name;
    customer.Email = model.Email;
    customer.Phone = model.Phone;
    customer.Cpf = model.Cpf;

    _context.Customers.Update(customer);
    await _context.SaveChangesAsync();

    return Ok(customer);
}
```

- [HttpPut("{id}")]: Especifica que este método lida com requisições PUT com um parâmetro ID.
- [FromRoute] int id: Extrai o ID da URL da requisição.
- FirstOrDefaultAsync(): Encontra o cliente pelo ID.
- NotFound(): Retorna uma resposta 404 Not Found se o cliente não existir.
- Atualização do cliente: Atribui novos valores ao objeto cliente existente.
- Update(): Marca o cliente como modificado.
- SaveChangesAsync(): Salva os dados do cliente atualizado no banco de dados.
- Ok(customer): Retorna uma resposta 200 OK com o cliente atualizado.

---

## 📖 7. Criando o Método DELETE (Remover um cliente)

```csharp
[HttpDelete("{id}")]
public async Task<IActionResult> DeleteAsync([FromRoute] int id)
{
    var customer = await _context.Customers.FirstOrDefaultAsync(x => x.Id == id);

    if (customer == null)
        return NotFound();

    _context.Customers.Remove(customer);
    await _context.SaveChangesAsync();

    return Ok();
}
```

- [HttpDelete("{id}")]: Especifica que este método lida com requisições DELETE com um parâmetro ID.
- [FromRoute] int id: Extrai o ID da URL da requisição.
- FirstOrDefaultAsync(): Encontra o cliente pelo ID.
- NotFound(): Retorna uma resposta 404 Not Found se o cliente não existir.
- Remove(): Exclui o cliente do banco de dados.
- SaveChangesAsync(): Salva as alterações.
- Ok(): Retorna uma resposta 200 OK indicando a exclusão bem-sucedida.

---

## 🎯 Resumo

| **Método** | **Endpoint**         | **Descrição**                |
|------------|----------------------|------------------------------|
| **GET**    | `/v1/customers`      | Retorna todos os clientes   |
| **GET**    | `/v1/customers/{id}` | Retorna um cliente pelo ID  |
| **POST**   | `/v1/customers`      | Cria um novo cliente        |
| **PUT**    | `/v1/customers/{id}` | Atualiza um cliente existente |
| **DELETE** | `/v1/customers/{id}` | Exclui um cliente           |

Agora sua API já pode processar requisições! 🚀

---

### 📌 **[English Version](../en-gb/controllers.md)**