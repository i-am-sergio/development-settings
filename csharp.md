# Most used packages in C# - .NET
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
  Add to global variables (~/.bashrc or ~/.zshrc) copy the following:
  ```vim
  export PATH=$PATH:$HOME/.dotnet/tools
  ```
  Reload global variables:
  ```bash
  source ~/.zshrc
  ```
- Generate Migrations
  ```bash
  dotnet ef migrations add NamedYourMigration --startup-project ../ProjectName
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
     dotnet add package Pomelo.EntityFrameworkCore.MySql
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
