# Node.js: A Brief Introduction
> Node.js is an open-source, cross-platform JavaScript runtime environment that allows developers to run JavaScript on the server side. It was first released in 2009 by Ryan Dahl and has since gained popularity for its ease of use, performance, and scalability.

## What makes Node.js unique?
> One of the key features of Node.js is its ability to handle large numbers of connections with low overhead. This makes it particularly well-suited for building real-time, high-traffic applications such as chat apps, gaming servers, and social networks.

> Node.js also uses an event-driven, non-blocking I/O model, which means that it is able to handle multiple requests simultaneously without blocking the execution of other tasks. This makes it very efficient and fast.

## How to use Node.js
To get started with Node.js, you'll need to install it on your computer. You can download it from the official website or install it using a package manager such as npm.

Once you have Node.js installed, you can create a new project by running the npm init command in your terminal. This will create a package.json file that describes your project and its dependencies.

node - This command is used to run a Node.js application. You can specify the name of the file you want to run as an argument, like this: node app.js.

##  Some important commands are :
npm - This is the Node Package Manager, used to manage dependencies and packages for Node.js applications

1. `npm init `- Initializes a new Node.js project and creates a package.json file.
2. `npm install` - Installs all the dependencies specified in the package.json file.
3. `npm install <package-name>` - Installs a specific package, and adds it to the package.json file as a dependency.
4. `npm update `- Updates all the dependencies to their latest versions.
5. `npm start` - Starts the Node.js application defined in the package.json file.
6. `nodemon` - A tool that automatically restarts your Node.js application whenever changes are made to the code. To use it, install it globally using npm install -g nodemon, and then run your application using nodemon app.js.
7. `node --inspect `- This starts a debugging session in Node.js. You can attach a debugger to this session using a tool like the Chrome DevTools.
8. `node --version `- This command displays the version of Node.js that is installed on your system.  

## Create a simple HTTP server using the http module in Node.js:

```javascript

const http = require('http');

const server = http.createServer((req, res) => {
  // Set the response headers
  res.writeHead(200, {'Content-Type': 'text/plain'});

  // Write the response body
  res.write('Hello, World!');
  res.end();
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

> In this example, we first import the http module. We then create a new server by calling the createServer method, which takes a callback function that is called for each incoming request.

> Inside the callback function, we first set the response headers using the writeHead method. In this case, we're setting the response status code to 200 and the content type to text/plain.

> We then write the response body using the write method, which sends the string "Hello, World!". Finally, we call the end method to signal that we have finished writing the response.

> After creating the server, we start listening for incoming requests by calling the listen method and specifying the port number to listen on (3000 in this case). We also log a message to the console to indicate that the server is running.

> You can run this code by saving it to a file (e.g., server.js) and then running node server.js in your terminal. Once the server is running, you can access it by visiting http://localhost:3000 in your web browser.


## Example - installing express

You can then install additional packages and dependencies using npm. For example, to install the popular Express.js framework, you would run the following command:
```
npm install express
```
After you have installed the necessary packages, you can start building your Node.js application. You can create a new file called app.js and start by importing the necessary modules:

```
const express = require('express');
const app = express();
```
You can then define routes and middleware for your app:

```
app.get('/', (req, res) => {
  res.send('Hello, World!');
});
```
Finally, you can start the server and listen for incoming requests:

```
app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```
Node.js is a powerful and versatile tool for building high-performance, scalable applications. Its unique features make it well-suited for real-time and high-traffic applications. With its growing popularity and active community, it is a great choice for developers looking to build modern web applications.



