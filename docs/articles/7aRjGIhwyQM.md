---
layout: "../../layouts/BlogPost.astro"
title: "Setting Up a Linux Server and Deploying a MERN Stack Application"
pubDate: "2025-03-02 13:58:22.702726"
youtubeVideoID: "7aRjGIhwyQM"
index:
---

# Setting Up a Linux Server and Deploying a MERN Stack Application

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/7aRjGIhwyQM" frameborder="0" allowfullscreen></iframe>

This chapter will guide you through the process of setting up a Linux server from scratch and deploying a MERN stack application to production. We will be using Ubuntu Server as our operating system and Lenode as our cloud hosting provider, although the principles and steps outlined here are applicable to any Ubuntu server environment. This comprehensive guide aims to provide a deep understanding of the deployment process, offering more control and customization compared to simplified hosting platforms.

## 1. Introduction to Server Setup and Deployment

Deploying a web application to production involves making it accessible to users on the internet. While various hosting platforms offer simplified deployment processes, understanding how to set up a server manually provides invaluable control and insight into the underlying infrastructure. This chapter focuses on a hands-on approach, guiding you through each step of setting up a server and deploying a MERN stack application.

### 1.1 Why Manual Server Setup?

Choosing to set up a server manually, rather than using automated platforms, offers several advantages:

*   **Complete Control:** You have full control over the server environment, allowing for deep customization and optimization.
*   **Understanding Infrastructure:**  Manual setup fosters a deeper understanding of server architecture, networking, and deployment processes.
*   **Cost Efficiency (Potentially):** Depending on your needs and scale, managing your own server can be more cost-effective than using managed services.
*   **Flexibility:** You are not restricted by the limitations of specific platforms and can tailor the server to your exact application requirements.

However, it is important to acknowledge that manual setup requires more technical expertise and time compared to using automated platforms. This chapter is designed to equip you with the necessary knowledge and skills to confidently navigate this process.

### 1.2 Overview of the Deployment Process

This chapter will cover the following key steps to deploy a MERN stack application:

*   **Setting up a Server:**  Provisioning a virtual server instance using a cloud hosting provider.
*   **Configuring SSH Keys:** Enhancing security by using SSH keys for server access instead of passwords.
*   **Creating a New User:**  Improving security by creating a non-root user for day-to-day server operations.
*   **Transferring Application Files with Git:**  Using Git to securely and efficiently transfer application code to the server.
*   **Setting up a MongoDB Database:** Configuring a MongoDB database to store application data.
*   **Installing Node.js and Dependencies:** Setting up the runtime environment and installing necessary application dependencies.
*   **Utilizing PM2 Process Manager:** Employing PM2 to reliably run and manage the Node.js application in the background.
*   **Configuring a Firewall (UFW):** Securing the server by restricting access to essential ports only.
*   **Setting up Nginx as a Reverse Proxy:** Configuring Nginx to serve the application on standard HTTP ports (port 80) and handle incoming requests.
*   **(Optional) Domain Name Configuration:**  Associating a domain name with the server for easy access.

## 2. Server Setup with Lenode (or any Ubuntu Server)

For this guide, we will utilize Lenode, a cloud hosting provider, to provision an Ubuntu server. However, the steps are generally applicable to any Ubuntu server, whether it's hosted on a different cloud platform or even running locally.

> **Cloud Hosting Provider:** A company that provides computing services—including servers, storage, databases, networking, software, analytics, and intelligence—over the Internet ("the cloud"). These providers offer on-demand access to computing resources, typically on a pay-as-you-go basis.

Lenode has generously provided a credit for users to follow along with this tutorial. You can access this offer through the provided link.

### 2.1 Creating a Lenode Instance

