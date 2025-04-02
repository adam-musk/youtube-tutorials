---
layout: "../../layouts/BlogPost.astro"
title: "Deploying Web Applications: A Comprehensive Guide"
pubDate: "2025-03-01 14:47:56.309135"
youtubeVideoID: "vROMXzOWqec"
index:
---

# Deploying Web Applications: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/vROMXzOWqec" frameborder="0" allowfullscreen></iframe>


## Introduction to Web Application Deployment

Welcome to this tutorial on deploying web applications. In this chapter, we will explore various methods and platforms for deploying your web applications, ensuring they are accessible to users online. We will cover both open-source solutions and cloud platform deployments, providing you with the knowledge to choose the most suitable option for your projects. The steps outlined in this chapter are broadly applicable across different programming languages and frameworks. The technologies demonstrated serve as practical examples to guide you through the deployment process.

> **Web applications:**  These are applications accessed via a web browser over a network like the internet. They are distinct from traditional desktop applications and leverage web technologies for functionality and user interaction.

> **Framework:** In software development, a framework provides a standardized structure and set of tools to build applications. It simplifies development by offering pre-built components and conventions.

> **Open Source:** This term refers to software with source code that is publicly accessible. Users can freely use, modify, and distribute open-source software, fostering collaboration and community-driven development.

This chapter is divided into two main sections:

*   **Section 1: Open-Source Deployment Options:**  We will begin by exploring deployment methods using open-source platforms, focusing on ease of use and accessibility, especially for hobby projects and learning purposes.
*   **Section 2: Cloud Provider Deployment (Microsoft Azure):**  We will then delve into deploying applications using a major cloud provider, Microsoft Azure, demonstrating how to leverage cloud infrastructure for robust and scalable deployments.

Let's embark on this journey to make your web applications live and accessible to the world.

## Section 1: Open-Source Deployment Options

This section will guide you through deploying web applications using open-source platforms. We will explore two different approaches, utilizing platforms that offer free tiers suitable for development, testing, and hobby projects.

### 1.1 Deployment using Render

Render is a platform that simplifies the deployment of both frontend and backend components of web applications. It supports various programming languages and frameworks and offers a user-friendly interface.

> **Backend:** This is the server-side component of a web application, responsible for data storage, processing, and business logic. It typically interacts with databases and APIs to manage and serve data to the frontend.

> **Frontend:** This is the client-side component of a web application, which users directly interact with in their web browser. It is responsible for the user interface and user experience, displaying information and handling user interactions.

Let's deploy our first application, "exams," which consists of a backend API and a frontend.

#### 1.1.1 Backend Deployment with Render

**Steps:**

1.  **Sign up for Render:**
    *   Navigate to the Render website and register for an account.
    *   Verify your email address to activate your account.
    *   Set up your account profile as prompted.

2.  **Create a PostgreSQL Database:**
    *   Render requires a PostgreSQL database for the "exams" backend.
    *   In the Render dashboard, create a new PostgreSQL database instance.
    *   Provide a unique name for your database (e.g., "myDB").
    *   **Crucially, select the same region for your database and backend web servers (e.g., Frankfurt).** This minimizes latency and improves performance.
    *   Choose the free tier suitable for hobby projects.
    *   Create the database.

    > **PostgreSQL (Postgres or POS):** This is a powerful, open-source relational database management system (RDBMS) known for its reliability, feature richness, and SQL compliance. It's often used for web application backends.

