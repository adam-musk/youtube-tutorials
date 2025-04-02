---
layout: "../../layouts/BlogPost.astro"
title: "Backend Development Fundamentals: Building a CRUD API with Node.js, Express, and MongoDB"
pubDate: "2025-03-02 14:32:37.637882"
youtubeVideoID: "_7UQPve99r4"
index:
---

# Backend Development Fundamentals: Building a CRUD API with Node.js, Express, and MongoDB

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/_7UQPve99r4" frameborder="0" allowfullscreen></iframe>

This chapter provides a beginner's guide to backend development, focusing on building a **CRUD (Create, Read, Update, Delete)** API using Node.js, Express, and MongoDB. We will construct a RESTful API from scratch, leveraging the core components of the **MERN stack** (MongoDB, Express, React, Node.js), albeit without the React frontend (hence, "MERN stack without the R"). This hands-on approach will solidify your understanding of backend principles and equip you with the skills to create functional APIs.

> **CRUD (Create, Read, Update, Delete):**  CRUD represents the four basic operations that can be performed on data in a database. These operations are fundamental to most applications that manage persistent data.

> **API (Application Programming Interface):** An API is a set of rules and specifications that software programs can follow to communicate with each other. In web development, APIs often define how different software components should interact over a network.

> **RESTful API (Representational State Transfer API):** A RESTful API is an architectural style for designing networked applications. It relies on a stateless, client-server communication protocol, and often uses standard HTTP methods (GET, POST, PUT, DELETE) to perform operations.

> **MERN Stack:** MERN is an acronym for MongoDB, Express.js, React.js, and Node.js. It represents a popular JavaScript-based technology stack used for building full-stack web applications.

## Prerequisites

Before we begin, ensure you have the following software installed on your system:

*   **Visual Studio Code (VS Code):** A powerful and widely used code editor. Download and install it from the official website.
*   **Node.js:** A JavaScript runtime environment that allows you to run JavaScript code outside of a web browser.

    *   Download the "Latest LTS Version" from [nodejs.org](https://nodejs.org/).
    *   Follow the installation steps provided by the installer.
    *   Verify the installation by opening your command prompt (CMD) or terminal and typing:
        ```bash
        node --version
        ```
        This command should display the installed Node.js version.

## Project Setup

1.  **Create a Project Folder:**
    *   Create a new folder on your computer to house your project. Name it something descriptive, such as `simple-crud-app`.

2.  **Open the Project in VS Code:**
    *   Navigate into your project folder.
    *   Right-click within the folder and select "Open with Code" (or open VS Code and then open the folder).

3.  **Initialize a Node.js Project:**
    *   Open the integrated terminal in VS Code (using the shortcut `Ctrl + `backtick`` or by selecting "Terminal" > "New Terminal" from the menu).
    *   In the terminal, run the following command to initialize a `package.json` file:
        ```bash
        npm init -y
        ```

        > **npm (Node Package Manager):** npm is the default package manager for Node.js. It is used to install, manage, and share JavaScript packages and libraries.

        > **package.json:** This file is essential for Node.js projects. It contains metadata about the project, including its name, version, dependencies, and scripts.

    *   This command creates a `package.json` file in your project directory with default settings. You can examine this file to understand its structure and initial content.

## Creating the Backend Server (Express.js)

1.  **Create `index.js`:**
    *   In VS Code, create a new file named `index.js` in the root of your project folder. This file will serve as the main entry point for your backend application.

2.  **Install Express.js:**
    *   Open your terminal (if it's not already open).
    *   Run the following command to install Express.js and save it as a project dependency:
        ```bash
        npm install express
        ```

        > **Express.js:** Express.js is a minimalist and flexible Node.js web application framework that provides a robust set of features for building web and mobile applications. It simplifies the process of creating server-side applications with Node.js.

    *   This command will download and install Express.js and add it to the `dependencies` section of your `package.json` file. You will also notice a `node_modules` folder and a `package-lock.json` file created in your project.

        > **node_modules:** This folder contains all the installed npm packages and their dependencies for your project.

        > **package-lock.json:** This file ensures that dependencies are installed consistently across different environments by locking down the specific versions of packages used.

3.  **Basic Express Server in `index.js`:**
    *   Open `index.js` and add the following code:

        ```javascript
        const express = require('express');
        const app = express();
        const port = 3000;

        app.get('/', (req, res) => {
          res.send('Hello from Node API Server!');
        });

        app.listen(port, () => {
          console.log(`Server is running on port ${port}`);
        });
        ```

    *   **Explanation:**
        *   `const express = require('express');`: Imports the Express.js library.
        *   `const app = express();`: Creates an Express application instance.
        *   `const port = 3000;`: Defines the port number on which the server will listen (port 3000 is commonly used for development).
        *   `app.get('/', (req, res) => { ... });`: Defines a route for handling GET requests to the root path (`/`).
            *   `req` (request): An object containing information about the incoming HTTP request from the client.
            *   `res` (response): An object used to send responses back to the client.
            *   `res.send('Hello from Node API Server!');`: Sends a simple text response back to the client.
        *   `app.listen(port, () => { ... });`: Starts the server and makes it listen for incoming requests on the specified port.
            *   The callback function `() => { ... }` is executed once the server starts successfully.
            *   `console.log(...)`: Logs a message to the console indicating that the server is running.

4.  **Run the Server:**
    *   In your terminal, run the following command to start the server using Node.js:
        ```bash
        node index.js
        ```
    *   You should see the message `Server is running on port 3000` in your terminal.

5.  **Access the API in a Browser:**
    *   Open your web browser and navigate to `http://localhost:3000`.
    *   You should see the message "Hello from Node API Server!" displayed in your browser.

## Testing APIs with Tools: Thunder Client, Insomnia, and Postman

To effectively test your API endpoints (especially those beyond simple GET requests in a browser), dedicated API testing tools are invaluable. Here's a brief overview of popular options:

*   **Thunder Client (VS Code Extension):** A lightweight and integrated API client directly within VS Code. It's convenient for quick testing during development.

*   **Insomnia:** A feature-rich, standalone API client available as a desktop application. It offers advanced features like collections, environments, and collaboration. You can download the free version from [insomnia.rest](https://insomnia.rest/).

*   **Postman:** Another widely used, powerful API platform for building, testing, and documenting APIs. It also offers a desktop application and a web interface. You can download the free version from [postman.com](https://postman.com/).

These tools allow you to:

*   **Send requests to different API endpoints.**
*   **Specify HTTP methods (GET, POST, PUT, DELETE, etc.).**
*   **Set headers and request bodies (e.g., JSON data).**
*   **Inspect responses (status codes, headers, body).**
*   **Organize and save API requests for reuse.**

For this tutorial, you can choose any of these tools to test the API endpoints we will build.

## Version Control with Git and Ignoring `node_modules`

> **Git:** Git is a distributed version control system that tracks changes in files over time. It is essential for managing code, collaborating with others, and reverting to previous versions if needed.

1.  **Install Git Bash (if not already installed):**
    *   Git is often pre-installed on macOS and Linux systems. For Windows, download and install Git Bash from [git-scm.com](https://git-scm.com/download/win).
    *   Verify installation by running `git --version` in your terminal.

2.  **Create `.gitignore` File:**
    *   In the root of your project, create a new file named `.gitignore` (no file extension).
    *   Add the following line to the `.gitignore` file:
        ```
        node_modules
        ```

        > **.gitignore:** This file specifies intentionally untracked files that Git should ignore. It is commonly used to exclude temporary files, build artifacts, and dependency folders like `node_modules` from version control.

    *   This ensures that the `node_modules` folder (which can be large and is easily regenerated) is not included when you commit your code to Git repositories like GitHub.

## Automatic Server Restart with Nodemon

> **Nodemon:** Nodemon is a utility that automatically restarts your Node.js application when it detects file changes in the directory. This significantly improves development workflow by eliminating the need to manually restart the server after every code modification.

1.  **Install Nodemon as a Development Dependency:**
    *   In your terminal, run the following command:
        ```bash
        npm install nodemon -D
        ```

        *   `-D` or `--save-dev`:  Installs Nodemon as a development dependency, meaning it's primarily used during development and not necessarily required in production.

2.  **Configure `npm run dev` Script:**
    *   Open your `package.json` file.
    *   In the `scripts` section, add a new script named `dev`:

        ```json
        "scripts": {
          "test": "echo \"Error: no test specified\" && exit 1",
          "serve": "node index.js",
          "dev": "nodemon index.js"
        },
        ```

    *   **Explanation:**
        *   `"dev": "nodemon index.js"`: This script defines a new command `npm run dev`. When executed, it will run `nodemon index.js`, which starts your server using Nodemon.

3.  **Run the Server with Nodemon:**
    *   In your terminal, run:
        ```bash
        npm run dev
        ```
    *   You will see a Nodemon-specific message indicating that it's monitoring your files.
    *   Now, whenever you save changes to your `index.js` or other project files, Nodemon will automatically restart the server, and you can immediately see the updates in your browser or API testing tool without manual restarts.

## Connecting to MongoDB Atlas

> **MongoDB:** MongoDB is a popular NoSQL database that stores data in flexible, JSON-like documents. It is well-suited for web applications due to its scalability and ease of use.

> **MongoDB Atlas:** MongoDB Atlas is a fully managed cloud database service provided by MongoDB. It simplifies the process of setting up, operating, and scaling MongoDB deployments.

1.  **Sign up for MongoDB Atlas:**
    *   Go to [mongodb.com/atlas](https://mongodb.com/atlas) and sign up for a free account.

2.  **Create a New Project and Cluster:**
    *   Once logged in, create a new project (e.g., "node-api").
    *   Within the project, create a new cluster. Choose the "M0 Free Tier" option for development purposes.
    *   Select your preferred region (e.g., Mumbai if geographically closer).
    *   You can name your cluster (e.g., "backendDB").
    *   Click "Create Cluster."

3.  **Configure Database Access and Network Access:**
    *   **Database Access:**
        *   Set up a username and password for database access.  **Important:** Store these credentials securely.
        *   Click "Create User."
    *   **Network Access:**
        *   Choose "Add My Current IP Address" for local development, or "Allow Access from Anywhere" (0.0.0.0/0) for broader access (use with caution in production, consider restricting IP access).
        *   Click "Add Entry" and then "Finish and Close."

4.  **Get the Connection String:**
    *   Click the "Connect" button for your cluster.
    *   Select "Drivers" and choose "Node.js" as the driver and the latest Node.js version.
    *   Copy the provided connection string. It will look something like this:
        ```
        mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/?retryWrites=true&w=majority
        ```
    *   **Important:** Replace `<username>` and `<password>` with the username and password you created, and `<cluster-name>` with your cluster name.

5.  **Install MongoDB Driver for Node.js:**
    *   In your terminal, stop your server (`Ctrl + C` if running with `npm run dev`).
    *   Run the following command to install the official MongoDB driver:
        ```bash
        npm install mongodb
        ```

6.  **Install Mongoose ODM (Optional but Recommended):**
    *   Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides a higher-level abstraction for interacting with MongoDB, making it easier to define schemas, validate data, and perform database operations.
    *   Install Mongoose:
        ```bash
        npm install mongoose
        ```

        > **Mongoose:** Mongoose is a popular Object Data Modeling (ODM) library for MongoDB and Node.js. It simplifies database interactions by providing schema definitions, data validation, and query building tools.

7.  **Connect to MongoDB in `index.js` using Mongoose:**
    *   Modify your `index.js` file to include the following code (replace `"YOUR_MONGODB_CONNECTION_STRING"` with the actual connection string you copied from MongoDB Atlas):

        ```javascript
        const express = require('express');
        const mongoose = require('mongoose'); // Import Mongoose
        const app = express();
        const port = 3000;

        // Middleware to parse JSON request bodies
        app.use(express.json());

        // Middleware to parse URL-encoded request bodies
        app.use(express.urlencoded({ extended: false }));

        // MongoDB Connection
        mongoose.connect("YOUR_MONGODB_CONNECTION_STRING", {
          useNewUrlParser: true, // Recommended options for newer MongoDB drivers
          useUnifiedTopology: true,
        })
        .then(() => {
          console.log("Connected to MongoDB Database");
        })
        .catch((error) => {
          console.error("MongoDB Connection Failed", error);
        });

        app.get('/', (req, res) => {
          res.send('Hello from Node API Server!');
        });

        app.listen(port, () => {
          console.log(`Server is running on port ${port}`);
        });
        ```

    *   **Explanation:**
        *   `const mongoose = require('mongoose');`: Imports the Mongoose library.
        *   `mongoose.connect(...)`: Establishes a connection to your MongoDB database using the provided connection string.
        *   `.then(...)`:  A promise-based approach to handle successful connection. If the connection is successful, it logs "Connected to MongoDB Database" to the console.
        *   `.catch(...)`: Handles potential connection errors. If the connection fails, it logs "MongoDB Connection Failed" and the error details to the console.
        *   `useNewUrlParser: true, useUnifiedTopology: true`: These are recommended options for newer MongoDB drivers to avoid deprecation warnings and ensure proper functionality.

8.  **Run the Server Again:**
    *   Start your server using `npm run dev`.
    *   If the connection is successful, you should see the message "Connected to MongoDB Database" in your console, along with "Server is running on port 3000".

## Defining a Mongoose Schema and Model

> **Schema:** In Mongoose, a schema defines the structure of documents within a MongoDB collection. It specifies the fields, data types, validation rules, and other properties of the data.

> **Model:** A Mongoose model is a constructor compiled from a schema definition.  Models allow you to create instances of documents, save them to the database, query data, and perform other database operations based on the defined schema.

1.  **Create a `models` Folder:**
    *   In your project root, create a new folder named `models`.

2.  **Create `product.model.js`:**
    *   Inside the `models` folder, create a new file named `product.model.js`.
    *   Add the following code to define a product schema and model:

        ```javascript
        const mongoose = require('mongoose');

        const productSchema = new mongoose.Schema(
          {
            name: {
              type: String,
              required: [true, "Please enter product name"],
            },
            quantity: {
              type: Number,
              required: true,
              default: 0,
            },
            price: {
              type: Number,
              required: true,
              default: 0,
            },
            image: {
              type: String,
              required: false, // Image is optional
            },
          },
          {
            timestamps: true, // Automatically adds createdAt and updatedAt fields
          }
        );

        const Product = mongoose.model('Product', productSchema); // 'Product' model for 'products' collection (Mongoose pluralizes)
        module.exports = Product; // Export the model
        ```

    *   **Explanation:**
        *   `const productSchema = new mongoose.Schema({...});`: Creates a new Mongoose schema named `productSchema`.
        *   **Schema Definition:**
            *   `name`: String, required, with a custom error message for validation failure.
            *   `quantity`: Number, required, default value of 0.
            *   `price`: Number, required, default value of 0.
            *   `image`: String, optional (not required).
        *   `timestamps: true`: Enables automatic creation and updating of `createdAt` and `updatedAt` timestamp fields for each document.
        *   `const Product = mongoose.model('Product', productSchema);`: Creates a Mongoose model named `Product` based on the `productSchema`. Mongoose will automatically create a MongoDB collection named "products" (pluralized and lowercase version of the model name).
        *   `module.exports = Product;`: Exports the `Product` model so it can be used in other files.

## Implementing CRUD Operations

Now, let's implement the CRUD operations for our `Product` model in `index.js`.

### 1. Create (POST) - Add a Product

1.  **Import the `Product` Model in `index.js`:**
    *   At the top of your `index.js` file, after importing `mongoose`, add:

        ```javascript
        const Product = require('./models/product.model');
        ```

2.  **Create a POST Route for Adding Products:**
    *   In `index.js`, add the following route handler:

        ```javascript
        app.post('/api/products', async (req, res) => {
          try {
            const product = await Product.create(req.body); // Create a new product document
            res.status(200).json(product); // Respond with the created product
          } catch (error) {
            console.error("Error creating product:", error);
            res.status(500).json({ message: error.message }); // Respond with error message
          }
        });
        ```

    *   **Explanation:**
        *   `app.post('/api/products', ...)`: Defines a route for handling POST requests to `/api/products`. This endpoint will be used to create new products.
        *   `async (req, res) => { ... }`:  Marks the route handler as asynchronous, allowing the use of `await` for database operations.
        *   `try...catch`:  Implements error handling.
        *   `const product = await Product.create(req.body);`:
            *   `Product.create(req.body)`: Uses the `Product` model's `create()` method to create a new product document in the database.  `req.body` is expected to contain the product data (name, quantity, price, image) sent in the request body (typically in JSON format).
            *   `await`:  Pauses execution until the `Product.create()` operation completes.
        *   `res.status(200).json(product);`: If successful, sends a 200 OK status code and the newly created `product` document in JSON format as the response.
        *   `res.status(500).json({ message: error.message });`: If an error occurs during product creation, sends a 500 Internal Server Error status code and an error message in JSON format.

3.  **Test the POST API:**
    *   Start your server (`npm run dev`).
    *   Use Insomnia, Postman, or Thunder Client:
        *   Create a new POST request.
        *   Set the URL to `http://localhost:3000/api/products`.
        *   Set the request body type to "JSON".
        *   In the body, provide product data in JSON format, for example:

            ```json
            {
              "name": "Pizza",
              "quantity": 10,
              "price": 5.99
            }
            ```
        *   Send the request.
        *   You should receive a 200 OK response with the created product data (including the MongoDB-generated `_id` and timestamps) in the response body. You can also verify that the product is added to your MongoDB Atlas collection by browsing collections in Atlas.

### 2. Read (GET) - Get All Products

1.  **Create a GET Route for Retrieving All Products:**
    *   In `index.js`, add the following route handler:

        ```javascript
        app.get('/api/products', async (req, res) => {
          try {
            const products = await Product.find({}); // Find all product documents
            res.status(200).json(products); // Respond with the array of products
          } catch (error) {
            console.error("Error fetching products:", error);
            res.status(500).json({ message: error.message }); // Respond with error message
          }
        });
        ```

    *   **Explanation:**
        *   `app.get('/api/products', ...)`: Defines a route for handling GET requests to `/api/products`. This endpoint will retrieve all products.
        *   `const products = await Product.find({});`:
            *   `Product.find({})`: Uses the `Product` model's `find()` method to retrieve all documents from the "products" collection. The empty object `{}` as the argument means "find all".
            *   `await`: Pauses execution until the `Product.find()` operation completes.
        *   `res.status(200).json(products);`: If successful, sends a 200 OK status code and an array of all `product` documents in JSON format as the response.

2.  **Test the GET All API:**
    *   Start your server (`npm run dev`).
    *   Use Insomnia, Postman, or Thunder Client:
        *   Create a new GET request.
        *   Set the URL to `http://localhost:3000/api/products`.
        *   Send the request.
        *   You should receive a 200 OK response with an array of product objects in JSON format.

### 3. Read (GET) - Get a Single Product by ID

1.  **Create a GET Route for Retrieving a Single Product:**
    *   In `index.js`, add the following route handler:

        ```javascript
        app.get('/api/products/:id', async (req, res) => {
          try {
            const { id } = req.params; // Extract the product ID from the URL parameters
            const product = await Product.findById(id); // Find product by ID
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` }); // Respond with 404 if product not found
            }
            res.status(200).json(product); // Respond with the found product
          } catch (error) {
            console.error("Error fetching product:", error);
            res.status(500).json({ message: error.message }); // Respond with error message
          }
        });
        ```

    *   **Explanation:**
        *   `app.get('/api/products/:id', ...)`: Defines a route for handling GET requests to `/api/products/:id`. The `:id` is a URL parameter placeholder that will capture the product ID from the URL.
        *   `const { id } = req.params;`: Extracts the value of the `id` URL parameter from `req.params`.
        *   `const product = await Product.findById(id);`:
            *   `Product.findById(id)`: Uses the `Product` model's `findById()` method to search for a product document with the matching `_id` (MongoDB's unique identifier).
            *   `await`: Pauses execution until the `Product.findById()` operation completes.
        *   `if (!product) { ... }`: Checks if a product with the given ID was found. If not found (`product` is null), it returns a 404 Not Found status code and an error message.
        *   `res.status(200).json(product);`: If a product is found, sends a 200 OK status code and the `product` document in JSON format.

2.  **Test the GET Single API:**
    *   Start your server (`npm run dev`).
    *   Use Insomnia, Postman, or Thunder Client:
        *   Create a new GET request.
        *   Set the URL to `http://localhost:3000/api/products/{product_id}`. Replace `{product_id}` with the actual `_id` of a product from your database (you can get this ID from the GET All Products API response).
        *   Send the request.
        *   You should receive a 200 OK response with the details of the specific product in JSON format. If you use an invalid or non-existent ID, you should receive a 404 Not Found response.