1.  **Access the Lenode Dashboard:** Log in to your Lenode account or create a new one. Navigate to the dashboard where you can manage your server instances (Nodes).
2.  **Create a New Node:** Click on the button to create a new Lenode instance.
3.  **Choose an Operating System (Distro):** Select Ubuntu as the distribution. We recommend using Ubuntu 22.04 LTS (Long Term Support) for stability.

    > **Distro (Distribution):**  In the context of Linux, a distribution is an operating system made from a software collection that is based upon the Linux kernel. Ubuntu, Debian, Fedora, and CentOS are examples of popular Linux distributions.

4.  **Select a Region:** Choose a region geographically closest to your target audience or yourself for optimal latency.
5.  **Choose a Plan (Package):** Select a server plan that meets your application's resource requirements. For demonstration purposes, a dedicated 4GB plan is suitable.
6.  **Set a Label:** Provide a descriptive label for your server instance (e.g., "youtube-linux-server").
7.  **Set a Root Password:**  Create a strong password for the root user. This password will be used for initial access to the server.
8.  **SSH Key Setup (Recommended):**  For enhanced security, we will configure SSH keys. For now, you can skip this step and revisit it later in Section 3.
9.  **Create Lenode:** Click the "Create Lenode" button to provision your server. This process typically takes a few minutes.

### 2.2 Accessing Your Server via SSH

Once your Lenode instance is running, you will be provided with an IP address. You can use this IP address to connect to your server via SSH (Secure Shell).

> **SSH (Secure Shell):** A cryptographic network protocol that allows you to securely access and manage a remote computer or server over an unsecured network. SSH provides encrypted communication, preventing eavesdropping and man-in-the-middle attacks.

1.  **Open a Terminal:** Open your terminal application (e.g., Terminal on macOS/Linux, Command Prompt or PowerShell on Windows).
2.  **Connect as Root User:** Use the following command, replacing `YOUR_SERVER_IP` with the actual IP address of your server:

    ```bash
    ssh root@YOUR_SERVER_IP
    ```
3.  **Password Authentication:** The first time you connect, you will be prompted to confirm the connection. Type `yes` and press Enter. Then, enter the root password you set during server creation when prompted.

You are now logged into your Ubuntu server as the root user.

### 2.3 Updating Packages

After logging in, it's best practice to update the system packages to their latest versions.

1.  **Update Package Lists:** Run the following command to update the package lists:

    ```bash
    apt update
    ```

    > **apt (Advanced Package Tool):** A powerful command-line package manager used in Debian-based Linux distributions like Ubuntu. It simplifies the process of installing, updating, and removing software packages.

2.  **Upgrade Packages:** After updating the lists, run the following command to upgrade installed packages to their latest versions:

    ```bash
    apt upgrade
    ```

    Confirm the upgrade by typing `y` when prompted. This process may take some time depending on the number of packages to be upgraded.

## 3. Setting up SSH Keys for Secure Access

Using SSH keys is a more secure and convenient method for accessing your server compared to password-based authentication. SSH keys involve a pair of keys: a private key, which you keep secret on your local machine, and a public key, which you place on the server.

### 3.1 Generating SSH Key Pair on Your Client Machine

1.  **Open a Terminal on your Local Machine:** Open a terminal or command prompt on your computer (the machine you will use to connect to the server).
2.  **Generate SSH Key Pair:** Run the following command:

    ```bash
    ssh-keygen
    ```
3.  **Key Storage Location:** You will be prompted to enter a file in which to save the key. The default location (`~/.ssh/id_rsa`) is usually fine. To create a key specifically for this server setup, you can specify a different name, for example: `~/.ssh/id_rsa_lenode`.
4.  **Passphrase (Optional):** You can set a passphrase to protect your private key. This adds an extra layer of security. If you don't want a passphrase, just press Enter twice.

This command will generate two files in the `.ssh` directory (which might be hidden):

*   `id_rsa_lenode` (or `id_rsa` if you used the default): This is your **private key**. Keep this file secure and do not share it.
*   `id_rsa_lenode.pub` (or `id_rsa.pub` if you used the default): This is your **public key**. This is the key you will place on the server.

### 3.2 Adding the Public Key to the Server

