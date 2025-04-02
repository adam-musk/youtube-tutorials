---
layout: "../../layouts/BlogPost.astro"
title: "Creating an API Proxy Server with Node.js: A Comprehensive Guide"
pubDate: "2025-03-08 15:49:34.347871"
youtubeVideoID: "ZGymN8aFsv4"
---

# Creating an API Proxy Server with Node.js: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/ZGymN8aFsv4" frameborder="0" allowfullscreen></iframe>

## Introduction: The Need for API Proxy Servers

In modern web development, utilizing third-party APIs (Application Programming Interfaces) is commonplace. These APIs, such as the GitHub API, Twitter API, or OpenWeatherMap API (as used in this example), provide access to valuable data and functionalities. However, a common security challenge arises when using these APIs: **API keys**.

> **API (Application Programming Interface)**
> An API is a set of rules and specifications that software programs can follow to communicate with each other. It allows developers to access certain features or data of an application, service, or platform, without needing to know the underlying implementation.

> **API Key**
> An API key is a code used to identify and authenticate an application or user making requests to an API. It's often required by API providers to track usage, manage access, and ensure security.

Many APIs require you to include your API key directly in the URL when making requests. While seemingly straightforward, this practice poses a significant security risk, especially in client-side applications. Exposing API keys in client-side code, such as JavaScript in a web browser, makes them vulnerable to theft. Anyone inspecting the source code of your webpage can easily find and misuse your API key.

This chapter will guide you through creating an **API proxy server** using Node.js. This server acts as an intermediary between your client-side application and the third-party API. By routing requests through your server, you can securely store your API key on the server-side, preventing direct exposure in client-side code. Furthermore, we will explore enhancing our proxy server with features like rate limiting and caching to improve performance and control API usage.

> **Proxy Server**
> A proxy server acts as an intermediary for requests from clients seeking resources from other servers. In the context of APIs, a proxy server can receive requests from a client application, forward them to the target API, and then relay the API's response back to the client. This adds a layer of abstraction and control.

## Setting Up the Server Environment

To begin building our API proxy server, we need to set up our development environment. This involves installing Node.js and initializing a new project.

### Prerequisites

Before proceeding, ensure you have the following installed on your system:

*   **Node.js:**  A JavaScript runtime environment that allows you to run JavaScript code outside of a web browser. Node.js is essential for building our server-side application.

### Initializing the Project

1.  **Create a Project Folder:** Start by creating a new directory for your project. For example, name it `node-api-proxy-server`.
2.  **Navigate to the Project Folder:** Open your terminal or command prompt and navigate into the newly created project directory using the `cd` command (e.g., `cd node-api-proxy-server`).
3.  **Initialize `package.json`:**  Run the command `npm init -y`. This command initializes a new Node.js project and creates a `package.json` file in your project directory.

    > **npm (Node Package Manager)**
    > npm is the default package manager for Node.js. It is used to install, manage, and share JavaScript packages (libraries and tools).

    > **package.json**
    > A `package.json` file is a JSON file that resides in the root directory of a Node.js project. It contains metadata about the project, such as its name, version, dependencies, and scripts.

### Installing Dependencies

We will need several packages to build our API proxy server. Install them using `npm install`:

```bash
npm install express dotenv cors needle nodemon -D
```

This command installs the following packages:

*   **`express`:** A minimalist and flexible Node.js web application framework that provides a robust set of features for building web applications and APIs.
*   **`dotenv`:** A zero-dependency module that loads environment variables from a `.env` file into `process.env`. This is crucial for securely managing API keys and other configuration settings.
*   **`cors`:**  (Cross-Origin Resource Sharing) A Node.js package that enables Cross-Origin Resource Sharing (CORS). CORS is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served. This is often necessary when your client-side application and server are running on different domains or ports.
*   **`needle`:** A lightweight HTTP client for Node.js. We will use `needle` to make requests from our server to the third-party API (OpenWeatherMap in this case).
*   **`nodemon`:** (Installed as a dev dependency using `-D`) A utility that monitors for any changes in your Node.js application and automatically restarts the server. This significantly improves the development workflow by eliminating the need to manually restart the server after each code modification.

    > **Dev Dependency**
    > In `package.json`, dependencies listed under `devDependencies` are packages that are only needed for development and testing, not for the production application itself. `nodemon` is a typical example of a dev dependency.

After running this command, you should see a `node_modules` folder in your project directory containing the installed packages, and your `package.json` file will be updated with the dependencies and devDependencies.

### Setting Up Start Scripts

