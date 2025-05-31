# Node.js_API
Introduction
Welcome to the fascinating world of creating RESTful APIs using Node.js and Express! In this guide, we’ll take you through a step-by-step journey on how to build your very own API with all the bells and whistles.

But before we dive into the nitty-gritty details, let’s get acquainted with what a Restful API is all about. Don’t worry, we won’t bore you with technical jargon. Simply put, a Restful API allows different applications to communicate with each other seamlessly, just like a well-choreographed dance.

Now, you might wonder why we’ve chosen Node.js and Express for this adventure. Well, brace yourself, because Node.js is a JavaScript runtime built on Chrome’s V8 engine, making it lightning-fast. And Express? It’s a minimalistic and flexible web application framework that brings out the best in Node.js.

So, let’s buckle up, set up our development environment, and embark on this exciting journey! We promise it’ll be worth it.

What is a RESTful API?
A RESTful API is a type of web service that allows different computer systems to communicate with each other over the internet. When we say “RESTful” we mean that it follows a set of rules for how that communication should take place.

Think of it as a way for two computers or applications to talk to each other through a common language, like English or Spanish. But instead of words, they use specific messages called “requests” and “responses” to do things like retrieve data or take actions on each other’s behalf.

These requests and responses are typically sent using a standardized format, like JSON or XML. This way, the different systems can understand each other and work together, even if they were built by different people or companies.

Why Choose Node.js and Express?
Node.js and Express are popular choices for creating a RESTful API for several reasons. Firstly, Node.js is built on Chrome’s V8 JavaScript engine, which provides ample performance and scalability. It allows developers to build server-side applications using JavaScript, a language that is widely used on the client side, making it easier to share code and reduce development time.

Express, on the other hand, is a lightweight framework built on top of Node.js. It provides a simple and intuitive way to create web applications and APIs. Express offers a wide range of features and middleware, making it highly flexible and customizable to suit different project requirements.

One of the key advantages of using Node.js and Express is their non-blocking, event-driven architecture. This means that they can handle a large number of concurrent requests efficiently, making them ideal for building high-performance APIs.

Additionally, Node.js has a thriving ecosystem with a vast number of open-source libraries and modules, providing developers with access to a wide range of tools and resources.

Furthermore, Express provides a clean and structured way to handle routing, allowing developers to define various endpoints and their corresponding HTTP methods. It also supports middleware, which allows for the easy implementation of functionality such as authentication, request validation, and error handling.

Setting Up the Development Environment
So, you’re ready to dive into the exciting world of creating a Restful API using Node.js and Express! But before we jump into coding, we need to set up our development environment. Don’t worry, it’s not as complicated as it sounds.

To set up the development environment for creating a basic Express server, you need to follow these steps:

Download and install Node.js from the official website if you haven’t already.

Open a new terminal or command prompt window and navigate to the directory where you want to create your server-side web application.

Create a new directory for your application by running the command mkdir my-express-server (You can replace “my-express-server” with any name of your choice).

Move into the newly created directory by running the command cd my-express-server.

Initialize a new Node.js project by running the command npm init. This will create a package.json file to store project dependencies and other relevant information.

Install Express as a dependency by running the command npm install express.

Once you have completed these steps, you can proceed to create a new file named server.js in the root directory of your project and begin building your Express server.

Creating a Basic Express Server
First things first, let’s create an entry point file for our Express server by running the command touch server.js. This file will serve as the starting point for our application. Feel free to name it whatever you like, but for the sake of simplicity, we’ll stick with the conventional name server.js.

Inside the server.js file, we’ll start by importing the necessary modules and creating an instance of the Express application. This can be done as follows:

const express = require('express');
const app = express();
Excellent! Now that we have our Express server set up, we need to specify which port it should listen on. This can be done by adding the following lines of code:

const port = process.env.PORT || 3000; // Use the port provided by the host or default to 3000
app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
Just add one home route for testing purposes by adding the following code at the end of the server.js file

 // Define a route to handle incoming requests