1.  **Display Public Key:** Use the `cat` command to display the contents of your public key file in the terminal. Replace `id_rsa_lenode.pub` with the actual name of your public key file if you used a different name:

    ```bash
    cat ~/.ssh/id_rsa_lenode.pub
    ```
2.  **Copy the Public Key:** Carefully copy the entire output, starting from `ssh-rsa` and ending with your username or hostname.
3.  **Add Public Key to Lenode (if not done during server creation):**
    *   In the Lenode dashboard, navigate to your server instance.
    *   Look for the "SSH Keys" section (often found under the "Settings" or "Access" tab).
    *   Click "Add SSH Key" or a similar button.
    *   Paste the copied public key into the text box.
    *   Give the key a descriptive label (e.g., "My Laptop").
    *   Click "Add Key" or "Save".

    **Alternatively, add the public key directly to the server (if already logged in via password):**

    *   On your server terminal (logged in as root), navigate to the root user's SSH directory:

        ```bash
        cd ~/.ssh
        ```

    *   If the `.ssh` directory doesn't exist, create it: `mkdir .ssh`
    *   Create or edit the `authorized_keys` file: `nano authorized_keys`
    *   Paste the copied public key into this file.
    *   Save and close the file (Ctrl+X, then Y, then Enter in Nano).
    *   Ensure the correct permissions for the `.ssh` directory and `authorized_keys` file:

        ```bash
        chmod 700 ~/.ssh
        chmod 600 ~/.ssh/authorized_keys
        ```

### 3.3 Logging in with SSH Keys

Now you should be able to log in to your server using your SSH key without needing to enter a password.

1.  **Open a Terminal on your Local Machine.**
2.  **Connect via SSH:** Use the following command, replacing `YOUR_SERVER_IP` with your server's IP address:

    ```bash
    ssh root@YOUR_SERVER_IP
    ```

    If you generated a key with a name other than `id_rsa`, you might need to specify the private key file using the `-i` option:

    ```bash
    ssh -i ~/.ssh/id_rsa_lenode root@YOUR_SERVER_IP
    ```

If you set a passphrase for your private key, you will be prompted to enter it. Otherwise, you should be logged in directly without a password prompt.

### 3.4 Disabling Password Authentication for Root User (Optional, Recommended for Security)

For enhanced security, you can disable password authentication for the root user, forcing SSH key-based login.

1.  **Edit SSH Configuration File:** Log in to your server as root via SSH. Open the SSH configuration file using a text editor like Nano:

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
2.  **Find `PasswordAuthentication` and `PermitRootLogin`:** Locate the lines `PasswordAuthentication yes` and `PermitRootLogin yes`.
3.  **Modify the Lines:** Change `PasswordAuthentication yes` to `PasswordAuthentication no`. You can also consider changing `PermitRootLogin yes` to `PermitRootLogin no` to further restrict root access, but for this tutorial, we will leave it as `yes` for simplicity.
4.  **Save and Close:** Save the file (Ctrl+X, then Y, then Enter in Nano).
5.  **Restart SSH Service:** Restart the SSH service to apply the changes:

    ```bash
    sudo systemctl restart sshd
    ```

    > **systemctl:** A command-line utility in Linux used to manage and control the systemd system and service manager. It allows you to start, stop, restart, enable, disable, and check the status of services.

After this, password-based login for the root user will be disabled. Ensure you have SSH key-based access configured correctly before disabling password authentication.

## 4. Creating a New User for Enhanced Security

It is a security best practice to avoid using the root user for day-to-day server operations. Instead, create a new user with `sudo` privileges for administrative tasks.

> **Root User:** The administrator user in Linux and other Unix-like operating systems. The root user has unrestricted access to all commands, files, and resources, making it crucial to use this account cautiously and primarily for system administration tasks.

### 4.1 Adding a New User

1.  **Log in as Root via SSH.**
2.  **Add a New User:** Use the `adduser` command to create a new user. Replace `your_username` with your desired username:

    ```bash
    adduser your_username
    ```
