# 📌 Instalação

Este guia ajudará você a configurar a API desde a instalação do .NET 7 até a preparação do banco de dados.

---

## 📖 1. Instalando o .NET 7

Para rodar esta API, você precisa instalar o **.NET 7 SDK**. Faça o download no site oficial:

🔗 [Baixar .NET 7](https://dotnet.microsoft.com/pt-br/download/dotnet/7.0)

Após a instalação, verifique se o **.NET** foi instalado corretamente executando o seguinte comando no terminal:

```powershell
dotnet --version
```

Se o comando retornar um número de versão (por exemplo, 7.0.15), a instalação foi concluída com sucesso.

---

## 📖 2. Criando o Projeto

Agora, crie um novo projeto no diretório desejado usando o seguinte comando:

```powershell
dotnet new web -o ClientesAPI -f net7.0
```

Isso criará um novo projeto ASP.NET Core chamado ClientesAPI. Em seguida, entre no diretório do projeto:

```powershell
cd ClientesAPI
```

---

## 📖 3. Abrindo o Projeto no Visual Studio

Se estiver usando o Visual Studio, abra o projeto recém-criado através da opção "Open a project or solution" e selecione a pasta ClientesAPI.

Caso prefira usar o Visual Studio Code, execute:

```powershell
code .
```

Isso abrirá o projeto diretamente no VS Code.

---

## 📖 4. Instalando o Entity Framework Core

Dentro do projeto, você precisa instalar o Entity Framework Core, que gerenciará o banco de dados.

Abra o Gerenciador de Pacotes NuGet no Visual Studio:

1. Vá até Tools > NuGet Package Manager > Manage NuGet Packages for Solution….
2. Na aba Browse, pesquise por Entity Framework Core.
3. Selecione Microsoft.EntityFrameworkCore e instale a versão mais recente (atualmente 7.0.15).
4. Instale também o pacote Microsoft.EntityFrameworkCore.SqlServer para conectar ao SQL Server.
5. Para suporte a migrations, instale Microsoft.EntityFrameworkCore.Design.

Se preferir instalar via terminal, execute os seguintes comandos dentro do diretório do projeto:

```powershell
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
```

---

## 📖 5. Configurando o Banco de Dados

Agora, vamos preparar a conexão com o banco de dados. No diretório do projeto, crie uma pasta chamada Data e adicione a classe AppDbContext:

```csharp
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Customer> Customers { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        => optionsBuilder.UseSqlServer("Server=localhost\\SQLEXPRESS; Database=CustomerDB; Trusted_Connection=True; Encrypt=False;");
}
```

A Connection String define a conexão com o banco de dados. Se necessário, modifique o Server e Database de acordo com sua configuração.

Para verificar diferentes formatos de Connection Strings, consulte: 🔗 [Connection Strings para SQL Server](https://www.connectionstrings.com/sql-server/)

---

## 📖 6. Criando a Primeira Migration

Agora, vamos criar a primeira migration para inicializar o banco de dados.

No terminal, execute:

```powershell
dotnet ef migrations add InitialCreation
dotnet ef database update
```

Se tudo estiver correto, o banco de dados será criado com a tabela necessária.

---

## 📖 7. Executando a API

Agora, inicie a API com o comando:

```powershell
dotnet watch run
```

A API estará rodando e pronta para ser testada no Postman ou no navegador!

✅ A instalação e configuração da API estão concluídas! 🚀

---

### 📌 **[English Version](`en-gb/installation.md`)**