app.get('/', (req, res) => {
  res.send('Hello, Express!');
});
Final server.js file:

const express = require('express');
const app = express();

const port = process.env.PORT || 3000; // Use the port provided by the host or default to 3000
app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});

// Define a route to handle incoming requests
app.get('/', (req, res) => {
  res.send('Hello, Express!');
});
To start the newly created express server run the following command:
node app.js

Your Express server should now be running, and you can access it by opening a web browser and going to http://localhost:3000 (or the port you specified). You should see "Hello, Express!" displayed in your browser.

Congratulations! You’ve successfully created a basic Express server and it’s running. It’s as simple as that! In the upcoming sections, we’ll explore how to implement CRUD operations and add authentication to our API. Exciting times ahead! Stay tuned for more awesomeness.

Implementing CRUD Operations
To create CRUD (Create, Read, Update, Delete) operations in your Express.js server, you can extend the existing code. Here’s how you can do it:

Add a Data Store
For this example, let’s create a simple in-memory data store to hold some data. You can replace this with a real database like MongoDB or PostgreSQL in a production application. Add the following code in your server.js file:

// In-memory data store (replace with a database in production)
const data = [
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
  { id: 3, name: 'Item 3' },
];
2. Create Routes for CRUD Operations

Now, create routes for each CRUD operation:

Create (POST): Add a new item to the data store.

Read (GET): Retrieve a list of items or a specific item by ID.

Update (PUT): Update an existing item by ID.

Delete (DELETE): Delete an item by ID.

Add the following code after the data store definition:

// Middleware to parse JSON requests
app.use(express.json());

// Create (POST) a new item
app.post('/items', (req, res) => {
  const newItem = req.body;
  data.push(newItem);
  res.status(201).json(newItem);
});

// Read (GET) all items
app.get('/items', (req, res) => {
  res.json(data);
});

// Read (GET) a specific item by ID
app.get('/items/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const item = data.find((item) => item.id === id);
  if (!item) {
    res.status(404).json({ error: 'Item not found' });
  } else {
    res.json(item);
  }
});

// Update (PUT) an item by ID
app.put('/items/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const updatedItem = req.body;
  const index = data.findIndex((item) => item.id === id);
  if (index === -1) {
    res.status(404).json({ error: 'Item not found' });
  } else {
    data[index] = { ...data[index], ...updatedItem };
    res.json(data[index]);
  }
});

// Delete (DELETE) an item by ID
app.delete('/items/:id', (req, res) => {
      const id = parseInt(req.params.id);
      const index = data.findIndex((item) => item.id === id);
      if (index === -1) {
        res.status(404).json({ error: 'Item not found' });
      } else {
        const deletedItem = data.splice(index, 1);
        res.json(deletedItem[0]);
      }
});
In this code:

We use Express middleware (express.json()) to parse JSON requests.

We define routes for each CRUD operation, specifying the HTTP method (e.g., POST, GET, PUT, DELETE) and the route path (e.g., /items).

Inside each route handler, we perform the respective CRUD operation on the data array and send a JSON response.

3. Start Your Express Server

Start your Express server as before:

node server.js
If the server is already running try closing the first one by pressing: CTRL + c

Now, you can use tools like Postman or curl to test your CRUD operations. Here are some example requests:

Create (POST) a new item:
POST http://localhost:3000/items
Body: { "name": "New Item" }
Read (GET) all items: You can use postman or curl or browser for get requests
GET http://localhost:3000/items
Read (GET) a specific item by ID:
GET http://localhost:3000/items/1

Update (PUT) an item by ID:
PUT http://localhost:3000/items/1
Body: { "name": "Updated Item" }
Delete (DELETE) an item by ID:
DELETE http://localhost:3000/items/1
Remember that this is a simple example using an in-memory data store. In a real application, you’d likely use a database for more robust data storage and management.

Adding Authentication to the API
Adding authentication to your API is an essential step to secure it. There are various authentication methods you can use in Express.js. Below, I’ll guide you through adding a basic token-based authentication using JSON Web Tokens (JWT). This is just one way to implement authentication; in a production environment, you may want to consider more advanced techniques and libraries.