3.  **Set Password:** You will be prompted to set a password for the new user. Enter and confirm a strong password.
4.  **User Information (Optional):** You will be asked for some user information like full name, room number, etc. You can press Enter to skip these fields if you wish.
5.  **Confirm Information:** Confirm the information is correct by typing `y` and pressing Enter.

### 4.2 Adding User to the `sudo` Group

To grant the new user administrative privileges, add them to the `sudo` group.

> **sudo (Superuser Do):** A command-line utility that allows permitted users to execute commands with the security privileges of another user, typically the root user. It is used to perform administrative tasks that require elevated permissions.

1.  **Add User to `sudo` Group:** Use the `usermod` command:

    ```bash
    usermod -aG sudo your_username
    ```

    This command adds the user `your_username` to the `sudo` group.

### 4.3 SSH Key Setup for the New User

You need to add your public SSH key to the new user's account to enable SSH key-based login for this user.

1.  **Switch to the New User's Home Directory:**

    ```bash
    cd /home/your_username
    ```
2.  **Create `.ssh` Directory:** If it doesn't exist, create the `.ssh` directory:

    ```bash
    mkdir .ssh
    ```
3.  **Navigate to `.ssh` Directory:**

    ```bash
    cd .ssh
    ```
4.  **Create `authorized_keys` File:** Create an empty file named `authorized_keys`:

    ```bash
    touch authorized_keys
    ```
5.  **Edit `authorized_keys` File:** Open the file with Nano:

    ```bash
    nano authorized_keys
    ```
6.  **Paste Public Key:** Paste your public SSH key (the same one you used for the root user, or a different one if you prefer) into this file.
7.  **Save and Close:** Save the file (Ctrl+X, then Y, then Enter in Nano).
8.  **Set Permissions:** Ensure correct permissions:

    ```bash
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
    ```

### 4.4 Logging in as the New User

Now you can log out of the root user session (type `logout` or `exit`) and attempt to log in as the new user using SSH.

1.  **Open a Terminal on your Local Machine.**
2.  **Connect via SSH:** Use the following command, replacing `your_username` with the username you created and `YOUR_SERVER_IP` with your server's IP address:

    ```bash
    ssh your_username@YOUR_SERVER_IP
    ```

    You should now be logged in as the new user using SSH key authentication. You can verify your current user by running the command `whoami`.

## 5. Transferring Application Files with Git

Git is a version control system that provides an efficient and secure way to transfer your application files to the server.

> **Git:** A distributed version control system that tracks changes in computer files and coordinates work on those files among multiple people. It is primarily used for source code management in software development.

### 5.1 Installing Git on the Server

If Git is not already installed on your server, install it using `apt`:

```bash
sudo apt install git
```

### 5.2 Cloning Your Application Repository

1.  **Navigate to the Desired Directory:** Decide where you want to store your application files on the server. A common practice is to create a `sites` directory in your home directory.

    ```bash
    mkdir sites
    cd sites
    ```
2.  **Clone the Repository:** Use `git clone` to clone your application's Git repository to the server. Replace `YOUR_REPOSITORY_URL` with the URL of your Git repository (e.g., from GitHub, GitLab, or Bitbucket).

    ```bash
    git clone YOUR_REPOSITORY_URL
    ```

    For example, to clone the "mern-tutorial" repository:

    ```bash
    git clone https://github.com/bradtraversy/mern-tutorial.git
    ```
3.  **Navigate to Application Directory:** Change directory into the newly cloned repository:

    ```bash
    cd mern-tutorial
    ```

## 6. Setting up a MongoDB Database with MongoDB Atlas

For MERN stack applications, a MongoDB database is required. MongoDB Atlas is a cloud-based database service that provides a convenient way to set up and manage MongoDB databases.

> **MongoDB:** A popular NoSQL document database program. It is designed for scalability and flexibility and is often used in web applications and other modern data-intensive applications.