### 4. Update (PUT) - Update a Product by ID

1.  **Create a PUT Route for Updating a Product:**
    *   In `index.js`, add the following route handler:

        ```javascript
        app.put('/api/products/:id', async (req, res) => {
          try {
            const { id } = req.params; // Extract product ID
            const product = await Product.findByIdAndUpdate(id, req.body, {
              new: true, // Return the updated document
              runValidators: true, // Run schema validators during update
            });
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` }); // 404 if product not found
            }
            res.status(200).json(product); // Respond with the updated product
          } catch (error) {
            console.error("Error updating product:", error);
            res.status(500).json({ message: error.message }); // Respond with error message
          }
        });
        ```

    *   **Explanation:**
        *   `app.put('/api/products/:id', ...)`: Defines a route for handling PUT requests to `/api/products/:id`.
        *   `const product = await Product.findByIdAndUpdate(id, req.body, { ... });`:
            *   `Product.findByIdAndUpdate(id, req.body, { ... })`: Uses the `Product` model's `findByIdAndUpdate()` method to find a product by its `_id` and update it with the data provided in `req.body`.
            *   `id`: The product ID to update.
            *   `req.body`: The data to update the product with (sent in the request body, typically JSON).
            *   `{ new: true, runValidators: true }`: Options object:
                *   `new: true`:  Ensures that the method returns the *updated* document after the modification, not the original document before the update.
                *   `runValidators: true`:  Forces Mongoose to run the schema validators defined in `productSchema` during the update operation, ensuring data integrity.
        *   Error handling and 404 response logic are similar to the GET Single API.

2.  **Test the PUT API:**
    *   Start your server (`npm run dev`).
    *   Use Insomnia, Postman, or Thunder Client:
        *   Create a new PUT request.
        *   Set the URL to `http://localhost:3000/api/products/{product_id}` (replace `{product_id}`).
        *   Set the request body type to "JSON".
        *   In the body, provide the fields you want to update, for example, to update the price:

            ```json
            {
              "price": 7.99
            }
            ```
        *   Send the request.
        *   You should receive a 200 OK response with the updated product data in JSON format. Verify the update by fetching the product again using the GET Single API.

