# Development-configs
## Create API (NodeJS with ExpressJS)

1. Install Node.js and npm (Node Package Manager)
2. Navigate to the directory where you want to create your project and run the following commands in the terminal:
    ```cmd
    npm init -y
    npm install express
    ```
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

## Create API (Java with Spring Boot)
1. Install JDK (Choose version 17 or 20, depending on your preference)
2. Configure Your Development Environment: Eclipse or Visual Studio Code
3. Make sure your IDE is set up to work with Java and Maven.
4. Create a New Spring Boot Project: 
    - Visit the [Spring Initializr](https://start.spring.io/) website.
    - Choose "Maven" as the project type.
    - Select the desired Spring Boot version.
    - Add the "Spring Web" dependency to your project.
    - Click "Generate" and download the generated project ZIP file.
    - Extract the contents of the ZIP file to your preferred directory.
4. Develop the API:
    - Open the extracted project in your chosen IDE.
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
    - In your IDE, run the main application class (YourApplicationNameApplication.java).
    - The Spring Boot application will start, and you can access your API at http://localhost:8080/hello
7. Install Swagger for API Documentation (Optional):
    - Open your pom.xml (Maven configuration) file.
    - Add the following dependency for Swagger documentation:
    ```xml
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-boot-starter</artifactId>
        <version>3.0.0</version>
    </dependency>
    ```
8. Build your project to install the dependency.
9. Access the Swagger UI documentation at `http://localhost:8080/swagger-ui/index.html`.