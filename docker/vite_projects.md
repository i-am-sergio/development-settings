# Dockerfile for Vite Projects (Production)

This Dockerfile is designed to containerize Vite projects, providing an easy way to deploy and run them in a Docker environment.

## Usage

To use this Dockerfile, follow these steps:

1. **Create Dockerfile**: Copy the contents of this Dockerfile into a file named `Dockerfile` in the root directory of your Vite project.

    ```Dockerfile
    # BUILD Dockerfile section ------------------------------
    # Use the node image as base image
    FROM node:20.11.1-alpine as builder

    # Set the working directory
    WORKDIR /app

    # Copy the package.json file to the working directory
    COPY package.json .

    # Install the dependencies
    RUN npm install

    # Copy the source code to the working directory
    COPY . .

    # Build the project
    RUN npm run build

    # PRDUCTION Dockerfile section ------------------------------
    # Use the nginx image as base image
    FROM nginx:alpine

    # Remove the default files from the nginx folder
    RUN rm -rf /usr/share/nginx/html/*

    # Copy the builded files from the builder stage to the nginx folder
    COPY --from=builder /app/dist /usr/share/nginx/html
    # Copy the builded files from the dist folder to the nginx folder
    # COPY dist /usr/share/nginx/html

    # Expose the port 80
    EXPOSE 80
    ```

2. **Build Docker Image**: Open a terminal, navigate to the directory containing your Dockerfile, and run the following command to build the Docker image:

    ```bash
    docker build -t my-vite-app .
    ```

    Replace `my-vite-react-app` with a desired name for your Docker image.
3. **Run Docker Container**: Once the image is built, you can run a Docker container based on this image using the following command:

    ```bash
    docker run -d -p 8080:80 my-vite-app
    ```

    This command will start a container in detached mode (`-d`) and map port `8080` of the host to port `80` of the container, allowing you to access your Vite application at `http://localhost:8080`.

## Dockerfile Explanation

### Build Stage:

- **Base Image**: Utilizes the lightweight Node.js Alpine image as the base image for building the project.

- **Working Directory**: Sets the working directory inside the container to `/app`.

- **Copy Dependencies**: Copies the project's `package.json` and `package-lock.json` files to the working directory.

- **Install Dependencies**: Installs the project dependencies using `npm install`.

- **Copy Project Files**: Copies the rest of the project files into the working directory.

- **Build Project**: Generates the production build of the Vite application using `npm run build`.

### Production Stage:

- **Base Image**: Utilizes the Nginx Alpine image as the base image for serving the static files.

- **Remove Default Nginx Configuration**: Removes the default Nginx configuration to replace it with our own.

- **Copy Build Files**: Copies the static files generated in the build stage from the `/app/dist` directory to the Nginx directory where it serves static files (`/usr/share/nginx/html`).

- **Expose Port**: Exposes port `80` to allow incoming connections to the Nginx server.

- **Start Nginx**: Nginx server automatically starts upon container initialization to serve the Vite application.
