---
layout: "../../layouts/BlogPost.astro"
title: "Encore: A Comprehensive Backend Development Platform - An Educational Overview"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "tL01EzN2-xA"
channel: "Traversy Media"
index: 5
---

# Encore: A Comprehensive Backend Development Platform - An Educational Overview

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/tL01EzN2-xA" frameborder="0" allowfullscreen></iframe>

## Introduction to Encore

In today's fast-paced digital world, efficient backend development is crucial for building robust and scalable applications.  This chapter introduces Encore, a novel backend development platform designed to streamline the entire development lifecycle, from local setup and testing to cloud deployment and operations.  Encore aims to abstract away much of the complexity traditionally associated with backend infrastructure and DevOps, allowing developers to focus primarily on writing application logic.

### What is Encore?

Encore is described as more than just a **backend framework**. It is a comprehensive **development platform** that offers a complete toolset tailored for backend development.

> **Backend framework:** A software framework designed to simplify the development of the server-side components of web applications, APIs, and mobile backends. These frameworks typically provide tools and libraries for handling routing, database interactions, and other server-side functionalities.
>
> **Development platform:** A suite of tools and services designed to support the complete software development lifecycle. This can include tools for coding, testing, debugging, deployment, and management of applications.

Encore distinguishes itself by handling everything from local development and testing environments to cloud infrastructure management and **DevOps**.

> **DevOps:** A set of practices that combines software development (Dev) and IT operations (Ops). It aims to shorten the systems development life cycle and provide continuous delivery with high software quality.

A key aspect of Encore is its use of **infrastructure as code**.

> **Infrastructure as code (IaC):**  The practice of managing and provisioning computer data centers through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. This approach allows for automation and version control of infrastructure.

This approach significantly reduces the amount of manual configuration and **boilerplate** code typically required for cloud infrastructure setup.

> **Boilerplate code:** Sections of code that are repeated in many contexts with little to no alteration. It is often used to set up basic functionalities or configurations.

### Core Features of Encore

Encore boasts a range of features designed to enhance developer productivity and application performance:

*   **Simplified Infrastructure:** With a single line of code, developers can spin up a **Docker container** containing a fully functional **Postgres database**.

    > **Docker container:** A standardized unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.
    >
    > **Postgres database:** An open-source relational database management system (RDBMS) known for its reliability, feature robustness, and extensibility.

*   **One-Command Deployment:** Deploying APIs or services to the cloud is achieved with a single command, further simplifying the **API** lifecycle management.

    > **API (Application Programming Interface):** A set of definitions and protocols used for building and integrating application software. APIs allow different software components to communicate and exchange data.

*   **Built-in Type Validation:** Encore incorporates inherent **type validation** to ensure data integrity and security.

    > **Type validation:** The process of verifying that data conforms to a defined data type, ensuring that the data being processed is of the expected format and structure.

*   **High-Performance Runtime:**  It leverages a **Rust multi-threaded runtime** for optimized performance and efficiency.

    > **Rust multi-threaded runtime:** A runtime environment written in the Rust programming language that supports concurrent execution of multiple threads. Rust is known for its performance, reliability, and safety features, making it suitable for building high-performance systems.

*   **Integrated Developer Dashboard:**  Encore provides a built-in **developer dashboard**, offering a visual interface for managing and monitoring applications.

    > **Developer dashboard:** A web-based user interface that provides developers with a centralized view of their projects, services, logs, and other relevant information, facilitating monitoring and management.

*   **Performance Advantages:** Encore is presented as being faster than **Express** and most other **JavaScript-based backend frameworks**.

    > **Express:** A minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.
    >
    > **JavaScript-based backend frameworks:** Backend frameworks built using the JavaScript programming language, commonly used with Node.js for server-side development.

## Encore TS and Encore Go

### Two Flavors of Encore

Encore offers two primary flavors to cater to different developer preferences and project requirements:

