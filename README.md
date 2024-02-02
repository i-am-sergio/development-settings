# Development-configs
## Create API (NodeJS with ExpressJS) 
[Click here for Nodejs Settings](nodejs.md)

1. Install Node.js and npm (Node Package Manager)
2. Navigate to the directory where you want to create your project and run the following commands in the terminal:
    ```cmd
    npm init -y
    npm install express
    ```
    * Add `"type": "module"` in package.json
3. Create an entry file for your Express application, for example, app.js.
4. Open app.js in a code editor and set up your Express application:
    ```javascript
    import express from 'express';

    const app = express();
    const port = 3000;

    app.get('/', (req, res) => {
      res.send('Hello, Express!');
    });

    app.listen(port, () => {
      console.log(`Server is running on port ${port}`);
    });

    ```
5. Run your Express application using the following command:
    ```cmd
    node app.js
    ```

## Create API (C# with .NET) 
[Click here for Dotnet Settings](csharp.md)

1. Install dotnet SDK from the official .NET website.
2. Navigate to the Desktop and run the following command in the terminal:
    ```cmd
    dotnet new web -o NameOfYourProjectHere -f net7.0
    ```
3. Navigate into the newly created project directory:
    ```cmd
    cd NameOfYourProject
    ```
4. You can run the API by executing the following command in the project directory:
    ```cmd
    dotnet run
    ```
5. Install Swashbuckle package:
    ```cmd
    dotnet add package Swashbuckle.AspNetCore
    ```
6. After uploaded project to github:
    - Para restaurar las dependencias, ejecutar:
    ```cmd
    dotnet restore
    ```
    - Compilar el projecto:
    ```cmd
    dotnet build
    ```
    - Ejecutar el projecto:
    ```cmd
    dotnet run
    ```

## Create API (Java with Spring Boot)
[Click here for Java Settings](csharp.md)
1. Install JDK (Choose version 17 or 20, depending on your preference)
2. Install Dependency manager (Maven o Gradle):
    - Download maven binary zip and copy to `C:\Program Files\Maven` (create Maven Folder if not exist)
3. Configure Your Environment variables:
    - JAVA_HOME = `C:\Program Files\Java\jdk-17` (This could be another version of JDK)
    - MAVEN_HOME = `C:\Program Files\Maven\apache-maven-3.9.4` (This could be another version of Maven)
    - Add to Path: 
        - %JAVA_HOME%\bin
        - %MAVEN_HOME%\bin
4. Install Visual Studio Code Extensions:
    - Spring Initializr Java Support (To add dependencies to your project)
    - Language Support for Java
4. Create a New Spring Boot Project: 
    - Visit the [Spring Initializr](https://start.spring.io/) website.
    - Choose "Maven" as the project type.
    - Select the desired Spring Boot version.
    - Select `war` for web app and `jar` for desktop app 
    - Add the "Spring Web" dependency to your project.
    - Click "Generate" and download the generated project ZIP file.
    - Extract the contents of the ZIP file to your preferred directory.
4. Develop the API:
    - Create a new Java class for your API's main application, such as `YourApplicationNameApplication.java`.
    - Annotate the class with `@SpringBootApplication` to indicate the Spring Boot application.
    - Create controller classes in a package like `com.example.yourapplication.controllers`.
    - Define API endpoints using annotations like `@RestController` and `@GetMapping`.
5. Write the API Code:
    ```java
    package com.example.yourapplication.controllers;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class HelloController {
        @GetMapping("/hello")
        public String hello() {
            return "Hello, Spring Boot!";
        }
    }
    ```
6. Run the Application:
    - Run in Terminal:
        ```bash
        mvn spring-boot:run
        ```
        The Spring Boot application will start, and you can access your API at http://localhost:8080/hello