3.  **Create a Web Service for the Backend:**
    *   In the Render dashboard, create a new "Web Service."
    *   Select "Deploy from a public Git repository."
    *   Paste the URL of your backend API's Git repository.
        *   Render automatically detects the use of Node.js and sets the region to Frankfurt (matching the database).
    *   **Configure Build and Start Commands:**
        *   **Build Command:**
            *   `npm install` (installs Node.js dependencies)
            *   `npm run db:generate` (generates Prisma client for database interaction - specific to this project)
            *   `npm run build` (transpiles TypeScript code to JavaScript - specific to TypeScript projects)
        *   **Start Command:** `npm start` (starts the Node.js backend server)
    *   Choose the free instance type.

    > **Repository:** In version control systems like Git, a repository is a storage location for all the files and revision history of a project. It allows for tracking changes and collaboration.

    > **API (Application Programming Interface):** An API is a set of rules and specifications that software programs can follow to communicate with each other. In web applications, APIs often define how the frontend interacts with the backend to request and exchange data.

    > **Node.js:** This is a JavaScript runtime environment that allows you to execute JavaScript code server-side. It's popular for building web application backends due to its event-driven, non-blocking architecture.

    > **npm (Node Package Manager):** npm is the default package manager for Node.js. It's used to install, manage, and share JavaScript packages and libraries, simplifying dependency management in Node.js projects.

    > **TypeScript:** This is a superset of JavaScript that adds optional static typing. It enhances code maintainability and scalability, especially in large projects, by catching type-related errors during development.

    > **Prisma:** Prisma is an open-source ORM (Object-Relational Mapper) for Node.js and TypeScript. It simplifies database access and management by providing a type-safe and intuitive way to interact with databases.

4.  **Set Environment Variables:**
    *   Environment variables are used to configure applications without hardcoding sensitive information or settings directly into the code.
    *   Refer to the `.env.example` file in your backend repository for required environment variables.
    *   **Database URL:**
        *   Navigate to your PostgreSQL database instance in the Render dashboard.
        *   Copy the "Internal Database URL" provided by Render.
        *   Add a new environment variable named `DATABASE_URL` in your web service settings and paste the copied URL as the value.
    *   **JWT Secret Key:**
        *   Generate a random, secure value for the `JWT_SECRET_KEY` environment variable. This key is used for signing and verifying JSON Web Tokens for authentication and authorization.
        *   Add a new environment variable named `JWT_SECRET_KEY` and paste the generated random value.
    *   **Admin Credentials (Username & Password):**
        *   Set environment variables for `ADMIN_USERNAME` and `ADMIN_PASSWORD` to define the credentials for the application administrator.
    *   Skip the "Advanced" section and create the web service.

    > **Environment variables:** These are dynamic named values that can affect the behavior of programs running on a computer. They are often used to configure applications without modifying their source code, especially for settings that vary between environments (development, staging, production).

    > **JWT (JSON Web Token) Secret Key:** JWTs are used for securely transmitting information between parties as a JSON object. A secret key is used to digitally sign these tokens, ensuring their integrity and authenticity. It's crucial for security to keep this key confidential.

5.  **Deployment Process:**
    *   Render will clone your repository, execute the build commands (`npm install`, `npm run db:generate`, `npm run build`), and then start the application using the start command (`npm start`).
    *   Monitor the deployment progress in the Render dashboard.
    *   Once deployment is successful, Render will indicate that your service is live and provide a URL to access your backend API.

6.  **Testing the Backend:**
    *   Access the provided URL for your backend API.
    *   Test an endpoint, such as `/questions`, to verify the backend is running correctly. You should expect a response indicating that a token is needed, confirming the API is functional and protected.

#### 1.1.2 Frontend Deployment with Render

**Steps:**

1.  **Create a Static Site on Render:**
    *   In the Render dashboard, create a new "Static Site."
    *   Select "Deploy from a public Git repository."
    *   Paste the URL of your frontend repository.
    *   Render automatically detects the necessary settings.
    *   **Configure Build Settings:**
        *   **Build Command:** `npm install && npm run build`
        *   **Publish directory:** `dist` (or the directory where your frontend build output is located)

    > **Static site:** A static website consists of web pages served to the user exactly as stored, in contrast to dynamic websites which generate content on the server-side. Static sites are often used for frontends built with frameworks like React, Vue, or Svelte after they are compiled into static HTML, CSS, and JavaScript files.