*   **Encore TS:** A **TypeScript** backend framework. TypeScript, being a superset of JavaScript, adds static typing, which enhances code maintainability and reduces runtime errors. This is the version primarily discussed and used in the context of the original transcript.

    > **TypeScript:** A strongly typed programming language that builds on JavaScript, giving you better tooling at any scale. TypeScript is often preferred for large projects due to its enhanced code organization and error detection capabilities.

*   **Encore Go:** A **Go** backend framework. Go is a statically typed, compiled programming language designed at Google. It is known for its efficiency, concurrency features, and suitability for building scalable and high-performance applications.

    > **Go:**  Also known as Golang, is a statically typed, compiled programming language designed at Google. It is known for its simplicity, efficiency, and built-in concurrency, making it well-suited for backend development and system programming.

Both Encore TS and Encore Go are designed to build robust and type-safe applications, sharing largely the same feature set, differing mainly in the underlying programming language.

### Performance Benchmarks

Encore emphasizes performance as a key differentiator. While acknowledging that performance can vary based on specific project needs, Encore provides benchmark data indicating significant speed advantages compared to other popular frameworks. According to their benchmarks, Encore outperforms:

*   **Express:**  Claiming to be up to nine times faster.
*   **Fastify:**  Reportedly twice as fast as Fastify.

    > **Fastify:** A web framework highly focused on providing the best developer experience with a focus on speed and low overhead.

*   **Bun JS:**  Even surpassing the performance of Bun JS, a relatively new JavaScript runtime environment known for its speed.

    > **Bun JS:** A fast, all-in-one JavaScript runtime, bundler, transpiler, and package manager, designed to be a drop-in replacement for Node.js.

This performance boost is attributed, in part, to Encore's Rust runtime, which is explored further in subsequent sections.

## Key Features of Encore

### Built-in Type Validation

Encore's type validation system is a core feature designed for both developer convenience and application security. It operates in a **declarative** manner.

> **Declarative:** A programming paradigm that expresses the logic of a computation without describing its control flow. In the context of type validation, it means defining the expected data types and structures in a way that the system automatically enforces them.

This declarative approach enables Encore to automatically parse and validate incoming requests, ensuring they conform to the defined schema. This automated validation happens before the request even reaches the application's JavaScript code layer, providing a robust layer of protection against attacks and data inconsistencies. This proactive validation removes the need for manual validation boilerplate, streamlining development and enhancing security.

### Infrastructure as Code: Simplified DevOps

One of the most compelling aspects of Encore is its **infrastructure as code** approach, which significantly simplifies **DevOps** tasks.  For developers accustomed to the complexities of deploying applications to cloud platforms like AWS using frameworks like Express, Encore offers a streamlined alternative.

Traditionally, deploying an Express application often involves intricate configurations and substantial boilerplate to set up cloud infrastructure. Encore is specifically architected for building **cloud-native applications**, abstracting away much of this infrastructure complexity.

> **Cloud-native applications:** Applications designed and built to take full advantage of cloud computing architectures. They are typically composed of microservices, packaged in containers, and dynamically orchestrated to optimize scalability, resilience, and agility.

This abstraction allows developers to concentrate more on core business logic rather than getting bogged down in infrastructure details.  Encore simplifies common infrastructure tasks:

*   **Databases:** Creating a Postgres database is reduced to a single line of code.
*   **Messaging:** Setting up **publish-subscribe topics** for asynchronous communication is similarly straightforward.

    > **Publish-subscribe topics:** A messaging pattern where publishers send messages to a topic, and subscribers who are interested in that topic receive the messages. This enables decoupled communication between different parts of an application.

*   **Scheduled Tasks:** Defining **cron jobs** for scheduled tasks becomes simple and declarative.

    > **Cron jobs:** Scheduled tasks that run automatically at specified intervals. They are commonly used for automating routine operations, such as backups, maintenance, or sending periodic reports.

