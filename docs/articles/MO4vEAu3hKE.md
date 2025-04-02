---
layout: "../../layouts/BlogPost.astro"
title: "Building a Website Accessibility Tester: A Practical Guide"
pubDate: "2025-03-08 15:48:19.598755"
youtubeVideoID: "MO4vEAu3hKE"
---

# Building a Website Accessibility Tester: A Practical Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/MO4vEAu3hKE" frameborder="0" allowfullscreen></iframe>

## Introduction to Website Accessibility and Automated Testing

In today's digital world, ensuring websites are accessible to everyone, including individuals with disabilities, is paramount. Website accessibility refers to the practice of designing and developing websites that can be used by people with a wide range of abilities and disabilities. This includes addressing issues that might hinder users with visual, auditory, motor, cognitive, or neurological impairments.

This chapter guides you through the process of building a simple yet effective website accessibility testing tool. We will leverage the power of **Pa11y**, an automated accessibility testing tool, along with **Node.js** to create an application that can analyze any website URL and report accessibility issues. This project will involve building both a backend **API** and a frontend user interface, providing a hands-on approach to understanding and implementing accessibility testing.

> **API (Application Programming Interface):** A set of rules and specifications that software programs can follow to communicate with each other. APIs allow developers to build applications that can interact with other systems or services in a standardized way.

We will construct a backend using Node.js and **Express.js**, a popular framework for building web applications. The frontend will be developed using fundamental web technologies – **HTML**, **CSS**, and **vanilla JavaScript**, enhanced with **Bootstrap** for styling and layout. This approach ensures the project is accessible to learners with varying levels of framework experience.

> **Node.js:**  A JavaScript runtime environment that allows you to execute JavaScript code server-side. It's commonly used for building backend services and web applications.

> **Express.js:** A minimal and flexible Node.js web application framework that provides a robust set of features for building single-page, multi-page, and hybrid web applications.

> **HTML (HyperText Markup Language):** The standard markup language for creating web pages. It provides the structure and content of a webpage.

> **CSS (Cascading Style Sheets):** A style sheet language used for describing the presentation of a document written in HTML or XML (including XML dialects such as SVG, MathML or XHTML). CSS describes how elements should be rendered on screen, on paper, in speech, or on other media.

> **Vanilla JavaScript:** Refers to using plain JavaScript without relying on any external libraries or frameworks. It emphasizes understanding the core JavaScript language.

> **Bootstrap:** A free and open-source CSS framework directed at responsive, mobile-first front-end web development. It contains CSS- and (optionally) JavaScript-based design templates for typography, forms, buttons, navigation, and other interface components.

## Setting Up the Backend API with Node.js and Pa11y

Our first step is to create the backend API, which will be responsible for using Pa11y to test websites and return the accessibility results.

### Project Initialization and Dependency Installation

1.  **Create a Project Folder:** Begin by creating a new folder for your project, for example, "website-accessibility-tester."
2.  **Initialize Node.js Project:** Navigate into your project folder in the terminal and run the command `npm init -y`. This command initializes a new Node.js project and creates a `package.json` file with default settings.

    > **npm (Node Package Manager):** The package manager for Node.js. It is used to install, manage, and share JavaScript packages and libraries.

    > **package.json:** A JSON file that acts as a manifest for your Node.js project. It contains metadata about the project, including dependencies, scripts, and project name.
3.  **Install Dependencies:**  We need to install two primary packages: `express` for creating the API and `pa11y` for accessibility testing. Run the following command in your terminal: `npm install express pa11y`. This will download and install these packages and add them to your `package.json` file as dependencies.

### Creating the Backend Logic in `index.js`

1.  **Create `index.js`:** Create a file named `index.js` in your project root. This file will contain the code for our backend server.
2.  **Import Modules and Configure Port:**  Start by importing the necessary modules (`express` and `pa11y`) and setting up the port for the server.

    ```javascript
    const express = require('express');
    const pa11y = require('pa11y');

    const app = express();
    const port = process.env.PORT || 5000;
    ```

    Here, we are setting the port to either the environment variable `PORT` (useful for deployment) or defaulting to port 5000 for local development.
3.  **Test Pa11y (Optional):** Before building the API route, you can test Pa11y directly to understand how it works. Add the following code to your `index.js` file and run it using `node index.js`.

    ```javascript
    async function runTest() {
        const response = await pa11y('https://www.traversing.dev');
        console.log(response);
    }

    runTest();
    ```

    This code snippet demonstrates how to use Pa11y. It takes a URL as input and returns a promise that resolves with an object containing accessibility issues. The output, logged to the console, will show details about any accessibility violations found on the provided URL.
