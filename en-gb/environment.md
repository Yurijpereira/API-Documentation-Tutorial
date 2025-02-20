# 🌍 Environment Variables Configuration

To avoid exposing sensitive information in the source code, it is recommended to use environment variables to store the connection string.

## 📌 1. Creating an `appsettings.json` File
Create an `appsettings.json` file in the project's root directory and add:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
  }
}
```

## 📌 2. Modifying `AppDbContext`
Update the `AppDbContext` class to read the connection string from `appsettings.json`:

```csharp
using Microsoft.Extensions.Configuration;

public class AppDbContext : DbContext
{
    private readonly IConfiguration _configuration;

    public AppDbContext(IConfiguration configuration)
    {
        _configuration = configuration;
    }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer(_configuration.GetConnectionString("DefaultConnection"));
    }

    public DbSet<Customer> Customers { get; set; }
}
```

## 📌 3. Setting Environment Variables on Windows
In PowerShell:
```powershell
$env:ConnectionStrings__DefaultConnection="Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
```

## 📌 4. Setting Environment Variables on Linux/Mac
```sh
export ConnectionStrings__DefaultConnection="Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
```