## API Rest start

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


## Most used packages in NodeJs - NPM

You can visit the website https://www.npmjs.com/ to find more packages.

1. **To Add swagger-ui-express:**
    ```bash
    dotnet add package Swashbuckle.AspNetCore
    ```
    This package provides an easy way to integrate Swagger UI into your Node.js Express application. It offers interactive API documentation for your APIs, making it simpler to explore and test them.

2. **For sequelize:**
    ```bash
    dotnet add package Microsoft.EntityFrameworkCore.InMemory
    ```
    Sequelize is an Object-Relational Mapping (ORM) library for Node.js that provides support for multiple database systems. It can be used for working with databases in a more abstracted and structured manner.

3. **For Connection with SQLite:**
    ```bash
    npm install sqlite3
    ```
    The sqlite3 package allows you to connect and interact with SQLite databases in a Node.js application. It provides an interface for executing SQL queries and managing SQLite databases.