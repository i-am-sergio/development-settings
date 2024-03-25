# Dockerfile for Spring Boot Java Projects

This Dockerfile is designed to containerize Spring Boot Java projects, providing a simple way to package and run them in a Docker environment.

## Usage

To use this Dockerfile for your Spring Boot Java project, follow these steps:

1. **Build Application**: Build the applicaction in JAR file:
    ```bash
    ./gradlew build
    ```
    The .JAR file is generated in the `./build/libs/` folder

2. **Create Dockerfile**: Copy the contents of this Dockerfile into a file named `Dockerfile` in the root directory of your Spring Boot Java project.

    ```Dockerfile
    # PRODUCTION: Dockerfile section -------------------
    # Use openjdk 17 as the base image
    FROM bellsoft/liberica-openjdk-alpine:17

    # Set the working directory
    WORKDIR /app

    # Copy jar file to the container
    COPY /build/libs/*.jar /app/app.jar

    # Expose the application port
    EXPOSE 8080

    # Run the application
    CMD ["java", "-jar", "app.jar"]

    ```

3. **Build Docker Image**: Open a terminal, navigate to the directory containing your Dockerfile, and run the following command to build the Docker image:

    ```bash
    docker build -t my-spring-boot-app .
    ```

    Replace `my-spring-boot-app` with a desired name for your Docker image.

4. **Run Docker Container**: Once the image is built, you can run a Docker container based on this image using the following command:

    ```bash
    docker run -d -p 5000:8080 --name my-app-container my-spring-boot-app
    ```

    This command will start a container in detached mode (`-d`), running your Spring Boot Java application and exposing it on port 8080.

## Dockerfile Explanation

### Run Stage:

- **Base Image**: Utilizes the builder stage as the base image for running the Spring Boot Java application.

- **Copy Built Jar**: Copies the built JAR file into the runtime container.

- **Working Directory**: Sets the working directory inside the container to `/app`.

- **Expose Port**: Exposes port 8080 to allow external access to the Spring Boot application.

- **Run Application**: Sets the command to run the Spring Boot application JAR file when the container starts.
