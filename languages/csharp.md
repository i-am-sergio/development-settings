## API Rest Start
1. Install dotnet SDK from the official .NET website.
2. Create new project:
    - Web Application Template
    ```bash
    dotnet new web -n NameOfYourProject
    ```
    - Console Project Template
    ```
    dotnet new console -n NameOfYourProject
    ```
    - List Templates:
    ```
    dotnet new --list
    ```
4. You can run the API by executing the following command in the project directory:
    ```bash
    cd NameOfYourProject
    dotnet run
    ```
5. After uploaded project to github:
    - Restore dependencies if *NameOfYourProject.csproj* has been modified:
    ```bash
    dotnet restore
    ```
    - Compile project:
    ```bash
    dotnet build
    ```
    - Execute project:
    ```bash
    dotnet run
    ```


## Most used packages in C# - .NET
You can visit the website https://www.nuget.org/ to find more packages.

## Settings
- List global tools
  ```bash
  dotnet tool list --global
  ```
- Install global tools as *dotnet ef*
  ```bash
  dotnet tool install --global dotnet-ef
  ```
  - Add to global variables (~/.bashrc or ~/.zshrc) copy the following:
    ```vim
    export PATH=$PATH:$HOME/.dotnet/tools
    ```
  - Reload global variables:
    ```bash
    source ~/.zshrc
    ```
- Database Connection
  - Edit *appsettings.json* according to the sql database
    ```json
    "ConnectionStrings": {
      "MySqlConnection": "Server=monorail.proxy.rlwy.net;Port=18098;Database=railway;User=root;Password=EH6F352114bCH14Ee5BG6E6c2EeDEbb5;ConvertZeroDateTime=True;",
      "PostgresConnection": "Server=viaduct.proxy.rlwy.net;Port=15406;Database=railway;Username=postgres;Password=52aBGEaeFE-ADbe22gG2aG11CADdFdcF",
      "SqlServerConnection": "Data Source=mssql-162515-0.cloudclusters.net,19796;Initial Catalog=sqlserverdb;User Id=root;Password=Admin123;TrustServerCertificate=True;"
    }
    ```
  - Install Entity Framework
    ```bash
    dotnet add package MySql.EntityFrameworkCore # for MySql
    ```
  - Add Class Models (*As follow sample*)
    ```csharp
    using System.ComponentModel.DataAnnotations;
    using System.ComponentModel.DataAnnotations.Schema;
    
    namespace MyWebProject;
    
    public class UserModel
    {
        [Key][DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int Id { get; set; }
        public required string Name { get; set; }
        public required string Email { get; set; }
        public required string Password { get; set; }
    }

    ```
  - Add DBContext (*create context/Context.cs*)
    ```csharp
    using Microsoft.EntityFrameworkCore;
    namespace MyWebProject;
    
    public class Context : DbContext
    {
        public Context(DbContextOptions<Context> options) : base(options) { }
        public DbSet<UserModel> Users { get; set; }
    }
    ```
  - Add DBContext in main file (*Program.cs*)
    ```csharp
    using Microsoft.EntityFrameworkCore;
    using MyWebProject;
    
    var builder = WebApplication.CreateBuilder(args);
    var connectionString = builder.Configuration.GetConnectionString("SqlServerConnection") ?? string.Empty;
    
    builder.Services.AddControllers();
    builder.Services.AddDbContext<SqlContext>(
        options => options.UseSqlServer(connectionString)
        // options => options.UseMySQL(connectionString) // Use MySQL
        // options => options.UseNpgsql(connectionString) // Use PostgreSQL
        // options => options.UseSqlite("Data Source=MiProyectoWeb.db") // Use SQLite
    );
    
    var app = builder.Build();
    
    app.UseAuthorization(); // Enable authorization
    app.MapControllers(); // Map the controllers
    
    app.Run();
    ```
  - Migrations
      - Add migration:
      ```bash
      dotnet ef migrations add NamedYourMigration
      ```
      - Apply migrations:
      ```bash
      dotnet ef database update
      ```
      - Undo migration:
      ```bash
      dotnet ef database update NamedYourPreviewMigration
      ```

## Pakages

1. **Swagger:**
    ```bash
    dotnet add package Swashbuckle.AspNetCore
    ```
    To integrate Swagger UI into your ASP.NET Core application. Swagger UI provides interactive documentation for your APIs, making it easier to explore and test them.

2. **Entity Framework:**
    ```bash
    dotnet add package Microsoft.EntityFrameworkCore
    ```
    Entity Framework Core is an ORM that simplifies access to relational databases in .NET applications. 
   - ***To Mysql***
     ```bash
     dotnet add package MySql.EntityFrameworkCore
     ```
     This package extends Entity Framework Core to support MySQL databases, allowing seamless integration with MySQL.
   - ***To Sql server***
     ```bash
     dotnet add package Microsoft.EntityFrameworkCore.SqlServer
     ```
     This package adds support for SQL Server to Entity Framework Core, enabling you to work with SQL Server databases.
   - ***To PostgreSql***
     ```bash
     dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
     ```
     Npgsql.EntityFrameworkCore.PostgreSQL extends Entity Framework Core to provide support for PostgreSQL databases, allowing you to seamlessly integrate PostgreSQL.

4. **Newtonsoft.Json:**
    ```bash
    dotnet add package Newtonsoft.Json
    ```
    This package provides advanced JSON serialization and deserialization functionalities and is widely used in .NET projects.

5. **AutoMapper:**
    ```bash
    dotnet add package AutoMapper
    ```
    AutoMapper simplifies property mapping between objects in your application, saving you time and reducing code duplication.

6. **Serilog:**
    ```bash
    dotnet add package Serilog
    ```
    Serilog is a flexible, high-performance logging library for .NET, making it easy to capture and analyze logs in your applications.

7. **FluentValidation:**
    ```bash
    dotnet add package FluentValidation
    ```
    This package provides a simple and expressive way to perform validations on your data models, improving code maintainability and clarity.

8. **IdentityServer4:**
    ```bash
    dotnet add package IdentityServer4
    ```
    IdentityServer4 is an open-source solution for identity and access management in .NET applications, following OAuth 2.0 and OpenID Connect standards.

10. **Dapper:**
    ```bash
    dotnet add package Dapper
    ```
    Dapper is an object-relational mapping library that enhances performance and efficiency when executing SQL queries in .NET applications.