4.  **Set up the Express Server and API Route:** Replace the test Pa11y code with the following to create an Express server and define an API endpoint to handle accessibility testing requests.

    ```javascript
    app.use(express.static('public')); // Middleware for serving static files

    app.get('/api/test', async (req, res) => {
        const url = req.query.url;

        if (!url) {
            return res.status(400).json({ error: 'URL is required' });
        }

        try {
            const results = await pa11y(url);
            res.status(200).json(results);
        } catch (error) {
            res.status(500).json({ error: 'Error running accessibility test' });
        }
    });

    app.listen(port, () => console.log(`Server started on port ${port}`));
    ```

    > **Middleware:** Functions that have access to the request object (req), the response object (res), and the next middleware function in the application’s request-response cycle. Middleware functions can perform tasks such as parsing request bodies, adding headers, or serving static files.

    > **Query Parameter:**  A part of a URL that assigns values to specified parameters. They appear after a question mark (?) at the end of the URL. For example, in `http://example.com/api/data?param1=value1&param2=value2`, `param1` and `param2` are query parameters.

    In this code:
    *   `app.use(express.static('public'));` serves static files from a folder named `public` (which we will create for our frontend).
    *   `app.get('/api/test', ...)` defines a **GET** route at `/api/test`.
    *   `req.query.url` retrieves the URL from the query parameters of the request.
    *   Error handling is implemented:
        *   If the `url` parameter is missing, a 400 (Bad Request) status is returned.
        *   If there's an error during the Pa11y test, a 500 (Internal Server Error) status is returned.
        *   On successful execution, Pa11y results are returned as JSON with a 200 (OK) status.
5.  **Add Start Script to `package.json`:**  Modify the `scripts` section in your `package.json` to include a `start` script for easily running your server.

    ```json
    "scripts": {
      "start": "node index.js"
    }
    ```

    Now you can start your backend server by running `npm start` in your terminal.
6.  **Test the API using Postman (or similar tool):** You can use a tool like **Postman** to test your API endpoint. Send a GET request to `http://localhost:5000/api/test?url=https://www.traversing.dev`. You should receive a JSON response containing the accessibility issues reported by Pa11y.

    > **Postman:** A popular API client that makes it easy for developers to test, develop, and document APIs. It provides a graphical user interface to send HTTP requests and view responses.

## Building the Frontend with HTML, CSS, and Vanilla JavaScript

With the backend API in place, we now focus on building the frontend to interact with the API and display the accessibility test results in a user-friendly manner.

### Frontend Structure in `public/index.html`

