# 📌 Creating Controllers

This guide explains how to create **API controllers** to handle HTTP requests.

---

## 📖 1. What is a Controller?

**Controllers** manage HTTP requests (GET, POST, PUT, DELETE) and process data before sending a response.

In an **ASP.NET Core API**, a controller must:

- **Handle HTTP requests** and process them.
- **Interact with the database** to retrieve, save, update, or delete data.
- **Return proper HTTP responses** such as `200 OK`, `201 Created`, `400 Bad Request`, etc.

---

## 📖 2. Creating the `CustomerController`

Inside the **`Controllers`** directory, create a `CustomerController` class:

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

**Explanation:**
- [ApiController]: Marks this class as an API controller.
- [Route("v1/customers")]: Defines the base route for this controller.
- ControllerBase: Provides basic functionality for an API controller without views.
- Dependency Injection: The AppDbContext is injected into the constructor to allow database interactions.

---

## 📖 3. Creating the GET Method (Retrieve all customers)

```csharp
[HttpGet]
public async Task<IActionResult> Get()
{
    var customers = await _context.Customers.AsNoTracking().ToListAsync();
    return Ok(customers);
}
```

- [HttpGet]: Specifies that this method handles GET requests.
- AsNoTracking(): Improves performance by preventing Entity - Framework from tracking changes.
- ToListAsync(): Retrieves the list of customers asynchronously.
- Ok(customers): Returns a 200 OK response with the list of customers.

---

## 📖 4. Creating the GET by ID Method (Retrieve a specific customer)

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

- [HttpGet("{id}")]: Specifies that this method handles GET requests with an ID parameter.
- [FromRoute] int id: Extracts the ID from the request URL.
- FirstOrDefaultAsync(): Retrieves the first record that matches the given ID.
- NotFound(): Returns a 404 Not Found response if the customer does not exist.
- Ok(customer): Returns a 200 OK response with the customer details.

---

## 📖 5. Creating the POST Method (Create a new customer)

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

- [HttpPost]: Specifies that this method handles POST requests.
- [FromBody] CreateCustomerViewModel model: The request body must contain a valid customer object.
- ModelState.IsValid: Validates the request data.
- AddAsync(): Adds the new customer to the database asynchronously.
- SaveChangesAsync(): Saves the changes in the database.
- Created(): Returns a 201 Created response with the newly created customer.

---

## 📖 6. Creating the PUT Method (Update an existing customer)

```csharp
[HttpPut("{id}")]
public async Task<IActionResult> PutAsync([FromRoute] int id, [FromBody] CreateCustomerViewModel model)
{
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

- [HttpPut("{id}")]: Specifies that this method handles PUT requests with an ID parameter.
- [FromRoute] int id: Extracts the ID from the request URL.
- FirstOrDefaultAsync(): Finds the customer by ID.
- NotFound(): Returns a 404 Not Found response if the customer does not exist.
- Updating the customer: Assigns new values to the existing customer object.
- Update(): Marks the customer as modified.
- SaveChangesAsync(): Saves the updated customer data to the database.
- Ok(customer): Returns a 200 OK response with the updated customer.

---

## 📖 7. Creating the DELETE Method (Remove a customer)

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

- [HttpDelete("{id}")]: Specifies that this method handles DELETE requests with an ID parameter.
- [FromRoute] int id: Extracts the ID from the request URL.
- FirstOrDefaultAsync(): Finds the customer by ID.
- NotFound(): Returns a 404 Not Found response if the customer does not exist.
- Remove(): Deletes the customer from the database.
- SaveChangesAsync(): Saves the changes.
- Ok(): Returns a **200 OK** response indicating successful deletion.

---

## 🎯 Summary

| **Method** | **Endpoint**         | **Description**               |
|------------|----------------------|-------------------------------|
| **GET**    | `/v1/customers`      | Retrieves all customers      |
| **GET**    | `/v1/customers/{id}` | Retrieves a customer by ID   |
| **POST**   | `/v1/customers`      | Creates a new customer       |
| **PUT**    | `/v1/customers/{id}` | Updates an existing customer |
| **DELETE** | `/v1/customers/{id}` | Deletes a customer           |

Now your API can process requests! 🚀

---

### 📌 **[Versão em Português](../pt-br/controllers.md)**