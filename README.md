# Development-configs

## Create API (C# with .NET)

1. Install dotnet SDK
2. Navigate to the Desktop and run the following command in the terminal:
```cmd
dotnet new web -o nameProjectHere -f net7.0
```

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