1.  **Create `public` Folder:** In your project root, create a new folder named `public`. This folder will house all our frontend files.
2.  **Create `index.html`:** Inside the `public` folder, create a file named `index.html`. This will be the main HTML file for our frontend.
3.  **Basic HTML Structure with Bootstrap:** Add the basic HTML structure, including Bootstrap CSS for styling and a link to your `main.js` JavaScript file.

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Website Accessibility Tester</title>
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
        <style>
            .loader {
                display: none;
            }
        </style>
    </head>
    <body>
        <div class="container container-sm">
            <div class="card my-5 p-3 bg-dark text-light">
                <div class="card-body">
                    <h2 class="mb-3">Website Accessibility Tester</h2>
                    <form id="form">
                        <div class="input-group mb-3">
                            <input type="url" class="form-control form-control" id="url" placeholder="Enter a website">
                            <div class="input-group-append">
                                <button class="btn btn-primary" type="submit">Submit</button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
            <div class="loader text-center" id="loader">
                <div class="spinner-border" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
            </div>
            <div id="issues"></div>
        </div>

        <script src="./js/main.js"></script>
    </body>
    </html>
    ```

    This HTML sets up:
    *   Bootstrap CSS from a **CDN (Content Delivery Network)** for styling.
    *   A basic form to input a URL.
    *   A loading spinner (initially hidden using CSS).
    *   A `div` with the ID `issues` where accessibility results will be displayed.

    > **CDN (Content Delivery Network):** A geographically distributed network of servers that caches static content (like CSS, JavaScript files, images) and delivers it to users based on their geographic location. Using CDNs can improve website loading speed and performance.
4.  **Create `public/js/main.js`:** Inside the `public` folder, create a new folder named `js`, and within it, create a file named `main.js`. This file will contain our frontend JavaScript logic.

### Frontend JavaScript Logic in `public/js/main.js`

1.  **Basic Structure and Event Listener:** Add the basic JavaScript structure to handle form submission and fetch accessibility issues.

    ```javascript
    document.addEventListener('DOMContentLoaded', () => {
        const form = document.querySelector('#form');
        const urlInput = document.querySelector('#url');
        const issuesOutput = document.querySelector('#issues');
        const loader = document.querySelector('#loader');

        form.addEventListener('submit', testAccessibility);

        async function testAccessibility(e) {
            e.preventDefault();
            const url = urlInput.value.trim();

            if (!url) {
                alert('Please add a URL');
                return;
            }

            setLoading(true); // Show loader
            issuesOutput.innerHTML = ''; // Clear previous issues

            try {
                const response = await fetch(`/api/test?url=${url}`);
                if (!response.ok) {
                    setLoading(false); // Hide loader
                    alert('Something went wrong');
                    return;
                }
                const data = await response.json();
                const issues = data.issues;
                addIssuesToDOM(issues);
            } catch (error) {
                setLoading(false); // Hide loader
                alert('Error fetching data');
            } finally {
                setLoading(false); // Ensure loader is hidden even if errors occur
            }
        }

        function setLoading(isLoading) {
            loader.style.display = isLoading ? 'block' : 'none';
        }

        function addIssuesToDOM(issues) {
            if (issues.length === 0) {
                issuesOutput.innerHTML = '<h4 class="text-center">No issues found!</h4>';
            } else {
                let output = '';
                issues.forEach(issue => {
                    output += `
                        <div class="card mb-5">
                            <div class="card-body">
                                <h4>${issue.message}</h4>
                                <p class="bg-light p-3 my-3">${escapeHTML(issue.context)}</p>
                                <p class="bg-secondary text-light p-2">Code: ${issue.code}</p>
                            </div>
                        </div>
                    `;
                });
                issuesOutput.innerHTML = output;
            }
        }

        function escapeHTML(html) {
            return html.replace(/&/g, "&amp;")
                       .replace(/</g, "&lt;")
                       .replace(/>/g, "&gt;")
                       .replace(/"/g, "&quot;")
                       .replace(/'/g, "&#039;");
        }
    });
    ```

    In this code:
    *   `document.addEventListener('DOMContentLoaded', ...)` ensures the script runs after the **DOM (Document Object Model)** is fully loaded.

        > **DOM (Document Object Model):** A programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as nodes and objects.

    *   Event listeners are added for form submission.
    *   `fetch('/api/test?url=${url}')` uses the **Fetch API** to make a request to our backend API.

        > **Fetch API:** A modern JavaScript interface for making network requests. It provides a more powerful and flexible alternative to XMLHttpRequest.

    *   `setLoading(true)` and `setLoading(false)` functions control the visibility of the loading spinner.
    *   `addIssuesToDOM(issues)` function dynamically creates HTML to display each accessibility issue.
    *   `escapeHTML(html)` function prevents HTML characters in the context from being rendered as actual HTML, ensuring they are displayed as text.

## Testing and Refinement

1.  **Run the Application:** Ensure your backend server is running (`npm start`). Open your web browser and navigate to `http://localhost:5000`. You should see the frontend interface.
2.  **Test with a Website URL:** Enter a website URL in the input field and click "Submit." The loading spinner should appear, and after a moment, the accessibility issues (if any) will be displayed below.
3.  **Address Accessibility Issues:** Use the output from the tool to identify and address accessibility issues on your websites. Pay attention to the messages, context, and codes provided for each issue.
4.  **Refine and Enhance:** Consider further enhancements to the tool, such as:
    *   Adding more detailed explanations for each accessibility issue code.
    *   Implementing different report formats (e.g., JSON, CSV).
    *   Allowing users to configure Pa11y options.
    *   Improving the frontend UI/UX with better styling and error handling.

## Conclusion

This chapter has provided a comprehensive guide to building a website accessibility tester using Pa11y, Node.js, and vanilla JavaScript. By following these steps, you can create a practical tool to automate accessibility testing and gain valuable insights into making websites more inclusive. This project serves as a strong foundation for further exploration into web accessibility and automated testing methodologies. Remember that automated tools are just one part of ensuring accessibility; manual testing and user feedback are also crucial components of a holistic accessibility strategy.
