# Docker Configurations for Databases

## General Settings [DockerHub Link](https://hub.docker.com/search?q=)

This document outlines how to set up Docker containers for various databases. Make sure Docker is installed on your machine before following these steps.

### MySQL

1. **Pull the latest image:**
   ```bash
   docker pull mysql
   ```

2. **Run the container:**
   ```bash
   docker run --name mymysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=admin -d mysql
   ```

3. **Access the container and run MySQL:**
   ```bash
   docker exec -it mymysql bash
   mysql -u root --password
   ```

   - **Password:** `admin`

#### Connection Details

| Variable         | Value           |
|------------------|-----------------|
| **Host**         | `localhost`     |
| **Port**         | `3306`          |
| **Database**     | (Specify your database name) |
| **User**         | `root`          |
| **Password**     | `admin`         |
| **Connection String** | `mysql://root:admin@localhost:3306/your_database_name` |

### MongoDB

1. **Pull the latest image:**
   ```bash
   docker pull mongo
   ```

2. **Run the container:**
   ```bash
   docker run --name mymongo -p 27017:27017 -d mongo
   ```

3. **Access the container:**
   ```bash
   docker exec -it mymongo bash
   ```

#### Connection Details

| Variable         | Value           |
|------------------|-----------------|
| **Host**         | `localhost`     |
| **Port**         | `27017`         |
| **Database**     | (Specify your database name) |
| **User**         | (If authentication is enabled) |
| **Password**     | (If authentication is enabled) |
| **Connection String** | `mongodb://localhost:27017/your_database_name` |

### PostgreSQL

1. **Pull the latest image:**
   ```bash
   docker pull postgres
   ```

2. **Run the container:**
   ```bash
   docker run --name mypostgres -p 5432:5432 -e POSTGRES_USER=root -e POSTGRES_PASSWORD=administrador -e POSTGRES_DB=myappdb -d postgres
   ```

3. **Access the container and run PostgreSQL:**
   ```bash
   docker exec -it mypostgres bash
   psql -U root --password --db myappdb
   ```

   - **Password:** `administrador`

#### Connection Details

| Variable         | Value           |
|------------------|-----------------|
| **Host**         | `localhost`     |
| **Port**         | `5432`          |
| **Database**     | `myappdb`       |
| **User**         | `root`          |
| **Password**     | `administrador` |
| **Connection String** | `postgres://root:administrador@localhost:5432/myappdb` |

---