Install Dependencies
First, you need to install the necessary packages for JWT authentication and password hashing. You can use jsonwebtoken and bcrypt for this purpose:

npm install jsonwebtoken bcrypt
2. Import the Dependencies

In your server.js file, import these dependencies at the top after port part:

const jwt = require('jsonwebtoken');
const bcrypt = require('bcrypt');
3. Create a Secret Key

Generate a secret key for JWT token signing. You should store this securely, preferably in an environment variable in a real application.

const secretKey = 'your-secret-key'; // Replace with a strong, secret key
4. User Data and Authentication Logic

For this example, we’ll assume a simple user database with usernames and hashed passwords. In a real application, you would use a database like MongoDB or PostgreSQL for user storage. Here’s a simplified example, add the following code at the end of server.js file:

// Sample user data (replace with a real database)
const users = [
  { id: 1, username: 'user1', password: '$2b$10$kgix/7wKMGMmqJYixdfvfugaj5W/iHKcjArX2H76DVIZmQzXr7/hJ' }, // Hashed password: "password1"
  { id: 2, username: 'user2', password: '$2b$10$kgix/7wKMGMmqJYixdfvfugaj5W/iHKcjArX2H76DVIZmQzXr7/hJ' }, // Hashed password: "password2"
];

// Function to verify user credentials
function authenticateUser(username, password) {
  const user = users.find((user) => user.username === username);
  if (!user) {
     return null; // User not found
  }
  if (bcrypt.compareSync(password, user.password)) {
    return user; // Password is correct
  }
  return null; // Password is incorrect
}
5. Create an Authentication Route

Define an authentication route where users can log in and receive a JWT token if their credentials are correct. Add the following code at the end of server.js file:

app.post('/auth/login', (req, res) => {
  const { username, password } = req.body;
  const user = authenticateUser(username, password);

  if (!user) {
    return res.status(401).json({ error: 'Authentication failed' });
  }

  const token = jwt.sign({ userId: user.id, username: user.username }, secretKey, {
        expiresIn: '1h', // Token expiration time
  });

  res.json({ token });
});
6. Secure Routes with Authentication Middleware

To protect routes that require authentication, you can create a middleware function that checks the JWT token in the request header.

function authenticateToken(req, res, next) {
  const token = req.header('Authorization');

  if (!token) {
    return res.status(401).json({ error: 'Authentication token missing' });
  }

  jwt.verify(token, secretKey, (err, user) => {
    if (err) {
      return res.status(403).json({ error: 'Token is invalid'});
    }
    req.user = user;
    next(); // Continue to the protected route
  });
}

// Example usage:
app.get('/protected', authenticateToken, (req, res) => {
  res.json({ message: 'This is a protected route', user: req.user });
});

In this example, the authenticateToken middleware checks if a valid JWT token is included in the Authorization header. If it's valid, it attaches the user information to the request object (req.user) and allows access to the protected route. Otherwise, it returns an error response.

Now, you have a basic token-based authentication system in your Express.js API. Users can log in to receive a JWT token, and you can secure specific routes by adding the authenticateToken middleware to them.

Conclusion
So, we’ve reached the end of our journey through creating a Restful API using Node.js and Express, including CRUD operations and authentication. Let’s quickly recap the key points we’ve covered so far.

Firstly, we explored what a Restful API is and why Node.js and Express are great choices for building one. Then, we dived into setting up our development environment, which is the foundation for our API.

Next, we created a basic Express server, following a step-by-step guide that included installing Express, creating a new project directory, initializing the project with a package.json file, installing dependencies, creating an entry point file, and finally setting up the Express server itself.

After that, we implemented CRUD operations by adding a data store, setting up API routes, and coding the operations to create, read, update, and delete data.

Lastly, we added authentication to our API by installing the necessary packages, creating a protected route, setting up authentication middleware, and securing our API endpoints.
