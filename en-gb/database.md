# 📌 Database Configuration

This guide explains how to configure the database for the API using **Entity Framework Core** and **SQL Server**.

---

## 📖 1. Installing SQL Server

If you don’t have **SQL Server** installed, you can download and install it from the official link:

🔗 [Download SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)

Additionally, install **SQL Server Management Studio (SSMS)** to manage your database visually:

🔗 [Download SSMS](https://aka.ms/ssmsfullsetup)

After installation, **make sure SQL Server is running** before proceeding.

---

## 📖 2. Installing Entity Framework Core

To connect the API to the database, install the following **Entity Framework Core** packages in the project:

```powershell
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
```

- Microsoft.EntityFrameworkCore: Provides core Entity Framework Core functionality.
- Microsoft.EntityFrameworkCore.SqlServer: Enables SQL Server connectivity.
- Microsoft.EntityFrameworkCore.Design: Required for migrations.

If you are using Visual Studio, you can install these packages via the NuGet Package Manager.

---

## 📖 3. Creating AppDbContext

In the project directory, create a folder named Data and add the AppDbContext class:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Customer> Customers { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        => optionsBuilder.UseSqlServer("Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;");
}
```

- DbSet<Customer> represents the Customers table in the database.
- Connection String: Adjust Server and Database according to your setup.

If you have trouble setting up the Connection String, check: 🔗 [SQL Server Connection Strings](https://www.connectionstrings.com/sql-server/)

---

## 📖 4. Creating the First Migration

Now, let's create the first migration to initialize the database.

```powershell
dotnet ef migrations add InitialCreation
dotnet ef database update
```

- dotnet ef migrations add InitialCreation: Creates the initial database structure.
- dotnet ef database update: Applies the migration and creates the database.

If everything is correct, the database will be created automatically.

---

## 📖 5. Testing the Connection

To verify that the connection is working, run the project:

```powershell
dotnet watch run
```

Now you can access the API and test the endpoints. ✅

---

### 📌 **[Versão em Português](../pt-br/banco.md)**