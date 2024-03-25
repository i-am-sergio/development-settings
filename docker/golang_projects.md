# Dockerfile for Golang Projects

This Dockerfile is designed to containerize Golang projects, providing a simple way to package and run them in a Docker environment.

## Usage

To use this Dockerfile for your Golang project, follow these steps:

1. **Create Dockerfile**: Copy the contents of this Dockerfile into a file named `Dockerfile` in the root directory of your Golang project.

    ```Dockerfile
    # BUILD Dockerfile section ------------------------------

    # Use the Golang image version as the base image
    FROM golang:1.22.1-alpine as builder

    # Set the working directory inside the container to /app
    WORKDIR /app

    # Copy the entire project directory into the container's /app directory
    COPY . .

    # Clean the Go module cache to ensure a clean build environment
    RUN go clean --modcache

    # Download and install project dependencies
    RUN go get

    # Build the Go application and output the binary as 'executable'
    RUN go build -o executable

    # PRDUCTION Dockerfile section ------------------------------

    # Use the official Alpine Linux image as the base image for the runtime container
    FROM alpine:latest

    # Set the working directory inside the container to /app
    WORKDIR /app

    # Copy the executable binary from the builder container (/app/executable) to the runtime container (/app/executable)
    COPY --from=builder /app/executable /app/executable

    # Set the default command to execute the 'executable' binary when the container starts
    CMD ["./executable"]
    ```

2. **Build Docker Image**: Open a terminal, navigate to the directory containing your Dockerfile, and run the following command to build the Docker image:

    ```bash
    docker build -t my-golang-app .
    ```

    Replace `my-golang-app` with a desired name for your Docker image.

3. **Run Docker Container**: Once the image is built, you can run a Docker container based on this image using the following command:

    ```bash
    docker run -d my-golang-app
    ```

    This command will start a container in detached mode (`-d`), running your Golang application.

## Dockerfile Explanation

### Build Stage:

- **Base Image**: Utilizes the Golang Alpine image as the base image for building the Golang project.

- **Working Directory**: Sets the working directory inside the container to `/app`.

- **Copy Project Files**: Copies all files from the project directory into the working directory inside the container.

- **Clean Mod Cache**: Cleans the Go module cache to ensure a clean build environment.

- **Install Dependencies**: Uses `go get` to download and install the project dependencies.

- **Build Binary**: Builds the Golang application binary (`executable`) using `go build`.

### Run Stage:

- **Base Image**: Utilizes the Alpine image as the base image for running the Golang application.

- **Working Directory**: Sets the working directory inside the container to `/app`.

- **Copy Binary**: Copies the executable binary generated in the build stage from the builder container to the runtime container.

- **Run Application**: Sets the command to run the executable binary when the container starts.

## Conclusion

This Dockerfile simplifies the process of containerizing Golang applications by providing separate build and run stages. It encapsulates the build process and dependencies within a Docker image, making it easy to deploy Golang applications consistently across different environments.
