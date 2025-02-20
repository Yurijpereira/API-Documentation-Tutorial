# 📌 Configuração do Banco de Dados

Este guia explica como configurar o banco de dados para a API, utilizando **Entity Framework Core** e **SQL Server**.

---

## 📖 1. Instalando o SQL Server

Caso ainda não tenha o **SQL Server** instalado, você pode baixá-lo e instalá-lo através do link oficial:

🔗 [Baixar SQL Server](https://www.microsoft.com/pt-br/sql-server/sql-server-downloads)

Além disso, instale o **SQL Server Management Studio (SSMS)** para gerenciar visualmente seu banco de dados:

🔗 [Baixar SSMS](https://aka.ms/ssmsfullsetup)

Após a instalação, **certifique-se de que o SQL Server está em execução** antes de continuar.

---

## 📖 2. Instalando o Entity Framework Core

Para conectar a API ao banco de dados, instale os seguintes pacotes **Entity Framework Core** no projeto:

```powershell
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
```

- Microsoft.EntityFrameworkCore: fornece as funcionalidades principais do Entity Framework Core.
- Microsoft.EntityFrameworkCore.SqlServer: permite conectar o SQL Server ao projeto.
- Microsoft.EntityFrameworkCore.Design: necessário para gerar migrations.

Caso esteja usando Visual Studio, você pode instalar esses pacotes pelo Gerenciador de Pacotes NuGet.

---

## 📖 3. Criando o AppDbContext

No diretório do projeto, crie uma pasta chamada Data e adicione a classe AppDbContext:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Customer> Customers { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        => optionsBuilder.UseSqlServer("Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;");
}
```

- DbSet<Customer> representa a tabela Customers no banco de dados.
- Connection String: Ajuste Server e Database conforme sua configuração.

Caso tenha dificuldades para configurar a Connection String, consulte: 🔗 [Connection Strings para SQL Server](https://www.connectionstrings.com/sql-server/)

---

## 📖 4. Criando a Primeira Migration

Agora, vamos criar a primeira migration para inicializar o banco de dados.

```powershell
dotnet ef migrations add InitialCreation
dotnet ef database update
```

- dotnet ef migrations add InitialCreation: Cria a estrutura inicial do banco.
- dotnet ef database update: Aplica a migration e cria o banco de dados.

Se tudo estiver correto, o banco de dados será criado automaticamente.

---

## 📖 5. Testando a Conexão

Para verificar se a conexão está funcionando, execute o projeto:

```powershell
dotnet watch run
```

Agora você pode acessar a API e testar os endpoints. ✅

A configuração do banco de dados está concluída! 🚀

---

### 📌 **[English Version](../en-gb/database.md)**