Open your `package.json` file and locate the `scripts` section. Modify it to include `start` and `dev` scripts:

```json
"scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
},
```

These scripts define commands that you can run using `npm`.

*   `npm start`:  This command will run your server using `node index.js`. This is typically used for running the server in a production environment.
*   `npm run dev`: This command will run your server using `nodemon index.js`. `nodemon` will watch for file changes and automatically restart the server, making development more efficient.

## Creating the API Proxy Server with Express

Now, let's create the core of our API proxy server using Express.

### Setting Up the Express Server ( `index.js` )

Create a file named `index.js` in your project root. This will be our main server file. Add the following code to `index.js`:

```javascript
const express = require('express');
const cors = require('cors');
require('dotenv').config(); // Load environment variables from .env

const app = express();
const port = process.env.PORT || 5000; // Use environment port or default to 5000

// Enable CORS for all routes
app.use(cors());

// Define routes (routes will be handled in a separate file later)
app.use('/api', require('./routes')); // Mount routes from ./routes/index.js under /api path

app.listen(port, () => {
    console.log(`Server running on port ${port}`);
});
```

**Explanation:**

1.  **`require('express')` and `require('cors')`:**  Imports the `express` and `cors` modules.
2.  **`require('dotenv').config()`:** Loads environment variables from a `.env` file (which we will create shortly) into `process.env`.
3.  **`const app = express()`:** Creates an Express application instance.
4.  **`const port = process.env.PORT || 5000;`:**  Defines the port for the server to listen on. It first tries to use the port specified in the `PORT` environment variable (which is often used in deployment environments like Heroku). If the `PORT` environment variable is not set, it defaults to port 5000.
5.  **`app.use(cors());`:** Enables CORS middleware for all routes in the application. This allows your client-side application (potentially running on a different domain) to make requests to this server.
6.  **`app.use('/api', require('./routes'));`:** Mounts the routes defined in `routes/index.js` (which we will create next) under the `/api` path. This means that any request starting with `/api` will be handled by the routes defined in that file.
7.  **`app.listen(port, ...)`:** Starts the Express server and makes it listen for incoming requests on the specified port. The callback function logs a message to the console indicating that the server is running.

### Creating Environment Variables ( `.env` )

Create a file named `.env` in the root of your project directory. This file will store your API keys and other configuration settings as environment variables. Add the following lines to `.env`:

```
API_BASE_URL=https://api.openweathermap.org/data/2.5/weather
API_KEY_NAME=appid
API_KEY_VALUE=YOUR_OPENWEATHERMAP_API_KEY
```