2.  **Set Environment Variables:**
    *   You need to configure the base URL for your backend API in the frontend environment variables so that the frontend knows where to send API requests.
    *   **API Base URL:**
        *   Add an environment variable named `VITE_API_BASE_URL` (or the appropriate variable name used in your frontend project - check your frontend's configuration files).
        *   Set the value to the base URL of your deployed backend API (obtained from the previous backend deployment steps).
    *   Create the static site.

3.  **Deployment and Testing:**
    *   Render will clone your frontend repository, run the build command, and deploy the static files from the specified publish directory.
    *   Once deployed, Render will provide a URL for your static site.
    *   Access the provided URL to view your frontend application.
    *   Use browser developer tools (Network tab) to verify that the frontend is correctly sending requests to your deployed backend API. Test functionalities like form submissions to ensure end-to-end connectivity.

### 1.2 Deployment using Kibo and Cloudflare Pages

This section will guide you through deploying another web application, "my super awesome app," using a combination of Kibo for backend deployment and Cloudflare Pages for frontend deployment. This setup also leverages free tiers and demonstrates deployment with different technologies like Bun and MongoDB.

> **Bun:** Bun is a fast, all-in-one JavaScript runtime, bundler, transpiler, and package manager. It's designed to be a faster alternative to Node.js and npm, offering performance improvements in JavaScript and TypeScript development.

> **MongoDB:** This is a popular NoSQL database, categorized as a document database. It's known for its flexibility, scalability, and ease of use, often chosen for applications requiring flexible data schemas and high availability.

> **NoSQL database:** NoSQL databases (Not only SQL) are databases that do not adhere to the traditional relational database structure (tables with rows and columns). They are designed for scalability, flexibility, and performance, often handling unstructured or semi-structured data.

#### 1.2.1 Backend Deployment with Kibo

Kibo is a platform designed for deploying Dockerized applications. It provides a straightforward way to deploy applications defined by Dockerfiles.

> **Dockerfile:** A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble a Docker image. It automates the process of creating container images.

> **Docker image:** A Docker image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings. Images are used to create containers.

**Steps:**

1.  **Set up MongoDB Atlas:**
    *   MongoDB Atlas is a cloud database service for MongoDB.
    *   Register for a MongoDB Atlas account.
    *   Verify your email address.
    *   Follow the setup prompts, choosing the free tier and unchecking "Preload Sample Dataset."
    *   Create a deployment.
    *   **Configure Network Access:**
        *   In MongoDB Atlas, navigate to "Network Access."
        *   Add your current IP address for local connectivity. For broader access during development, you can "Allow Access from Anywhere," but for production, restrict access to known IP addresses.
    *   **Create a Database User:**
        *   Navigate to "Database Access."
        *   Add a new database user (e.g., "user1").
        *   Auto-generate a secure password and save it securely.
        *   Grant the user "Read and write to any database" role.
    *   **Get Connection String:**
        *   Go to "Database" and click "Connect."
        *   Select "Drivers" and choose "Node.js."
        *   Copy the provided connection string.
        *   Replace the `<password>` placeholder in the connection string with the password you generated for your database user. Save this updated connection string.

    > **MongoDB Atlas:** This is MongoDB's fully managed cloud database service. It simplifies deploying, operating, and scaling MongoDB databases in the cloud, handling infrastructure management and providing features like automated backups and monitoring.

2.  **Set up MailerSend (Email API):**
    *   MailerSend is an email delivery service.
    *   Sign up for a MailerSend account.
    *   Verify your email address.
    *   Navigate to "SMTP Relays" and then "Manage."
    *   Note the trial domain provided by MailerSend, which you can use for sending emails.
    *   Generate a new API token (e.g., "my super awesome token") and copy the value. Save this API token.

    > **API key:** An API key is a code used to identify and authenticate an application or user when calling an API. It's a security measure to control access and track API usage.

3.  **Set up ImageHippo (Image Upload API):**
    *   ImageHippo is a free image hosting service.
    *   Create an account on ImageHippo.
    *   Go to "API" and add a new API key.
    *   Copy and save the API key.

4.  **Sign up for Kibo:**
    *   Register for a Kibo account.
    *   Verify your email address.
    *   Set up your organization and name.

5.  **Create a Web Service on Kibo for the Backend:**
    *   In the Kibo dashboard, create a new "Web Service."
    *   Select "GitHub" and enter the URL of your backend API's public GitHub repository.
    *   Choose the free CPU option.
    *   For "Configuration," select "Dockerfile." Kibo will detect the Dockerfile in your repository.
    *   **Set Environment Variables:**
        *   Select "Bulk Import" and upload your `.env.example` file from your backend repository.
        *   Remove the `PORT` definition as Kibo manages port assignment.
        *   Update the `MONGODB_URI` environment variable with the MongoDB connection string you configured earlier (including the password).
        *   Set the following environment variables using the credentials you obtained:
            *   `EMAIL_API_KEY` (from MailerSend)
            *   `EMAIL_FROM_NAME` (e.g., "My Awesome App")
            *   `EMAIL_FROM_ADDRESS` (e.g., `abc@your-mailersend-domain.mailersend.net` - using the MailerSend trial domain)
            *   `IMAGE_UPLOAD_API_KEY` (from ImageHippo)
            *   Leave `FRONTEND_BASE_URI` empty for now. We will update this after deploying the frontend.
        *   Save the environment variables.

6.  **Deploy the Backend:**
    *   Create the web service in Kibo.
    *   Kibo will build the Docker image using the Dockerfile in your repository and deploy the container.
    *   Monitor the deployment progress in the Kibo dashboard.
    *   Once deployment is successful, Kibo will provide a base URL for your backend API.

7.  **Test the Backend:**
    *   Access the provided backend API base URL.
    *   Test an endpoint like `/articles` to verify the backend is running and responding.

#### 1.2.2 Frontend Deployment with Cloudflare Pages

Cloudflare Pages is a platform for deploying static websites and frontend applications. It offers fast deployment and integration with Cloudflare's global network.

> **Cloudflare Pages:** This is a platform from Cloudflare specifically designed for deploying static websites and frontend applications. It offers fast global content delivery, serverless functions, and seamless integration with Cloudflare's CDN and security features.

**Steps:**

1.  **Sign up for Cloudflare Pages:**
    *   Register for a Cloudflare account.
    *   Verify your email address.
    *   Navigate to "Workers & Pages" and click "Pages."
    *   Connect to GitHub and authorize Cloudflare Pages to access your GitHub account.
    *   Select your frontend repository ("my super awesome app frontend").
    *   Begin setup.

2.  **Configure Deployment Settings:**
    *   For "Framework preset," choose "Svelte" (or the framework your frontend uses).
    *   Set the "Build command" to `npm run build`.
    *   Set the "Build output directory" to `dist`.
    *   **Set Environment Variables:**
        *   Add an environment variable `VITE_API_BASE_URL` (or the appropriate variable name for your frontend project).
        *   Set the value to the base URL of your backend API deployed on Kibo.
    *   Save and deploy.

    > **Svelte:** Svelte is a free and open-source compiler that turns your declarative components into highly efficient JavaScript that surgically updates the DOM. It's a frontend framework like React and Vue.js, but with a different approach to performance and reactivity.

3.  **Deployment and Testing:**
    *   Cloudflare Pages will clone your frontend repository, build the application, and deploy the static files to its global network.
    *   Deployment is typically very fast.
    *   Once deployed, Cloudflare Pages will provide a URL for your frontend application. It may take a few minutes for the URL to become fully active.
    *   Access the provided URL to view your frontend application.

4.  **Update Backend Environment Variables with Frontend URL:**
    *   Now that your frontend is deployed and has a URL, you need to update the backend environment variables in Kibo.
    *   Go back to Kibo, navigate to your "my super awesome API" service, and go to "Settings" -> "Environment Variables."
    *   Update the `FRONTEND_BASE_URI` environment variable with the URL of your deployed frontend from Cloudflare Pages.
    *   Trigger a "Build and Deploy" in Kibo to redeploy the backend with the updated environment variable. This is necessary for features like email verification that rely on the frontend URL.

5.  **Test the Complete Application:**
    *   Access your frontend application via the Cloudflare Pages URL.
    *   Test functionalities like user signup, login, creating articles, and image uploads to ensure everything is working correctly end-to-end. Verify that email verification is working as expected.

## Section 2: Cloud Provider Deployment: Microsoft Azure

This section will guide you through deploying a full-stack web application on Microsoft Azure, a leading cloud computing platform. We will use Azure Virtual Machines to host our application, providing a more hands-on approach to server management within a cloud environment.

> **Cloud Provider:** A cloud provider is a company that offers cloud computing services, which include infrastructure (like servers, storage, and networks), platforms (for application development and deployment), and software (applications delivered over the internet). Examples include Microsoft Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP).

