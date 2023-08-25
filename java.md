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