### 5. Delete (DELETE) - Delete a Product by ID

1.  **Create a DELETE Route for Deleting a Product:**
    *   In `index.js`, add the following route handler:

        ```javascript
        app.delete('/api/products/:id', async (req, res) => {
          try {
            const { id } = req.params; // Extract product ID
            const product = await Product.findByIdAndDelete(id); // Delete product by ID
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` }); // 404 if product not found
            }
            res.status(200).json({ message: "Product deleted successfully" }); // Respond with success message
          } catch (error) {
            console.error("Error deleting product:", error);
            res.status(500).json({ message: error.message }); // Respond with error message
          }
        });
        ```

    *   **Explanation:**
        *   `app.delete('/api/products/:id', ...)`: Defines a route for handling DELETE requests to `/api/products/:id`.
        *   `const product = await Product.findByIdAndDelete(id);`:
            *   `Product.findByIdAndDelete(id)`: Uses the `Product` model's `findByIdAndDelete()` method to find a product by its `_id` and delete it from the database.
            *   `await`: Pauses execution until the `Product.findByIdAndDelete()` operation completes.
        *   Error handling and 404 response logic are similar to the GET Single API.
        *   `res.status(200).json({ message: "Product deleted successfully" });`: If successful, sends a 200 OK status code and a success message in JSON format.

2.  **Test the DELETE API:**
    *   Start your server (`npm run dev`).
    *   Use Insomnia, Postman, or Thunder Client:
        *   Create a new DELETE request.
        *   Set the URL to `http://localhost:3000/api/products/{product_id}` (replace `{product_id}`).
        *   Send the request.
        *   You should receive a 200 OK response with the message "Product deleted successfully" in JSON format. Verify deletion by attempting to fetch the product again using the GET Single API (which should now return a 404) or by using the GET All Products API (the deleted product should no longer be listed).