> **Microsoft Azure:** This is a cloud computing service created by Microsoft for building, testing, deploying, and managing applications and services through Microsoft-managed data centers. It offers a wide range of services, including virtual machines, databases, and web application hosting.

> **Azure Virtual Machine:** This is an on-demand, scalable computing resource available in Azure. It provides you with the flexibility of virtualization without having to buy and maintain the physical hardware that runs it. You can choose from a gallery of operating systems, including Windows and Linux.

### 2.1 Deploying on Azure Virtual Machine

We will deploy the "exams" application (previously deployed on Render) on an Azure Virtual Machine. This will involve setting up a virtual machine, configuring the server environment, and deploying both the frontend and backend components.

**Steps:**

1.  **Create an Azure Virtual Machine:**
    *   Log in to the Azure portal.
    *   Search for "Virtual machines" and create a new virtual machine.
    *   **Basic Configuration:**
        *   **Name:** Choose a name for your virtual machine (e.g., "HelloWorld-VM").
        *   **Region:** Select a region geographically close to your users.
        *   **Image:** Choose "Ubuntu 22.04 LTS" (a common Linux distribution).
        *   **Size:** Select "Standard_B1s" (or a suitable size based on your needs and budget; `Standard_B1s` is a basic, cost-effective option).
        *   **Administrator account:**
            *   **Authentication type:** Select "SSH public key."

            > **SSH (Secure Shell):** SSH is a cryptographic network protocol that allows you to securely access and manage servers over an unsecured network. It provides encrypted communication between two computers, commonly used for remote server administration and file transfers.

            > **Key pair:** A key pair consists of a public key and a private key used for SSH authentication. The public key is placed on the server, and the private key is kept securely by the user. When connecting via SSH, the private key is used to prove identity without transmitting a password.

            *   **Username:** Set a username (e.g., `azureuser`).
            *   **Key pair name:** "HelloWorld-key" (or a descriptive name).
        *   **Inbound rules:**
            *   **Public inbound ports:** Allow "HTTP (80)" and "HTTPS (443)" traffic to make your web application accessible over the internet.

            > **Inbound traffic:** In network security, inbound traffic refers to network communication originating from outside a network (like the internet) and directed towards resources within the network (like a server or virtual machine).

    *   Create the virtual machine.
    *   Download the private key file (`HelloWorld-key.pem`). **Store this file securely as it's essential for accessing your virtual machine.**

