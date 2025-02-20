# 🌎 Configuração de Variáveis de Ambiente

Para evitar expor informações sensíveis no código-fonte, recomenda-se o uso de variáveis de ambiente para armazenar a connection string.

## 📌 1. Criando um arquivo `appsettings.json`
Crie um arquivo `appsettings.json` na raiz do projeto e adicione:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
  }
}
```

## 📌 2. Modificando o `AppDbContext`
Atualize a classe `AppDbContext` para ler a connection string do `appsettings.json`:

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

## 📌 3. Definir Variáveis de Ambiente no Windows
No terminal PowerShell:
```powershell
$env:ConnectionStrings__DefaultConnection="Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
```

## 📌 4. Definir Variáveis de Ambiente no Linux/Mac
```sh
export ConnectionStrings__DefaultConnection="Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;"
```