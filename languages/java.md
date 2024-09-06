## API Rest with spring boot
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



## Most used packages in Java - Spring Boot

You can visit the website https://mvnrepository.com/ to find more packages.

1. **To Add springfox-boot-starter:**
    Add the dependency in the pom.xml file:
    ```xml
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-boot-starter</artifactId>
        <version>3.0.0</version>
    </dependency>
    ```
    This package allows you to integrate Swagger UI into your Java Spring Boot application. Swagger UI provides interactive documentation for your APIs, making it easier to explore and test them.


2. **For JPA and Hibernate:**
    Add the dependencies in the pom.xml file:
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    ```
    ```xml
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
    </dependency>
    ```
    These dependencies allow you to work with JPA and Hibernate, which are object-relational mapping technologies in Spring Boot.

3. **For Connection with SQLite:**
    Add the dependencies in the pom.xml file:
    ```xml
    <dependency>
        <groupId>org.xerial</groupId>
        <artifactId>sqlite-jdbc</artifactId>
    </dependency>
    ```
    In Java Spring Boot, you can work with SQLite databases using sqlite-jdbc 