**Replace `YOUR_OPENWEATHERMAP_API_KEY` with your actual OpenWeatherMap API key.** You can obtain an API key by creating a free account on the OpenWeatherMap website ([https://openweathermap.org/](https://openweathermap.org/)).

**Explanation:**

*   **`API_BASE_URL`:**  Stores the base URL for the OpenWeatherMap API. We extract the base URL, excluding query parameters, to make our proxy server more flexible and reusable with other APIs.
*   **`API_KEY_NAME`:**  Specifies the name of the query parameter used for the API key in the OpenWeatherMap API. In this case, it's `appid`.
*   **`API_KEY_VALUE`:** Stores your actual OpenWeatherMap API key. **Crucially, never commit your `.env` file containing sensitive information like API keys to version control (e.g., Git).** We will configure `.gitignore` shortly to prevent this.

### Setting Up Routes ( `routes/index.js` )

Create a folder named `routes` in your project root. Inside the `routes` folder, create a file named `index.js`. This file will handle the routing logic for our API proxy. Add the following code to `routes/index.js`:

```javascript
const express = require('express');
const router = express.Router();
const needle = require('needle');
const url = require('url');

// Environment variables
const API_BASE_URL = process.env.API_BASE_URL;
const API_KEY_NAME = process.env.API_KEY_NAME;
const API_KEY_VALUE = process.env.API_KEY_VALUE;

// Define a route to handle API requests
router.get('/', async (req, res) => {
    try {
        const params = new URLSearchParams({
            [API_KEY_NAME]: API_KEY_VALUE, // Add API key as a query parameter
            ...url.parse(req.url, true).query, // Forward all query parameters from client request
        });

        const apiRes = await needle('get', `${API_BASE_URL}?${params}`); // Make request to OpenWeatherMap API
        const data = apiRes.body;

        // Log the request to the public API in development mode
        if (process.env.NODE_ENV !== 'production') {
            console.log(`Request to public API: ${apiRes.url}`);
        }

        res.status(200).json(data); // Send back the API response to the client

    } catch (error) {
        res.status(500).json({ error }); // Handle errors and send a 500 status code
    }
});

module.exports = router;
```

**Explanation:**

1.  **`require('express')`, `require('needle')`, `require('url')`:** Imports necessary modules.
2.  **`const router = express.Router()`:** Creates an Express Router instance. Routers are used to create modular, mountable route handlers.
3.  **Environment Variables:** Retrieves environment variables defined in `.env` using `process.env`.
4.  **`router.get('/', async (req, res) => { ... })`:** Defines a GET route for the root path (`/`) under the `/api` path (because we mounted this router at `/api` in `index.js`). This route will handle incoming requests to our API proxy.
    *   **`try...catch` block:**  Encloses the asynchronous operation within a `try...catch` block for error handling.
    *   **`const params = new URLSearchParams(...)`:** Creates a `URLSearchParams` object to construct the query parameters for the request to the OpenWeatherMap API.
        *   **`[API_KEY_NAME]: API_KEY_VALUE`:** Adds the API key as a query parameter. The `API_KEY_NAME` (e.g., `appid`) is used as the key, and `API_KEY_VALUE` (your actual API key) is used as the value.
        *   **`...url.parse(req.url, true).query`:**  Parses the query parameters from the incoming request (`req.url`) and spreads them into the `URLSearchParams` object. This ensures that any query parameters sent by the client to our proxy server are forwarded to the OpenWeatherMap API.
    *   **`const apiRes = await needle('get', `${API_BASE_URL}?${params}`);`:** Uses `needle` to make a GET request to the OpenWeatherMap API. The URL is constructed by combining `API_BASE_URL` with the query parameters built in the `params` object. `await` is used because `needle` returns a promise.
    *   **`const data = apiRes.body;`:** Extracts the response body from the API response.
    *   **`if (process.env.NODE_ENV !== 'production') { ... }`:**  Conditionally logs the request URL to the public API in development environments (when `NODE_ENV` is not set to `production`). This is helpful for debugging and understanding the requests being made.
    *   **`res.status(200).json(data);`:** Sends a successful response (HTTP status code 200) back to the client with the data received from the OpenWeatherMap API in JSON format.
    *   **`res.status(500).json({ error });`:** In case of an error during the API request, sends an error response (HTTP status code 500 - Internal Server Error) back to the client with an error object in JSON format.
5.  **`module.exports = router;`:** Exports the `router` so that it can be used in `index.js`.

    > **REST API (Representational State Transfer API)**
    > REST is an architectural style for designing networked applications, particularly web services. REST APIs communicate via standard HTTP methods like GET, POST, PUT, DELETE and are often used for accessing and manipulating data. OpenWeatherMap API is a REST API.

    > **HTTP Client**
    > An HTTP client is a software or library that allows applications to send HTTP requests to servers and receive responses. `needle` and `node-fetch` are examples of HTTP clients in Node.js.

    > **Query Parameters**
    > Query parameters are parts of a URL that come after the question mark `?`. They are used to send additional information to the server, often for filtering, sorting, or specifying data to retrieve. They are key-value pairs, like `?key1=value1&key2=value2`.

    > **URL Search Params (URLSearchParams)**
    > `URLSearchParams` is a built-in JavaScript interface for working with the query string of a URL. It provides methods for easily creating, manipulating, and encoding URL query parameters.

    > **Async/Await**
    > `async` and `await` are keywords in JavaScript that simplify working with asynchronous operations, such as promises. `async` marks a function as asynchronous, and `await` pauses the execution of an `async` function until a promise resolves, making asynchronous code look and behave more like synchronous code.

    > **JSON (JavaScript Object Notation)**
    > JSON is a lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate. It is commonly used for transmitting data in web applications and APIs.

    > **Promises**
    > In JavaScript, a Promise is an object representing the eventual outcome of an asynchronous operation. It can be in one of three states: pending, fulfilled, or rejected. Promises are used to handle asynchronous operations in a more structured way than traditional callbacks.

    > **HTTP Status Codes**
    > HTTP status codes are three-digit codes that servers send back in response to HTTP requests. They indicate the outcome of the request. Common status codes include:
    > *   **200 OK:**  Indicates that the request was successful.
    > *   **401 Unauthorized:** Indicates that the client is not authorized to access the requested resource (often due to missing or invalid credentials).
    > *   **404 Not Found:** Indicates that the server cannot find the requested resource.
    > *   **500 Internal Server Error:** Indicates that the server encountered an unexpected error while processing the request.

    > **Error Handling**
    > Error handling is the process of anticipating, detecting, and resolving errors in a program. In web servers, proper error handling is crucial to gracefully manage unexpected situations, prevent crashes, and provide informative error responses to clients.

### Ignoring Sensitive Files ( `.gitignore` )

Create a file named `.gitignore` in the root of your project directory. This file tells Git which files and directories to ignore when committing changes to version control. Add the following lines to `.gitignore`:

```
node_modules
.env
```

This ensures that the `node_modules` folder (which can be large and is automatically generated) and the `.env` file (containing sensitive API keys) are not committed to your Git repository.

### Testing the Server

1.  **Start the server:** In your terminal, run `npm run dev`. This will start your server using `nodemon`. You should see the message "Server running on port 5000" (or the port you configured).
2.  **Test with Postman or Browser:** You can use Postman or any HTTP client (or even your web browser) to test your API proxy server. Send a GET request to `http://localhost:5000/api?q=London`. Replace `London` with any city you want to test.

    You should receive a JSON response containing weather data for the specified city from the OpenWeatherMap API. If you check your server console, you should also see a log message indicating the request made to the public OpenWeatherMap API (if `NODE_ENV` is not set to `production`).

If you receive the weather data successfully, your API proxy server is working correctly! You have successfully created a server that forwards requests to the OpenWeatherMap API, securely adding your API key on the server-side.

## Enhancing the Proxy Server: Rate Limiting and Caching

To further improve our API proxy server, we will implement rate limiting and caching.

### Rate Limiting

Rate limiting is a technique to control the number of requests a user or client can make to an API within a given time period. This helps prevent abuse, protect your server from overload, and manage API usage. We will use the `express-rate-limit` package for this.

1.  **Install `express-rate-limit`:** If you haven't already, ensure `express-rate-limit` is installed (`npm install express-rate-limit`).
2.  **Implement Rate Limiting in `index.js`:** Modify your `index.js` file to include rate limiting middleware:

    ```javascript
    const express = require('express');
    const cors = require('cors');
    const rateLimit = require('express-rate-limit'); // Import rate limiter
    require('dotenv').config();

    const app = express();
    const port = process.env.PORT || 5000;

    // Rate limiting configuration
    const limiter = rateLimit({
        windowMs: 10 * 60 * 1000, // 10 minutes window
        max: 100, // Max 100 requests per 10 minutes per IP
        message: 'Too many requests, please try again later.',
    });

    // Apply rate limiting middleware to all routes
    app.use(limiter);
    app.set('trust proxy', 1); // Trust first proxy (for Heroku, etc.)

    app.use(cors());
    app.use('/api', require('./routes'));

    app.listen(port, () => {
        console.log(`Server running on port ${port}`);
    });
    ```

**Explanation of Rate Limiting Changes:**

*   **`const rateLimit = require('express-rate-limit');`:** Imports the `express-rate-limit` module.
*   **`const limiter = rateLimit({ ... });`:** Configures the rate limiter middleware.
    *   **`windowMs: 10 * 60 * 1000`:** Sets the time window for rate limiting to 10 minutes (in milliseconds).
    *   **`max: 100`:**  Sets the maximum number of requests allowed within the `windowMs` to 100 per IP address.
    *   **`message: 'Too many requests, please try again later.'`:**  Sets the message to be sent back to the client when the rate limit is exceeded.
*   **`app.use(limiter);`:** Applies the `limiter` middleware to *all* routes in the application. This means that rate limiting will be enforced for every request to your server.
*   **`app.set('trust proxy', 1);`:**  If your server is behind a proxy (like Heroku's load balancer), you need to set `trust proxy` to `1` to make rate limiting work correctly based on the client's actual IP address.

    > **Middleware**
    > In Express.js, middleware are functions that have access to the request object (`req`), the response object (`res`), and the next middleware function in the application's request-response cycle. Middleware functions can perform various tasks, such as logging, authentication, request parsing, and in our case, rate limiting. `app.use()` is used to apply middleware to the application.

**Testing Rate Limiting:**

Restart your server (`npm run dev`). Now, try sending requests to `http://localhost:5000/api?q=London` repeatedly in quick succession. After sending more than 100 requests within 10 minutes, you should start receiving the "Too many requests, please try again later." message with an HTTP status code of 429 (Too Many Requests).  You can observe the rate limit headers in the response, like `X-RateLimit-Limit`, `X-RateLimit-Remaining`, and `Retry-After`, which provide information about the rate limit status.

    > **429 Too Many Requests**
    > The HTTP status code 429 Too Many Requests is returned by a server when the user has sent too many requests in a given amount of time ("rate limiting"). It indicates that the user should reduce the rate of requests and try again later, often after waiting for a specified duration provided in the `Retry-After` header.

### Caching

Caching is a technique to store frequently accessed data in a temporary storage location (cache) so that future requests for the same data can be served faster. This reduces latency, improves performance, and reduces load on the upstream API. We will use the `apicache` package for caching API responses.

1.  **Install `apicache`:** If you haven't already, ensure `apicache` is installed (`npm install apicache`).
2.  **Implement Caching in `routes/index.js`:** Modify your `routes/index.js` file to include caching middleware:

    ```javascript
    const express = require('express');
    const router = express.Router();
    const needle = require('needle');
    const url = require('url');
    const apicache = require('apicache'); // Import apicache

    // Initialize cache
    let cache = apicache.middleware;

    // Environment variables (same as before)
    const API_BASE_URL = process.env.API_BASE_URL;
    const API_KEY_NAME = process.env.API_KEY_NAME;
    const API_KEY_VALUE = process.env.API_KEY_VALUE;

    // Define a route to handle API requests with caching
    router.get('/', cache('2 minutes'), async (req, res) => { // Apply caching middleware for 2 minutes
        try {
            const params = new URLSearchParams({
                [API_KEY_NAME]: API_KEY_VALUE,
                ...url.parse(req.url, true).query,
            });

            const apiRes = await needle('get', `${API_BASE_URL}?${params}`);
            const data = apiRes.body;

            if (process.env.NODE_ENV !== 'production') {
                console.log(`Request to public API: ${apiRes.url}`);
            }

            res.status(200).json(data);

        } catch (error) {
            res.status(500).json({ error });
        }
    });

    module.exports = router;
    ```

**Explanation of Caching Changes:**

*   **`const apicache = require('apicache');`:** Imports the `apicache` module.
*   **`let cache = apicache.middleware;`:** Initializes the `apicache` middleware.
*   **`router.get('/', cache('2 minutes'), async (req, res) => { ... })`:** Applies the `cache('2 minutes')` middleware as the second argument to the `router.get()` route handler. This configures `apicache` to cache the response for this route for 2 minutes. You can adjust the cache duration as needed (e.g., '5 minutes', '1 hour', '1 day').

**Testing Caching:**

Restart your server (`npm run dev`). Send a request to `http://localhost:5000/api?q=London`. The first request will fetch data from the OpenWeatherMap API and store it in the cache. Subsequent requests for the same city (within the 2-minute cache duration) will be served directly from the cache, without hitting the OpenWeatherMap API again. You can observe the `Cache-Control` header in the response, which will indicate the cache duration (e.g., `max-age=120` for 2 minutes in seconds).  After 2 minutes, the cache will expire, and the next request will again fetch fresh data from the OpenWeatherMap API and refresh the cache.

## Integrating with the Client-Side Application

To utilize our API proxy server in a client-side application, you need to update the application to make requests to your server's endpoint instead of directly to the OpenWeatherMap API.

Assuming you have a basic client-side JavaScript application (as mentioned in the transcript), you would typically have code similar to this (before using the proxy):

```javascript
async function fetchWeather(city) {
    const apiKey = 'YOUR_OPENWEATHERMAP_API_KEY'; // API key directly in client-side code (BAD PRACTICE!)
    const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

    try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        // ... process weather data
    } catch (error) {
        console.error('Error fetching weather:', error);
    }
}
```

**Modify your client-side JavaScript code as follows to use the API proxy:**

```javascript
async function fetchWeather(city) {
    const proxyApiUrl = `/api?q=${city}&units=metric`; // Request to your proxy server's endpoint (/api)

    try {
        const response = await fetch(proxyApiUrl);
        const data = await response.json();
        // ... process weather data
    } catch (error) {
        console.error('Error fetching weather:', error);
    }
}
```

**Key Changes in Client-Side Code:**

*   **Remove API Key from Client-Side:**  The `apiKey` variable and its value are removed from the client-side JavaScript code.
*   **Update API URL:** The `apiUrl` is changed to `/api?q=${city}&units=metric`. Now, the request is made to the `/api` endpoint of your own server (assuming your client-side application and server are served from the same domain or you have configured CORS appropriately). The query parameters (`q` for city and `units=metric`) are still included in the request to your proxy server, which will forward them to the OpenWeatherMap API.

**Serving Static Files (Client-Side Application):**

To serve your client-side application (HTML, CSS, JavaScript files) using your Express server, you can configure Express to serve static files from a designated directory (e.g., a `public` folder). Add the following to your `index.js` file, typically before defining routes:

```javascript
const express = require('express');
// ... other requires

const app = express();
// ... other configurations

// Set static folder to serve client-side application
app.use(express.static('public')); // Assuming your client-side files are in a 'public' folder

// ... rate limiting, cors, routes, etc.
```

Create a folder named `public` in your project root and place your `index.html`, `styles.css`, `main.js` (and any other client-side files) inside it. Now, when you run your server and access `http://localhost:5000` in your browser, Express will serve your `index.html` file from the `public` folder.

    > **Static Folder**
    > In web servers, a static folder is a directory that contains static files, such as HTML files, CSS stylesheets, JavaScript files, images, and other assets that are served directly to the client without any server-side processing. `express.static()` middleware in Express.js is used to serve files from a specified static folder.

## Deployment to Heroku

Heroku is a popular Platform as a Service (PaaS) that makes it easy to deploy and run web applications. Here's a guide to deploy your API proxy server to Heroku:

### Prerequisites for Heroku Deployment

1.  **Heroku Account:** Create a free Heroku account at [https://www.heroku.com/](https://www.heroku.com/).
2.  **Heroku CLI:** Install the Heroku Command Line Interface (CLI) on your local machine. Instructions for installation can be found on the Heroku website.
3.  **Git:** Ensure Git is installed on your system, as Heroku uses Git for deployment.

### Deployment Steps

1.  **Login to Heroku CLI:** Open your terminal and run `heroku login`. This will open a browser window where you can log in to your Heroku account.
2.  **Create a Heroku Application:** In your terminal, navigate to your project directory and run `heroku create <your-app-name>` (replace `<your-app-name>` with a unique name for your application, or just run `heroku create` to let Heroku generate a name). This command creates a new Heroku application and associates it with your local Git repository.
3.  **Initialize Git Repository (if not already done):** If you haven't already, initialize a Git repository in your project directory by running `git init`.
4.  **Add and Commit Changes:** Add all your project files to the Git repository and commit them:
    ```bash
    git add .
    git commit -m "Initial commit"
    ```
5.  **Push to Heroku:** Deploy your application to Heroku by pushing your Git repository to the Heroku remote:
    ```bash
    git push heroku master
    ```
    Heroku will detect your Node.js application, install dependencies, and start your server.
6.  **Set Environment Variables on Heroku:**  You need to set your environment variables ( `API_BASE_URL`, `API_KEY_NAME`, `API_KEY_VALUE` ) on Heroku. You can do this through the Heroku dashboard:
    *   Go to your Heroku application dashboard in your browser.
    *   Navigate to the "Settings" tab.
    *   Click on "Reveal Config Vars".
    *   Add the environment variables and their values, just like you defined them in your `.env` file locally.

7.  **Open the Deployed Application:** Once the deployment is complete, you can open your deployed application in your browser by running `heroku open` in your terminal or by clicking "Open app" on your Heroku application dashboard.

Your API proxy server should now be live and accessible on the Heroku-provided URL. You can test it by accessing your client-side application (if you deployed it as static files) or by sending requests to the Heroku application URL with appropriate query parameters.

    > **Git**
    > Git is a distributed version control system that tracks changes in computer files and coordinates work on those files among multiple people. It is widely used for source code management in software development.

    > **CLI (Command Line Interface)**
    > A command-line interface (CLI) is a text-based interface used to interact with a computer system or application by typing commands. The Heroku CLI allows developers to manage Heroku applications from the terminal.

    > **Environment Variables (in Deployment)**
    > In deployment environments like Heroku, environment variables are used to configure applications without hardcoding sensitive information or configuration settings directly into the code. They are set outside of the application code and accessed by the application at runtime. This is essential for security and configuration management in production.

## Conclusion

Congratulations! You have successfully built a Node.js API proxy server that securely hides your API key, implements rate limiting, and utilizes caching. This setup not only enhances the security of your client-side applications by preventing API key exposure but also improves performance and manages API usage effectively.

By understanding the principles and techniques outlined in this chapter, you can apply them to proxy and secure various third-party APIs in your web development projects, creating more robust and secure applications. You can further extend this proxy server with additional features like request logging, data transformation, and authentication to meet specific application requirements.
