# 📌 Installation

This guide will help you set up the API, from installing .NET 7 to preparing the database.

---

## 📖 1. Installing .NET 7

To run this API, you need to install the **.NET 7 SDK**. Download it from the official website:

🔗 [Download .NET 7](https://dotnet.microsoft.com/en-us/download/dotnet/7.0)

After installation, verify that **.NET** is installed correctly by running the following command in the terminal:

```powershell
dotnet --version
```

If the command returns a version number (e.g., 7.0.15), the installation was successful.

---

## 📖 2. Creating the Project

Now, create a new project in your desired directory using the following command:

```powershell
dotnet new web -o CustomersAPI -f net7.0
```

This will create a new ASP.NET Core project named CustomersAPI. Then, navigate into the project directory:

```powershell
cd CustomersAPI
```

---

## 📖 3. Opening the Project in Visual Studio\

If you're using Visual Studio, open the newly created project via "Open a project or solution" and select the CustomersAPI folder.

If you prefer to use Visual Studio Code, run:

```powershell
code .
```

This will open the project in VS Code.

---

## 📖 4. Installing Entity Framework Core
Inside the project, you need to install Entity Framework Core to manage the database.

Open the NuGet Package Manager in Visual Studio:

1. Go to Tools > NuGet Package Manager > Manage NuGet Packages for Solution….
2. In the Browse tab, search for Entity Framework Core.
3. Select Microsoft.EntityFrameworkCore and install the latest version (7.0.15).
4. Also install Microsoft.EntityFrameworkCore.SqlServer to connect to SQL Server.
5. To support migrations, install Microsoft.EntityFrameworkCore.Design.

Alternatively, install via terminal:

```powershell
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
```

---

## 📖 5. Setting Up the Database

Now, let’s configure the database connection. In the project directory, create a folder Data and add the AppDbContext class:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Customer> Customers { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        => optionsBuilder.UseSqlServer("Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;");
}
```

The Connection String defines the connection to the database. Modify the Server and Database as needed.

For more Connection String formats, check: 🔗 [SQL Server Connection Strings](https://www.connectionstrings.com/sql-server/)

---

## 📖 6. Creating the First Migration

Now, create the first migration to initialize the database.

Run the following commands in the terminal:

```powershell
dotnet ef migrations add InitialCreation
dotnet ef database update
```

If everything is correct, the database will be created with the required table.

---

## 📖 7. Running the API

Now, start the API with the command:

```powershell
dotnet watch run
```

The API will be running and ready to test in Postman or a browser!

✅ API installation and configuration is complete! 🚀

---

### 📌 **[Versão em Português](`pt/installation.md`)**