*   **Future Integrations:**  Encore plans to integrate with services like **Redis** for caching and data management in the near future.

    > **Redis:** An open-source, in-memory data structure store, used as a database, cache, and message broker. It is known for its high performance and versatility.

Encore achieves this simplification in local development environments by leveraging **Docker**.  By running a **migration file**, Encore automatically sets up a Docker container with the necessary database and other specified infrastructure components.

> **Migration file:** A script that defines changes to a database schema. Migration files are used to track and apply database schema updates in a controlled and versioned manner.

Developers only need to have Docker installed; Encore handles the creation and management of containers automatically.  Deployment to the cloud is equally streamlined, accomplished with a single command, further emphasizing Encore's commitment to simplifying the DevOps workflow.

## Core Components

### High-Performance Rust Runtime

Encore's architecture comprises two key parts:

1.  **TypeScript/Go SDK:**  A Software Development Kit (**SDK**) in either TypeScript or Go, used for building backend services and APIs.

    > **SDK (Software Development Kit):** A set of software development tools that allows the creation of applications for a certain software package, software framework, hardware platform, computer system, video game console, operating system, or similar development platform.

2.  **High-Performance Rust Runtime:** A multi-threaded runtime environment written in Rust. This runtime is crucial for Encore's performance advantages.

This Rust runtime is designed to integrate seamlessly with the **Node.js runtime** for executing JavaScript code, ensuring 100% compatibility with the **Node.js ecosystem**.

> **Node.js runtime:** A JavaScript runtime environment that executes JavaScript code server-side. Node.js is built on Chrome's V8 JavaScript engine and is popular for building scalable network applications.
>
> **Node.js ecosystem:** The collection of libraries, frameworks, tools, and community resources available for Node.js development. It is known for its vast and active community support.

The use of Rust provides a significant performance boost compared to the traditional Node.js runtime. Benchmarks indicate:

*   **Throughput Increase:** Throughput is increased by up to seven times.
*   **Latency Reduction:** Response latency is reduced by as much as 85%.

Furthermore, Encore boasts zero **npm dependencies**, which also contributes to improved performance and enhanced security.

> **npm dependencies:** External libraries or packages that a Node.js project relies on, managed by npm (Node Package Manager). Reducing dependencies can improve performance and security by minimizing the codebase and potential vulnerabilities.

**How it works:**

1.  **Initialization:** Node.js initializes the Rust runtime.
2.  **Request Handling:** The Rust runtime listens for incoming requests, parsing and validating them against the **API schema**.

    > **API schema:** A formal specification that defines the structure and constraints of an API, including the data types, request formats, and response formats.

3.  **Code Execution:** Valid requests are passed to the application code running in Node.js.
4.  **Resource Management:** When the application interacts with infrastructure resources (e.g., database queries), these operations are offloaded to the Rust runtime for faster execution.

This architecture allows the single-threaded **Node.js event loop** to focus on executing business logic, while resource-intensive tasks are handled concurrently by Encore's multi-threaded Rust runtime.

> **Node.js event loop:** A single-threaded loop in Node.js that handles asynchronous operations. It allows Node.js to perform non-blocking I/O operations efficiently.

### Developer Dashboard

Encore provides a built-in **developer dashboard**, a web-based tool accessible on a separate port. This dashboard offers a visual interface for interacting with and managing APIs and services. Key features include:

*   **Built-in Request Client:**  Enables making API requests directly from the dashboard, eliminating the need for external tools like **Postman**.

    > **Postman:** A popular API client used for testing, developing, and documenting APIs by sending HTTP requests and viewing responses.

*   **Tracing and Logging:** Provides comprehensive **tracing** and **logging** capabilities for monitoring application behavior and debugging issues.

    > **Tracing:** A method of monitoring and visualizing the flow of requests and operations through a distributed system, helping to understand performance bottlenecks and dependencies.
    >
    > **Logging:** The process of recording events and information about an application's execution, used for monitoring, debugging, and auditing.