2.  **Connect to the Virtual Machine via SSH:**
    *   **Change Permissions of Private Key:**
        *   Open a terminal and navigate to the directory where you downloaded the private key file.
        *   Use the command `chmod 400 HelloWorld-key.pem` to restrict permissions to only the owner (you), enhancing security.
    *   **Connect using SSH command:**
        *   In the Azure portal, navigate to your virtual machine, click "Connect," and select "SSH."
        *   Copy the provided SSH command. It will look similar to: `ssh azureuser@<public-ip-address> -i HelloWorld-key.pem`
        *   Replace `HelloWorld-key.pem` with the actual path to your downloaded private key file if necessary.
        *   Run the SSH command in your terminal. Type `yes` if prompted to continue connecting. You will be logged into your Azure Virtual Machine's terminal.

3.  **Install Node.js and Dependencies:**
    *   **Install `unzip`:** `sudo apt update && sudo apt install unzip` (needed for `fnm` installation).
    *   **Install `fnm` (Fast Node.js Manager):**
        *   `curl -fsSL https://fnm.vercel.app/install.sh | bash`
        *   Follow the on-screen instructions to set up `fnm` in your shell environment (usually involves adding a line to your `.bashrc` or `.zshrc` file and sourcing it).
        *   After setup, verify `fnm` is working by running `fnm --version`.
    *   **Install Node.js LTS:** `fnm install lts` (installs the latest Long-Term Support version of Node.js).
    *   Verify Node.js installation: `node -v` and `npm -v`.

    > **Node Version Manager (nvm or fnm):** These tools allow you to manage multiple versions of Node.js on your system. This is helpful for projects that may require different Node.js versions. `fnm` (Fast Node.js Manager) is a Node.js version manager written in Rust, known for its speed and efficiency.