## Handling Form URL-Encoded Data

> **Middleware:** In Express.js, middleware functions are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application’s request-response cycle. Middleware functions can perform various tasks, such as parsing request bodies, handling authentication, logging, and more.

By default, Express.js only parses JSON request bodies using the `express.json()` middleware. If you want to handle form data submitted using `application/x-www-form-urlencoded` (common for HTML forms), you need to add the `express.urlencoded()` middleware:

```javascript
app.use(express.urlencoded({ extended: false }));
```

*   `extended: false`:  Uses the built-in querystring library for parsing. For more complex scenarios, you might use `extended: true` (which uses the `qs` library), but `false` is sufficient for basic form data.

We added this middleware earlier in the `index.js` file. Now, your API can handle both JSON and form URL-encoded data in POST and PUT requests.

## Refactoring for Better Code Organization: Routes and Controllers

For larger applications, it's best practice to separate your route definitions and request handling logic into separate files and folders to improve code organization and maintainability.

1.  **Create `routes` and `controllers` Folders:**
    *   In your project root, create two new folders: `routes` and `controllers`.

2.  **Create `product.route.js` in `routes` Folder:**
    *   Inside the `routes` folder, create a new file named `product.route.js`.
    *   Add the following code to define product routes:

        ```javascript
        const express = require('express');
        const router = express.Router(); // Create an Express Router instance
        const productController = require('../controllers/product.controller'); // Import product controller functions

        // Define routes and associate them with controller functions
        router.get('/', productController.getProducts); // GET all products
        router.get('/:id', productController.getProduct); // GET single product by ID
        router.post('/', productController.createProduct); // POST - create a new product
        router.put('/:id', productController.updateProduct); // PUT - update a product by ID
        router.delete('/:id', productController.deleteProduct); // DELETE - delete a product by ID

        module.exports = router; // Export the router
        ```

    *   **Explanation:**
        *   `const router = express.Router();`: Creates an Express Router instance. Routers are used to define modular sets of routes.
        *   `const productController = require('../controllers/product.controller');`: Imports the controller functions from `product.controller.js` (which we will create next).
        *   `router.get('/', productController.getProducts);`: Defines a GET route for `/` (which will be `/api/products` when mounted in `index.js`) and associates it with the `getProducts` function from the `productController`. Similar routing is done for other CRUD operations.
        *   `module.exports = router;`: Exports the `router` instance so it can be used in `index.js`.