*   **Service Visualization:** Visual representation of **publish-subscribe** flows, providing insights into message flows within the application.
*   **Code Snippets:** Access to code snippets for common tasks, such as database schema creation.
*   **Documentation:**  Integrated documentation for easy reference.
*   **AI Lab:** An experimental feature for exploring AI-powered development assistance.

The developer dashboard serves as a central hub for development, testing, and monitoring, significantly enhancing the developer experience.

## Getting Started with Encore

### Encore Cloud Account

To fully leverage Encore's capabilities, creating an Encore **cloud account** is recommended.

> **Cloud account:** An account with a cloud service provider that grants access to cloud computing resources and services. In the context of Encore, it provides access to Encore's cloud platform for deployment and management.

Upon installing Encore and creating a new project, users are prompted to create a cloud account. This account is essential for utilizing Encore's built-in infrastructure and one-command deployment features. The account setup process typically involves a simple registration, potentially redirecting users to a browser to complete the process.

### Installation

Encore provides straightforward installation instructions for various operating systems:

*   **macOS:**  Installation is simplified using **Homebrew**, a popular package manager for macOS. If Homebrew is not installed, users are directed to **brew.sh** to obtain the installation command.

    > **Homebrew:** A free and open-source software package management system that simplifies the installation of software on macOS and Linux.
    >
    > **brew.sh:** The official website for Homebrew, providing installation instructions and documentation.

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    brew install encore
    ```

*   **Windows:**  Installation on Windows is facilitated via a **PowerShell** command.

    > **PowerShell:** A task automation and configuration management framework from Microsoft, consisting of a command-line shell and associated scripting language.

    ```powershell
    iwr -useb https://storage.googleapis.com/encore-cli/install.ps1 | iex
    ```

*   **Linux:**  Linux users can install Encore using **Curl**, a command-line tool for transferring data with URLs.

    > **Curl:** A command-line tool and library for transferring data with URLs. It supports various protocols, including HTTP, HTTPS, FTP, and more.

    ```bash
    curl -sfL https://storage.googleapis.com/encore-cli/install.sh | sh
    ```

After successful installation, the **Encore CLI** (Command Line Interface) becomes accessible.

> **Encore CLI (Command Line Interface):** A text-based interface for interacting with the Encore platform. It provides commands for creating projects, running local development servers, deploying applications, and managing Encore resources.

Executing the `encore` command in the terminal displays a list of available commands and options.  The `encore version` command can be used to check the installed Encore CLI version.

### Creating a New Project

To initiate a new Encore project, the `encore app create` command is used. This command may prompt users to log in or create a cloud account if not already done.

```bash
encore app create
```

During project creation, users are asked to choose between **Go** or **TypeScript** for their project.  They are also presented with a selection of project **templates**, including:

> **Templates:** Pre-configured project structures that provide a starting point for different types of applications.

*   **REST API:** A template for building **RESTful APIs**.

    > **REST API (Representational State Transfer API):** An architectural style for designing networked applications. REST relies on a stateless, client-server, cacheable communications protocol -- and in virtually all cases, the HTTP protocol is used.

*   **Uptime Monitor:** A template for creating an **uptime monitoring** service.

    > **Uptime monitor:** A service that periodically checks the availability and responsiveness of a website or application.

*   **URL Shortener:** A template for building a **URL shortening** service, similar to the project example in the transcript.
*   **Empty App:** A basic template with minimal pre-configured settings, offering a blank canvas for custom application development.

Choosing the **empty app** template allows for building projects from scratch, providing maximum flexibility.  Users are then prompted to provide an **app name** for their project.

> **App name:** The identifier for an Encore application, used for organization and management within the Encore platform.

After specifying the app name and template, Encore proceeds to create the project directory, install necessary dependencies, and provide a web URL for accessing the project's dashboard.

Upon opening the project directory in a code editor like VS Code, the project structure is revealed. The `package.json` file contains project dependencies, including `encore.dev`. The project dashboard, accessible via the provided URL, displays services, **publish-subscribe topics**, **cron jobs**, and other project-related information.

> **package.json:** A file in the root of a Node.js project that describes the project's dependencies, scripts, and other metadata.

The dashboard also provides features like a **service catalog flow**, code **snippets**, an **AI lab**, and **tracing and logging** interfaces, offering a comprehensive development and management environment.

## Project Structure and API Endpoints

### Project Dashboard Overview

The Encore project dashboard serves as a central control panel for managing and interacting with your application. It provides a visual interface for:

*   **Services:** Viewing and managing the services that make up your application.
*   **Endpoints:** Inspecting and testing API **endpoints**.

    > **Endpoints:** Specific URLs or routes in an API that correspond to different functionalities or resources.

*   **Publish/Subscribe Topics:** Monitoring and managing asynchronous message queues.
*   **Cron Jobs:** Scheduling and reviewing automated tasks.
*   **Service Catalog Flow:** Visualizing the relationships and dependencies between services.
*   **Code Snippets:** Accessing pre-written code snippets for common tasks.
*   **AI Lab:** Exploring experimental AI-powered development tools.
*   **Tracing and Logging:** Analyzing request flows and application logs for debugging and monitoring.

The dashboard effectively acts as a built-in **Postman**-like tool, allowing developers to test API endpoints directly without needing external applications.

### Creating a Basic Endpoint

Encore simplifies the creation of API endpoints.  Endpoints are typically organized within a folder structure that mirrors the desired API URL structure.  For example, to create an endpoint at `/greeting`, a folder named `greeting` would be created. Within this folder, a file (e.g., `greeting.ts`) would define the endpoint logic.

To define an endpoint, the `API` function is imported from `encore.dev/api`.

```typescript
import { API } from 'encore.dev/api';
```

An endpoint is then defined by exporting a function and assigning it to `API()`, configuring the endpoint's properties within the `API()` call.

```typescript
export const greeting = API({
    method: 'GET',
    path: '/greeting',
    expose: true,
}, async () => {
    // Endpoint logic here
});
```

*   **method:** Specifies the HTTP **method** for the endpoint (e.g., 'GET', 'POST').

    > **Method (HTTP method):**  Indicates the desired action to be performed for a given resource in an HTTP request. Common methods include GET (retrieve data), POST (create new data), PUT (update existing data), and DELETE (remove data).

*   **path:** Defines the URL **path** for the endpoint.

    > **Path (URL path):** The part of a URL that identifies a specific resource within a web server.

*   **expose:** A boolean value indicating whether the endpoint should be publicly **exposed**.

    > **Expose:** To make an API endpoint publicly accessible over the internet.

The second argument to `API()` is an **async function** that contains the endpoint's business logic.

> **Async function:** A function that allows asynchronous operations using the `async` and `await` keywords, enabling non-blocking execution.

This function should return a **Promise** that resolves to the desired response type.

> **Promise:** An object representing the eventual completion (or failure) of an asynchronous operation and its resulting value.

**TypeScript Interfaces for Type Safety:**

To leverage TypeScript's type safety, interfaces are often defined to specify the structure of request and response data.

```typescript
interface Response {
    data: string;
}
```

The endpoint function is then typed to return a `Promise` of the defined response interface.

```typescript
async (): Promise<Response> => {
    return { data: 'Hello, world!' };
}
```

After saving the endpoint file, the Encore development server may need to be restarted (`encore run`) for the new endpoint to be registered and visible in the dashboard.

### Handling Path Parameters

To capture dynamic segments in the URL path, **path parameters** are used.

> **Path parameters:**  Dynamic segments within a URL path that are used to identify specific resources. They are typically denoted by colons in route definitions (e.g., `/users/:userId`).

Path parameters are defined in the `path` property using a colon prefix (e.g., `/greeting/:name`).  The parameter name (e.g., `name`) is then accessible as an argument to the endpoint function.

```typescript
export const greeting = API({
    method: 'GET',
    path: '/greeting/:name',
    expose: true,
}, async ({ name }: { name: string }): Promise<Response> => {
    return { data: `Hello, ${name}!` };
});
```

### Handling Query Parameters

**Query parameters** are used to pass optional data to an endpoint via the URL.

> **Query parameters:**  Key-value pairs appended to the end of a URL after a question mark (?). They are used to pass additional information to the server, often for filtering, sorting, or pagination.

To access query parameters, the `query` function is imported from `encore.dev/api`.

```typescript
import { API, query } from 'encore.dev/api';
```

An interface is defined to specify the expected query parameters, using `query<string>` to indicate that the `filter` query parameter is expected to be a string.

```typescript
interface SearchParams {
    filter: query<string>;
}
```

The endpoint function is then defined to accept the query parameters interface using **generics**.

> **Generics:**  A feature in programming languages that allows types to be parameters to type definitions. Generics enable writing code that can work with different types while maintaining type safety.

```typescript
export const search = API<SearchParams, SearchResponse>({
    method: 'GET',
    path: '/greeting/search',
    expose: true,
}, async ({ filter }): Promise<SearchResponse> => {
    return { matches: `Matched: ${filter}` };
});
```

The query parameters are then accessible within the endpoint function's arguments. The Encore dashboard provides input fields for specifying query parameter values when testing endpoints.

## Building a URL Shortener Service

### Endpoint 1: Shortening a URL (POST /url)

To build a URL shortener service, the first endpoint required is one that accepts a long URL and returns a shortened URL. This endpoint will use the POST method at the `/url` path.

**Functionality:**

1.  **Receive Long URL:** The endpoint receives a long URL in the request body.
2.  **Generate Short ID:** It generates a unique short ID for the URL. **Random bytes** from the **crypto** module are used to create a cryptographically secure random ID.

    > **Random bytes:**  A sequence of bytes generated randomly or pseudo-randomly, often used for cryptographic purposes, such as generating unique IDs or keys.
    >
    > **crypto:** A Node.js core module that provides cryptographic functionality, including generating random numbers, hashing, and encryption.

    This ID is then encoded into a **base64 URL** string for URL-safe characters.

    > **Base64 URL:** A URL-safe variant of Base64 encoding, which is a binary-to-text encoding scheme that represents binary data in an ASCII string format. Base64 URL encoding replaces characters that are not URL-safe with URL-safe alternatives.

3.  **Store in Database:** The long URL and its corresponding short ID are stored in a **database schema**. A **migration file** is used to define the database schema.

    > **Database schema:** The structure of a database, defining tables, columns, relationships, and constraints.
    >
    > **Migration file:** A script that defines changes to a database schema. Migration files are used to track and apply database schema updates in a controlled and versioned manner.

    Encore simplifies database operations through the **SQL database utility**.

    > **SQL database utility:** A feature provided by Encore that simplifies interaction with SQL databases, including setup, schema migration, and querying.

    Encore automatically sets up a **Docker container** running a Postgres database when a database resource is defined in the code.

    > **Docker container:** A standardized unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

    A **database instance** is created using `SQLDatabase` from `encore.storage.sqldb`.

    > **Database instance:** A running instance of a database server.

    The `migrations` option points to the directory containing **migration files**.

    > **Migrations folder:** A directory within an Encore project that contains SQL migration files for managing database schema changes.

4.  **Return Short ID:** The endpoint returns the generated short ID and the original URL in the response.

**Code Implementation:**

```typescript
import { API } from 'encore.dev/api';
import { SQLDatabase } from 'encore.dev/storage/sqldb';
import { randomBytes } from 'node:crypto';