4.  **Deploy Backend API:**
    *   **Clone Backend Repository:**
        *   On your VM terminal, navigate to your home directory (`cd ~`).
        *   Clone your backend API repository using `git clone <backend-repository-url> exams-backend`.
        *   Navigate into the backend directory: `cd exams-backend`.
    *   **Install Backend Dependencies:** `npm install`.
    *   **Copy Environment File:** `cp .env.example .env`.
    *   **Generate Prisma Client and Build (if necessary):**
        *   `npm run db:generate`
        *   `npm run build` (if it's a TypeScript project).

5.  **Set up PostgreSQL Database in Docker:**
    *   **Install Docker:**
        *   `sudo apt update`
        *   `sudo apt install docker.io`
        *   `sudo systemctl start docker`
        *   `sudo systemctl enable docker`
        *   `sudo usermod -aG docker $USER` (add current user to the Docker group - you may need to log out and back in or run `newgrp docker` for this to take effect).
    *   **Run PostgreSQL Docker Container:**
        *   `docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres:16`
            *   `-d`: Runs the container in detached mode (in the background).
            *   `-p 5432:5432`: Maps port 5432 on the host (VM) to port 5432 in the container (PostgreSQL default port).
            *   `-e POSTGRES_PASSWORD=mysecretpassword`: Sets the PostgreSQL superuser password. **Change `mysecretpassword` to a strong, secure password for production environments.**
            *   `postgres:16`: Specifies the PostgreSQL Docker image to use (version 16).

    > **Docker containerization:** Containerization is a method of packaging software code with its dependencies into isolated units called containers. Docker is a popular platform for containerization, enabling consistent application deployment across different environments.

6.  **Configure Backend Environment Variables:**
    *   Edit the `.env` file in your `exams-backend` directory using a text editor like `nano` or `vim`.
    *   Update the `DATABASE_URL` to point to the PostgreSQL database running in Docker. The connection string will typically be: `postgresql://postgres:mysecretpassword@localhost:5432/postgres?schema=public` (adjust username, password, host, port, and database name if needed).
    *   Set other necessary environment variables (e.g., `JWT_SECRET_KEY`, `ADMIN_USERNAME`, `ADMIN_PASSWORD`).

7.  **Start Backend Application:**
    *   **Using `npm start` (for testing):** `npm start` to run the backend directly in the terminal.
    *   **Using `pm2` (Process Manager for production):**

        > **Process manager (pm2):** A process manager is a tool that helps you manage and daemonize applications, ensuring they run continuously in the background, automatically restart upon crashes, and provide features for monitoring and logging. `pm2` is a popular process manager for Node.js applications.

        *   **Install `pm2` globally:** `npm install pm2 -g`.
        *   **Start backend with `pm2`:** `pm2 start npm -- start`. This starts your backend using `npm start` and manages it with `pm2`.
        *   **Save process list:** `pm2 save` (makes sure your application restarts automatically after server reboot).
        *   **List managed processes:** `pm2 list` or `pm2 status` to check the status of your backend application.

8.  **Test Backend:**
    *   From your local machine's browser, access your VM's public IP address followed by the backend API port (default is often 5000, e.g., `http://<vm-public-ip>:5000`).
    *   Test API endpoints (like `/questions`) to verify the backend is running and accessible.

9.  **Deploy Frontend Application:**
    *   **Clone Frontend Repository:**
        *   On your VM terminal, navigate to your home directory (`cd ~`).
        *   Clone your frontend repository using `git clone <frontend-repository-url> exams-frontend`.
        *   Navigate into the frontend directory: `cd exams-frontend`.
    *   **Install Frontend Dependencies:** `npm install`.
    *   **Build Frontend:** `npm run build`.

10. **Install and Configure Caddy Web Server:**

    > **Web server (Caddy):** A web server is software that handles HTTP requests from clients (web browsers) and serves web content, such as HTML pages, images, and other files. Caddy is a modern, easy-to-configure web server known for its automatic HTTPS and simplicity.

    > **DNS (Domain Name System):** DNS is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It translates domain names (like `example.com`) into IP addresses that computers use to locate each other.

    > **Subdomain:** A subdomain is a domain that is part of a larger domain. For example, `api.example.com` is a subdomain of `example.com`. Subdomains are used to organize and separate different parts of a website or application.

    > **HTTPS (Hypertext Transfer Protocol Secure):** HTTPS is a secure version of HTTP, the protocol over which data is sent between your browser and the website you are connected to. The 'S' stands for 'Secure' and it means all communication between your browser and the website is encrypted.

    > **TLS certificate (Transport Layer Security certificate):** A TLS certificate (often referred to as an SSL certificate) is a digital certificate that verifies the identity of a website and encrypts traffic to and from the site using the TLS/SSL protocol. This ensures secure communication over HTTPS.

    *   **Install Caddy:**
        *   Follow the official Caddy installation instructions for Ubuntu. Typically involves adding the Caddy repository and using `apt install caddy`.
    *   **Check Caddy Status:** `sudo systemctl status caddy`. Ensure it is "active (running)."
    *   **Get VM Public IP Address:** In the Azure portal, find the public IP address of your virtual machine.
    *   **Configure DNS (using freedns.afraid.org as an example):**
        *   Sign up for a free DNS service like freedns.afraid.org.
        *   Add two subdomains:
            *   `exams.<your-chosen-domain>` pointing to your VM's public IP address.
            *   `api.exams.<your-chosen-domain>` pointing to your VM's public IP address.
    *   **Configure Caddyfile:**
        *   Edit the Caddyfile configuration file: `sudo nano /etc/caddy/Caddyfile`.
        *   Replace the default content with the following Caddyfile configuration:

        ```caddyfile
        exams.<your-chosen-domain> {
            root * /var/www/html/exams-frontend/dist
            file_server
            try_files {path} /index.html
        }

        api.exams.<your-chosen-domain> {
            reverse_proxy localhost:5000
        }
        ```

        *   Replace `<your-chosen-domain>` with the domain you registered in your DNS settings.
        *   `root * /var/www/html/exams-frontend/dist`: Sets the root directory for serving static files for the frontend.
        *   `file_server`: Enables serving static files.
        *   `try_files {path} /index.html`:  Handles single-page application routing by directing all requests to `index.html` if the requested file is not found.

        > **File server:** A file server is a computer responsible for the central storage and management of data files so that other computers on the same network can access those files. In web servers, it refers to the component that serves static files like HTML, CSS, JavaScript, and images.

        > **Port forwarding (reverse proxy):** Port forwarding, often implemented as a reverse proxy in web servers, is a technique to redirect network requests from one port or IP address to another. In this context, Caddy is acting as a reverse proxy, forwarding requests to `api.exams.<your-chosen-domain>` to the backend application running on `localhost:5000` on the same VM.

    *   **Move Frontend Build Files:**
        *   Create directories: `sudo mkdir -p /var/www/html/exams-frontend`.
        *   Move the built frontend files from `~/exams-frontend/dist` to `/var/www/html/exams-frontend/dist`: `sudo mv ~/exams-frontend/dist/* /var/www/html/exams-frontend/dist/`.
    *   **Reload Caddy Configuration:** `sudo systemctl reload caddy`.
    *   **Check Caddy Status:** `sudo systemctl status caddy` to ensure there are no errors and TLS certificate generation is successful. Caddy automatically obtains TLS certificates for HTTPS.

11. **Update Frontend API Base URL:**
    *   In your frontend application's configuration (e.g., environment variables or config file), update the API base URL to `https://api.exams.<your-chosen-domain>`.
    *   Rebuild and redeploy the frontend if necessary (in this Azure VM setup, you would rebuild on the VM and move the new `dist` folder contents to `/var/www/html/exams-frontend/dist`).

12. **Access and Test Application:**
    *   Access your deployed application in your browser using the domain you configured: `https://exams.<your-chosen-domain>`.
    *   Test all functionalities, including frontend-backend interactions, user signup, login, and exam functionalities. Verify that HTTPS is enabled (check for the padlock icon in your browser's address bar).

## Conclusion

Congratulations! You have successfully deployed web applications using both open-source platforms (Render, Kibo, Cloudflare Pages) and a cloud provider (Microsoft Azure Virtual Machine). This chapter has provided a comprehensive overview of different deployment strategies, from simplified platform-as-a-service solutions to more hands-on infrastructure management in the cloud. You now have a solid foundation to choose the most appropriate deployment method for your web projects based on your requirements, scale, and technical expertise. Remember to always consider security best practices, monitor your applications, and scale your infrastructure as needed.