3.  **Create `product.controller.js` in `controllers` Folder:**
    *   Inside the `controllers` folder, create a new file named `product.controller.js`.
    *   Add the following code to define controller functions (copy the logic from your route handlers in `index.js` and paste them into these functions):

        ```javascript
        const Product = require('../models/product.model');

        // Controller function to get all products
        exports.getProducts = async (req, res) => {
          try {
            const products = await Product.find({});
            res.status(200).json(products);
          } catch (error) {
            console.error("Error fetching products:", error);
            res.status(500).json({ message: error.message });
          }
        };

        // Controller function to get a single product by ID
        exports.getProduct = async (req, res) => {
          try {
            const { id } = req.params;
            const product = await Product.findById(id);
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` });
            }
            res.status(200).json(product);
          } catch (error) {
            console.error("Error fetching product:", error);
            res.status(500).json({ message: error.message });
          }
        };

        // Controller function to create a new product
        exports.createProduct = async (req, res) => {
          try {
            const product = await Product.create(req.body);
            res.status(200).json(product);
          } catch (error) {
            console.error("Error creating product:", error);
            res.status(500).json({ message: error.message });
          }
        };

        // Controller function to update a product by ID
        exports.updateProduct = async (req, res) => {
          try {
            const { id } = req.params;
            const product = await Product.findByIdAndUpdate(id, req.body, {
              new: true,
              runValidators: true,
            });
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` });
            }
            res.status(200).json(product);
          } catch (error) {
            console.error("Error updating product:", error);
            res.status(500).json({ message: error.message });
          }
        };

        // Controller function to delete a product by ID
        exports.deleteProduct = async (req, res) => {
          try {
            const { id } = req.params;
            const product = await Product.findByIdAndDelete(id);
            if (!product) {
              return res.status(404).json({ message: `Product not found with ID: ${id}` });
            }
            res.status(200).json({ message: "Product deleted successfully" });
          } catch (error) {
            console.error("Error deleting product:", error);
            res.status(500).json({ message: error.message });
          }
        };
        ```

    *   **Explanation:**
        *   Each function (`getProducts`, `getProduct`, `createProduct`, `updateProduct`, `deleteProduct`) corresponds to one of the CRUD operations.
        *   The code within each function is essentially the request handling logic that was previously in your `index.js` route handlers.
        *   `exports.functionName = ...`: Exports each function so it can be imported and used in `product.route.js`.

4.  **Mount the Product Router in `index.js`:**
    *   In your `index.js` file, replace the individual route definitions (`app.get('/api/products', ...)`, `app.post('/api/products', ...)`, etc.) with the following middleware mounting line:

        ```javascript
        const productRoute = require('./routes/product.route'); // Import the product route

        // ... other code ...

        // Mount the product routes at /api/products
        app.use('/api/products', productRoute);

        // ... rest of index.js ...
        ```

    *   **Explanation:**
        *   `const productRoute = require('./routes/product.route');`: Imports the `router` instance exported from `product.route.js`.
        *   `app.use('/api/products', productRoute);`: Mounts the `productRoute` at the path `/api/products`. This means that all routes defined in `product.route.js` will now be prefixed with `/api/products`. For example, the route defined as `router.get('/', ...)` in `product.route.js` will now be accessible at `/api/products/` in your application.

5.  **Clean up `index.js`:**
    *   Remove the individual route handlers for products (the `app.get('/api/products', ...)`, `app.post('/api/products', ...)`, etc. blocks) from your `index.js` file as they are now handled by the `productRoute`. Your `index.js` should now be significantly cleaner and primarily responsible for server setup, middleware configuration, and database connection.

6.  **Test Again:**
    *   Start your server (`npm run dev`).
    *   Test all your CRUD API endpoints using Insomnia, Postman, or Thunder Client. Everything should function exactly as before, but your code is now much better organized.

## Pushing Code to GitHub

1.  **Create a GitHub Repository:**
    *   Go to [github.com](https://github.com) and create a new repository (e.g., "simple-crud-app-backend").

2.  **Initialize Git and Commit (if not already done):**
    *   If you haven't already initialized Git in your project (using `git init`) and made an initial commit (`git add .`, `git commit -m "Initial commit"`), do so now.

3.  **Add Remote Repository:**
    *   In your terminal, run the following command, replacing `<your_github_username>` and `<repository_name>` with your GitHub username and repository name:
        ```bash
        git remote add origin https://github.com/<your_github_username>/<repository_name>.git
        ```

4.  **Push to GitHub:**
    *   Push your local repository to the remote GitHub repository:
        ```bash
        git push -u origin main
        ```
    *   This will upload your code to GitHub. You can now access your project code online in your GitHub repository.

## Conclusion

Congratulations! You have successfully built a complete RESTful CRUD API for managing products using Node.js, Express, and MongoDB. This chapter covered fundamental backend development concepts, including:

*   Setting up a Node.js project.
*   Creating an Express.js server.
*   Connecting to a MongoDB Atlas database.
*   Defining Mongoose schemas and models.
*   Implementing CRUD operations (Create, Read, Update, Delete).
*   Testing APIs with tools like Insomnia and Postman.
*   Organizing code with routes and controllers.
*   Using Git for version control and pushing to GitHub.

This project serves as a solid foundation for further exploration into backend development. You can expand upon this API by adding features like:

*   Authentication and authorization.
*   More complex data models and relationships.
*   File uploads.
*   Search and filtering functionalities.
*   Deployment to a cloud platform.

Keep practicing and building, and you'll become a proficient backend developer!