const db = new SQLDatabase('url_shortener', {
    migrations: './migrations',
});

interface URLResponse {
    id: string;
    url: string;
}

interface URLParams {
    url: string;
}

export const shorten = API<URLParams, URLResponse>({
    method: 'POST',
    path: '/url',
    expose: true,
}, async ({ url }): Promise<URLResponse> => {
    const id = randomBytes(6).toString('base64url');

    await db.exec`
        INSERT INTO url (id, original_url)
        VALUES (${id}, ${url})
    `;

    return { id, url };
});
```

**Migration File (`migrations/encore_create_url_tables.up.sql`):**

```sql
CREATE TABLE url (
    id TEXT PRIMARY KEY,
    original_url TEXT NOT NULL
);
```

*   **CREATE TABLE:** SQL command to create a new table named `url`.
*   **id TEXT PRIMARY KEY:** Defines a column named `id` of type TEXT as the **primary key**.

    > **Primary key:** A column or set of columns in a database table that uniquely identifies each row in the table. Primary keys enforce uniqueness and are used for efficient data retrieval.

*   **original\_url TEXT NOT NULL:** Defines a column named `original_url` of type TEXT that **cannot be null**.

    > **NOT NULL:** A constraint in database schema design that ensures a column cannot contain null values.

### Endpoint 2: Redirecting with Short ID (GET /url/:id)

The second endpoint handles redirection from a short URL to the original long URL. This endpoint uses the GET method at the `/url/:id` path, where `:id` is the short ID.

**Functionality:**

1.  **Receive Short ID:** The endpoint receives the short ID as a path parameter.
2.  **Retrieve Long URL:** It queries the database to retrieve the original long URL associated with the provided short ID using the `queryRow` method.

    > **queryRow method:** A method provided by Encore's SQL database utility to execute a SQL query and retrieve a single row of results.

3.  **Handle Not Found:** If no matching short ID is found in the database, an **API error** with a "not found" status is thrown using `APIError.notFound()`.

    > **API error:** An error response returned by an API to indicate that something went wrong during request processing.
    >
    > **Not found (404):** An HTTP status code indicating that the requested resource could not be found on the server.

4.  **Return Long URL:** If a matching short ID is found, the endpoint returns the corresponding long URL.

**Code Implementation:**

```typescript
export const getShortenedURL = API<{ id: string }, URLResponse>({
    method: 'GET',
    path: '/url/:id',
    expose: true,
}, async ({ id }): Promise<URLResponse> => {
    const row = await db.queryRow<{ original_url: string }>`
        SELECT original_url FROM url WHERE id = ${id}
    `;

    if (!row) {
        throw APIError.notFound('URL not found');
    }

    return { id, url: row.original_url };
});
```

## Deployment and Conclusion

### Deployment to Encore Cloud

Deploying an Encore application to the Encore Cloud platform is remarkably simple. After initializing a Git repository and committing the code, deployment is achieved with a single **Git** command:

> **Git:** A distributed version control system for tracking changes in source code during software development.

```bash
git push encore
```

This command triggers a deployment process, pushing the application code to Encore's **staging environment**.

> **Staging environment:** A deployment environment that mirrors the production environment and is used for testing and quality assurance before deploying to production.

The deployment status can be monitored on the Encore Cloud dashboard, accessible via `app.encore.dev`. The dashboard displays deployment logs and progress.

### Staging Environment

Once deployed, the application is accessible in the **staging environment**. Encore provides a staging URL for testing and verification.  The staging environment allows developers to test the application in a cloud environment that closely resembles the **production environment**.

> **Production environment:** The live environment where the application is deployed and accessible to end-users.

### Production Deployment

While the transcript primarily focuses on staging deployment, Encore also supports deployment to **production environments**.  Details on production deployment, including scaling and **pricing structure**, can be found in Encore's official documentation.

> **Production environment:** The live environment where the application is deployed and accessible to end-users.
>
> **Pricing structure:** The cost model for using a service or platform, typically outlining different pricing tiers and features.

### Further Exploration

Encore presents a compelling platform for backend development, offering significant advantages in terms of developer productivity, performance, and simplified DevOps. This chapter provides an introductory overview. Further exploration of Encore's documentation and experimentation with its features are recommended for a deeper understanding and appreciation of its capabilities.