> **MongoDB Atlas:** A fully managed cloud database service provided by MongoDB. It simplifies the deployment, operation, and scaling of MongoDB databases in the cloud.

### 6.1 Creating a MongoDB Atlas Account and Project

1.  **Go to MongoDB Atlas Website:** Navigate to the MongoDB Atlas website ([https://www.mongodb.com/atlas](https://www.mongodb.com/atlas)) and create an account or log in if you already have one.
2.  **Create a New Project:** After logging in, you will be prompted to create a new project. Follow the on-screen instructions to create a project.
3.  **Build a Database:** Within your project, click the "Build a Database" button.
4.  **Choose Shared (Free) Tier:** Select the "Shared" option (Free Tier) for demonstration purposes. This is suitable for development and learning.
5.  **Configure Database Settings:** Choose a cloud provider (AWS is common), region, and cluster tier. You can leave most settings at their defaults for a basic setup.
6.  **Cluster Name:** Give your cluster a name (e.g., "Cluster0").
7.  **Create Cluster:** Click "Create Cluster". Atlas will begin provisioning your MongoDB cluster, which may take a few minutes.

### 6.2 Configuring Database Access

1.  **Database Access:** Once the cluster is provisioned, navigate to the "Database Access" section in your Atlas project.
2.  **Add a New Database User:** Click "Add New Database User".
3.  **Username and Password:** Enter a username and password for your database user. Make sure to use strong credentials.
4.  **User Privileges:** For simplicity, you can grant the user "Read and write to any database" privileges for this tutorial.
5.  **Add User:** Click "Add User".
6.  **Network Access:** Navigate to the "Network Access" section.
7.  **Add IP Address:** Click "Add IP Address".
8.  **Whitelist Server IP:** Choose "Add Current IP Address" if you are configuring from your local machine. **Crucially, to allow your server to connect, you must add the public IP address of your Lenode server.** You can find your server's IP address in the Lenode dashboard. Click "Confirm".
9.  **Finish and Close:** Click "Finish and Close" and then "Go to Databases".

### 6.3 Getting the Connection String

1.  **Navigate to Databases:** In your Atlas project, go to the "Databases" section.
2.  **Connect:** Click the "Connect" button for your cluster.
3.  **Choose Connection Method:** Select "Connect your application".
4.  **Copy Connection String:** Choose the "Connection String only" option and copy the provided connection string. It will look something like:

    ```
    mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/?retryWrites=true&w=majority
    ```
5.  **Modify Connection String:**
    *   Replace `<username>` with the username you created in Database Access.
    *   Replace `<password>` with the password for that user.
    *   After the cluster name and before `?retryWrites`, you can optionally add the database name if you want to connect to a specific database upon initial connection. For instance, if your database is named "goalsetter", append `/goalsetter` after `.net/`.

## 7. Installing Node.js and Application Dependencies

Node.js is the runtime environment for your backend server in a MERN stack application. You need to install Node.js and then install the application's dependencies using npm (Node Package Manager).

> **Node.js:** An open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside of a web browser. It is commonly used to build server-side and networking applications.

> **npm (Node Package Manager):** The default package manager for Node.js. It is used to install, manage, and share JavaScript packages and modules.

### 7.1 Installing Node.js and npm

1.  **Install `curl` (if not already installed):** `sudo apt install curl`
2.  **Add NodeSource Repository:** Use `curl` to add the NodeSource repository for Node.js v18 (or your desired version):

    ```bash
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
    ```
3.  **Install Node.js:** Install Node.js and npm using `apt`:

    ```bash
    sudo apt install -y nodejs
    ```
4.  **Verify Installation:** Check the installed versions of Node.js and npm:

    ```bash
    node -v
    npm -v
    ```

### 7.2 Installing Backend Dependencies

1.  **Navigate to Backend Directory:** Change directory to the root of your application repository (where your `package.json` file for the backend is located). In the "mern-tutorial" example, this is the root directory of the cloned repository.
2.  **Install Dependencies:** Run `npm install` to install all the backend dependencies listed in `package.json`:

    ```bash
    npm install
    ```

### 7.3 Installing Frontend Dependencies and Building the Frontend

1.  **Navigate to Frontend Directory:** Change directory to the frontend directory of your application:

    ```bash
    cd frontend
    ```
2.  **Install Frontend Dependencies:** Run `npm install` to install frontend dependencies:

    ```bash
    npm install
    ```
3.  **Build the Frontend:** Build the React frontend application for production:

    ```bash
    npm run build
    ```

    This command compiles your React application and creates a `build` directory containing static assets ready for production deployment.

### 7.4 Configuring Environment Variables

Your application likely uses environment variables to store sensitive information like database connection strings.

1.  **Rename `.env.example` to `.env`:** In the root directory of your application, rename the `.env.example` file (if it exists) to `.env`:

    ```bash
    mv .env.example .env
    ```
2.  **Edit `.env` File:** Open the `.env` file using a text editor:

    ```bash
    sudo nano .env
    ```
3.  **Set Environment Variables:** Add or modify the environment variables in this file. **Crucially, set your MongoDB connection URI.**  For example:

    ```
    NODE_ENV=production
    MONGO_URI=mongodb+srv://your_atlas_connection_string
    PORT=5000
    ```

    Replace `mongodb+srv://your_atlas_connection_string` with the connection string you obtained from MongoDB Atlas, including your username, password, and database name.

    Set `NODE_ENV=production` to ensure your application runs in production mode. You can also specify the port your backend server will listen on (e.g., `PORT=5000`).

4.  **Save and Close:** Save the `.env` file (Ctrl+X, then Y, then Enter in Nano).

## 8. Using PM2 Process Manager to Run the Node.js Application

PM2 is a process manager for Node.js applications that keeps your application running reliably, even after crashes or server reboots.

> **PM2 (Process Manager 2):** A production process manager for Node.js applications. It allows you to daemonize applications, manage processes, monitor performance, and ensure high availability and resilience for your Node.js applications.

### 8.1 Installing PM2 Globally

Install PM2 globally using npm:

```bash
sudo npm install -g pm2
```

### 8.2 Starting the Application with PM2

1.  **Navigate to Application Root Directory:** Ensure you are in the root directory of your application (where `backend/server.js` or your main server file is located).
2.  **Start Application with PM2:** Use the `pm2 start` command to start your Node.js application. Specify the entry point to your backend server file (e.g., `backend/server.js`):

    ```bash
    pm2 start backend/server.js --name your-app-name
    ```

    Replace `your-app-name` with a descriptive name for your application process in PM2 (e.g., "mern-app-backend").

3.  **Verify Application Status:** Check the status of your application using `pm2 status` or `pm2 list`. You should see your application listed with a status of "online".
4.  **Access Application (Initially on Port 5000):** Your application is now running and should be accessible on the port specified in your `.env` file (e.g., port 5000). You can access it in a web browser using your server's IP address and the port number: `http://YOUR_SERVER_IP:5000`.

### 8.3 PM2 Management Commands

Here are some useful PM2 commands:

*   `pm2 stop your-app-name`: Stops the application process named "your-app-name".
*   `pm2 restart your-app-name`: Restarts the application process.
*   `pm2 delete your-app-name`: Deletes the application process from PM2's process list.
*   `pm2 logs your-app-name`: Shows logs for the application.
*   `pm2 monit`: Opens a monitoring dashboard in the terminal.
*   `pm2 startup systemd`: Generates and configures a startup script for PM2 to automatically start your applications on server reboot. Follow the instructions output by this command to complete the setup.
*   `pm2 save`: Saves the current PM2 process list so that applications are automatically restarted after a server reboot. Run this after starting your application with PM2.

## 9. Configuring a Firewall (UFW) for Security

A firewall is essential to secure your server by controlling network traffic and blocking unauthorized access. Ubuntu comes with UFW (Uncomplicated Firewall) which is easy to configure.

> **Firewall:** A network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It acts as a barrier between a trusted internal network and an untrusted external network, such as the Internet.

> **UFW (Uncomplicated Firewall):** A user-friendly frontend for `iptables`, a powerful command-line firewall utility in Linux. UFW simplifies the process of configuring and managing firewall rules.

### 9.1 Enabling UFW

1.  **Enable UFW:** Enable the firewall:

    ```bash
    sudo ufw enable
    ```

    You might get a warning about SSH connections being broken. Since we are already connected via SSH, we can proceed. Type `y` and press Enter.

### 9.2 Allowing Essential Ports

By default, UFW blocks all incoming traffic. You need to allow traffic on the ports required for your application and SSH access.

1.  **Allow SSH Port (Port 22):** Allow incoming SSH connections (port 22):

    ```bash
    sudo ufw allow ssh
    ```
2.  **Allow HTTP Port (Port 80):** Allow incoming HTTP traffic (port 80):

    ```bash
    sudo ufw allow http
    ```
3.  **Allow HTTPS Port (Port 443):** Allow incoming HTTPS traffic (port 443):

    ```bash
    sudo ufw allow https
    ```
4.  **Allow Application Port (Port 5000, if needed temporarily):** If you need to access your application directly on port 5000 temporarily before setting up Nginx, allow this port:

    ```bash
    sudo ufw allow 5000
    ```
    **Note:** After setting up Nginx, you will typically access your application through port 80, and you can remove this rule if desired: `sudo ufw delete allow 5000`.

### 9.3 Checking UFW Status

Verify the UFW status and the allowed rules:

```bash
sudo ufw status
```

You should see that UFW is active and rules are set for SSH, HTTP, and HTTPS (and optionally port 5000 if you added it).

## 10. Setting up Nginx as a Reverse Proxy

Nginx is a high-performance web server and reverse proxy server. We will configure Nginx to act as a reverse proxy, forwarding requests from port 80 (HTTP) to your Node.js application running on port 5000. This allows users to access your application using standard HTTP port without needing to specify port 5000 in the URL.

> **Nginx (Engine X):** A popular open-source web server, reverse proxy, load balancer, HTTP cache, and media streamer. It is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

> **Reverse Proxy:** A server that sits in front of backend servers and forwards client requests to those backend servers. Reverse proxies can provide benefits such as load balancing, security, SSL termination, and caching.

### 10.1 Installing Nginx

Install Nginx using `apt`:

```bash
sudo apt install nginx
```

### 10.2 Configuring Nginx for Reverse Proxy

1.  **Edit Nginx Configuration File:** Open the default Nginx server block configuration file:

    ```bash
    sudo nano /etc/nginx/sites-available/default
    ```
2.  **Modify Server Block:** Inside the `server` block, locate the `location /` block. Replace the contents of the `location /` block with the following configuration to set up a reverse proxy to your Node.js application running on `localhost:5000`:

    ```nginx
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
    ```

    Optionally, you can also configure the `server_name` directive within the `server` block to match your domain name if you have one. For example:

    ```nginx
    server {
        listen 80;
        server_name yourdomain.com www.yourdomain.com; # Replace with your domain

        location / {
            proxy_pass http://localhost:5000;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
    ```

    Replace `yourdomain.com` and `www.yourdomain.com` with your actual domain name.

3.  **Save and Close:** Save the file (Ctrl+X, then Y, then Enter in Nano).
4.  **Test Nginx Configuration:** Test the Nginx configuration for syntax errors:

    ```bash
    sudo nginx -t
    ```

    If the configuration is okay, you will see a message like: `nginx: configuration file /etc/nginx/nginx.conf test is successful`.
5.  **Restart Nginx:** Restart the Nginx service to apply the changes:

    ```bash
    sudo systemctl restart nginx
    ```

### 10.3 Accessing Application via Port 80

Now, you should be able to access your application in a web browser using just your server's IP address (or domain name if configured), without specifying port 5000. Nginx will forward requests to your Node.js application running in the background.

`http://YOUR_SERVER_IP` or `http://yourdomain.com`

## 11. (Optional) Domain Name Configuration

To make your application easily accessible with a domain name instead of an IP address, you need to configure your domain registrar and Lenode DNS (or your DNS provider).

### 11.1 Configuring Domain Registrar

1.  **Access Domain Registrar:** Log in to your domain registrar account (e.g., Namecheap, GoDaddy, etc.) where you registered your domain name.
2.  **Manage DNS Settings:** Find the DNS management settings for your domain.
3.  **Update Name Servers:** Update the name servers for your domain to point to Lenode's name servers. Lenode provides name servers like `ns1.lenode.com`, `ns2.lenode.com`, `ns3.lenode.com`, `ns4.lenode.com`, `ns5.lenode.com`. The exact name servers may be found in your Lenode dashboard under "DNS" or "Domains".
4.  **Save Changes:** Save the changes in your domain registrar's settings. DNS propagation may take some time (up to 48 hours) for the changes to fully take effect across the internet.

### 11.2 Configuring Lenode DNS (or your DNS Provider)

1.  **Access Lenode DNS Manager:** In your Lenode dashboard, navigate to the "DNS" or "Domains" section.
2.  **Create a Domain Zone:** If you haven't already, create a new domain zone for your domain name.
3.  **Add A Records:** Add "A" records to point your domain and `www` subdomain to your server's IP address.
    *   **Record Type:** A (Address)
    *   **Hostname:** `@` (for your domain root, e.g., `yourdomain.com`)
    *   **IP Address:** Your server's IP address
    *   **TTL:** (Default is usually fine)
    *   **Record Type:** A (Address)
    *   **Hostname:** `www` (for `www.yourdomain.com`)
    *   **IP Address:** Your server's IP address
    *   **TTL:** (Default is usually fine)
4.  **Save Changes:** Save the DNS records in Lenode's DNS manager.

After DNS propagation is complete, your application should be accessible via your domain name (e.g., `http://yourdomain.com`).

## 12. (Optional) Setting up SSL/HTTPS with Let's Encrypt

To secure your application with HTTPS, you can obtain a free SSL certificate from Let's Encrypt and configure Nginx to use it.

> **SSL/HTTPS (Secure Sockets Layer/Hypertext Transfer Protocol Secure):** A protocol that provides encrypted communication over the Internet. HTTPS uses SSL/TLS to encrypt HTTP requests and responses, protecting data in transit and ensuring secure communication between a web browser and a web server.

> **Let's Encrypt:** A free, automated, and open certificate authority (CA) that provides SSL/TLS certificates for enabling HTTPS on websites.

### 12.1 Installing Certbot

Certbot is a free, open-source software tool for automatically using Let's Encrypt certificates on manually-administered websites to enable HTTPS.

```bash
sudo apt install certbot python3-certbot-nginx
```

### 12.2 Obtaining SSL Certificate

Run Certbot to obtain and install an SSL certificate for your domain, automatically configuring Nginx:

```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

Replace `yourdomain.com` and `www.yourdomain.com` with your actual domain name. Follow the prompts from Certbot to complete the process, including agreeing to terms of service and providing an email address.

Certbot will automatically modify your Nginx configuration to use the SSL certificate.

### 12.3 Verifying HTTPS

After Certbot completes successfully, your application should now be accessible via HTTPS. Try accessing your application using `https://yourdomain.com` in your web browser. You should see a secure connection indicator (e.g., a padlock icon) in your browser's address bar.

## Conclusion

Congratulations! You have successfully set up a Linux server, deployed a MERN stack application, configured essential security measures, and made your application accessible via a domain name and HTTPS. This comprehensive guide provides a solid foundation for understanding server setup and deployment processes. While this setup is a starting point, further exploration into areas like automated deployment, containerization (Docker), and orchestration (Kubernetes) can enhance your deployment workflow and scalability as your application grows.
