---
layout: "../../layouts/BlogPost.astro"
title: "Deploying Django Projects on Digital Ocean: A Comprehensive Guide"
pubDate: "2025-03-02 14:19:34.873038"
youtubeVideoID: "Td3lirXIeRI"
index:
---

# Deploying Django Projects on Digital Ocean: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/Td3lirXIeRI" frameborder="0" allowfullscreen></iframe>

This chapter provides a step-by-step guide to deploying Django projects on a Digital Ocean server. While the examples primarily focus on Django, the fundamental principles and techniques discussed can be adapted for deploying other types of web applications and frameworks. We will cover essential technologies and processes involved in setting up a production-ready server environment.

## 1. Introduction to Deployment

Deployment is the process of making a web application accessible to users over the internet. This typically involves setting up a server, configuring the necessary software, and transferring your application's code to that server.  This guide will walk you through these steps using Digital Ocean, a popular cloud hosting provider, and focusing on best practices for stability, security, and performance.

We will utilize a range of technologies throughout this deployment process, including:

*   **Digital Ocean:** A cloud infrastructure provider that offers virtual servers (Droplets) for hosting applications.
*   **Ubuntu 22.04 LTS:** A popular and stable Linux distribution that will serve as the operating system for our server.
*   **Nginx:** A high-performance web server that will handle incoming requests and serve static files.
*   **Gunicorn:** A Python WSGI HTTP server that will serve our Django application.
*   **PostgreSQL:** A robust and feature-rich open-source relational database system for storing application data.
*   **Supervisor:** A process control system that ensures our Django application (via Gunicorn) runs reliably and restarts automatically if it crashes.
*   **Let's Encrypt:** A free, automated, and open certificate authority that provides SSL certificates for enabling HTTPS.
*   **Git & GitHub:** Version control and code hosting platform for managing and transferring our application code.

## 2. Setting Up Your Digital Ocean Account and Creating a Droplet

### 2.1. Creating a Digital Ocean Account

If you don't already have a Digital Ocean account, you'll need to create one.

*   Visit [digitalocean.com](https://digitalocean.com) and sign up. New users often receive promotional credits for initial server usage (check the video description for potential referral links with credits).
*   Once signed up, log in to your Digital Ocean account.

### 2.2. Creating a Droplet (Virtual Server)

A **Droplet** in Digital Ocean terminology is a virtual private server (VPS). It's your isolated server instance in the cloud where you'll deploy your application.

> **Droplet:** A virtual private server (VPS) offered by Digital Ocean. It provides a virtualized computing environment where users can install and run operating systems and applications.

To create a Droplet:

1.  Click the **Create** button in the Digital Ocean dashboard and select **Droplets**.
2.  **Choose a Region:** Select a data center region geographically closest to your target users. For example, if your users are primarily in Europe, Frankfurt or Amsterdam might be suitable choices.
3.  **Choose an Operating System:** Under the **OS** tab, select **Ubuntu**. For this guide, choose version **22.04 LTS**.

    > **LTS (Long-Term Support):** A designation for software releases that are supported for an extended period, typically five years for Ubuntu LTS versions. This ensures stability and security updates for a longer duration.

4.  **Choose a Plan (Size):** Select a server size. For initial deployments and learning purposes, the **Basic** plan is usually sufficient. You can scale up later if needed. Consider the resources (CPU, RAM, SSD) offered at different price points.
5.  **Choose Authentication Method:**
    *   **Password (Simpler for beginners):**  Select the "Password" tab and enter a strong password. **Important:** Store this password securely.
    *   **SSH Keys (More Secure):**  For enhanced security, consider using SSH keys. This method involves generating a key pair and uploading the public key to Digital Ocean.

    > **SSH Keys:** A more secure method of authenticating to a server compared to passwords. It uses cryptographic key pairs (public and private) for verification.

6.  **Choose a Hostname:**  Give your Droplet a descriptive hostname. This is for your internal management and can help identify the server easily. A hostname like `ubuntu-1vcpu-2gb-fra1` (indicating Ubuntu, 1 vCPU, 2GB RAM, Frankfurt region 1) can be informative.
7.  Click **Create Droplet**.

Digital Ocean will now provision your server. This process usually takes a few minutes. Once completed, you'll see your Droplet listed in your dashboard with its public IP address.

## 3. Initial Server Setup and Software Installation

### 3.1. Connecting to Your Server via SSH

To manage your server, you'll connect to it using **SSH (Secure Shell)**.

> **SSH (Secure Shell):** A cryptographic network protocol that allows secure communication, especially for remote command-line login and command execution.

1.  **Obtain Droplet IP Address:** Copy the IP address of your newly created Droplet from the Digital Ocean dashboard.
2.  **Open a Terminal:**
    *   **macOS/Linux:** Open the built-in Terminal application or a terminal emulator like iTerm2.
    *   **Windows:** Use PuTTY or the built-in Windows Subsystem for Linux (WSL) terminal.
3.  **Connect using SSH:**  In your terminal, type the following command, replacing `your_droplet_ip` with your Droplet's IP address:

    ```bash
    ssh root@your_droplet_ip
    ```

    *   If you used a password, you'll be prompted to enter it.
    *   If you used SSH keys, your SSH client will use your private key for authentication.

    You might be asked to confirm adding the server's fingerprint to your known hosts file. Type `yes` and press Enter.

### 3.2. Updating the Server

It's crucial to update the server's package lists and upgrade existing packages to ensure you have the latest security patches and software versions.

1.  **Update Package Lists:** Run the following command:

    ```bash
    sudo apt update
    ```

    > **sudo:** A command that allows permitted users to execute commands as a superuser or another user, as defined by the security policy. It's often used to perform administrative tasks.

    > **apt (Advanced Package Tool):** A package management tool used in Debian-based Linux distributions like Ubuntu for installing, updating, and removing software packages.

    This command refreshes the package lists, ensuring your system knows about the latest available software versions.

2.  **Upgrade Packages:** Run the following command to upgrade all outdated packages:

    ```bash
    sudo apt upgrade
    ```

    Confirm the upgrade by typing `Y` when prompted and pressing Enter. This process might take some time depending on the number of updates.

    During the upgrade, you might be prompted to make decisions about configuration files. In most cases, choosing to "keep the local version" is acceptable for initial setup.

### 3.3. Installing Essential Software

We need to install several software packages that are essential for deploying our Django application: Python, pip, PostgreSQL, Nginx, Certbot, and Supervisor.

Run the following command to install these packages:

```bash
sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx certbot python3-certbot-nginx supervisor
```

Let's break down what each package is:

*   `python3-pip`: Installs **pip**, the package installer for Python.

    > **pip (Pip Installs Packages):** A package management system used to install and manage software packages written in Python.

*   `python3-dev`: Includes header files and libraries needed for compiling Python extensions, which are often required by Python packages that interact with system-level libraries (like `psycopg2` for PostgreSQL).
*   `libpq-dev`: Development headers and libraries for **libpq**, the PostgreSQL client library, necessary for compiling Python PostgreSQL adapters.
*   `postgresql` and `postgresql-contrib`: Install the PostgreSQL database server and additional utilities.
*   `nginx`: Installs the Nginx web server.

    > **Nginx (engine x):** A high-performance web server and reverse proxy server known for its efficiency and scalability. We'll use it to serve static files and proxy requests to Gunicorn.

*   `certbot` and `python3-certbot-nginx`: Install **Certbot**, a tool for obtaining free SSL certificates from Let's Encrypt, and its Nginx plugin.

    > **Certbot:** A free, open-source software tool for automatically using Let's Encrypt certificates to enable HTTPS on websites.

*   `supervisor`: Installs **Supervisor**, a process control system.

    > **Supervisor:** A process control system for Unix-like operating systems. It allows you to monitor and control processes, ensuring they run reliably and restart automatically if they fail.

Confirm the installation by typing `Y` when prompted and pressing Enter.

## 4. Setting Up PostgreSQL Database

PostgreSQL will be our database system. We need to create a database and a user specifically for our Django project.

### 4.1. Accessing PostgreSQL Command Line

PostgreSQL creates a default user named `postgres`. We'll use this user initially to set up our database and user.

Run the following command to switch to the `postgres` user and access the PostgreSQL command-line interface (`psql`):

```bash
sudo -u postgres psql
```

### 4.2. Creating a Database

Inside the `psql` prompt, create a new database for your Django project. Let's name it `project1`.

```sql
CREATE DATABASE project1;
```

### 4.3. Creating a Database User

Create a dedicated user for accessing the `project1` database. Let's name this user `project1_user` and set a password (remember to choose a strong password for production environments; for this tutorial, a simple password like `project1_password` is used for demonstration).

```sql
CREATE USER project1_user WITH PASSWORD 'project1_password';
```

### 4.4. Configuring User Roles and Privileges

We need to configure some settings for the `project1_user` to ensure proper database operation and grant it necessary privileges.

1.  **Set Client Encoding to UTF8:**

    ```sql
    ALTER ROLE project1_user SET client_encoding TO 'utf8';
    ```

    This ensures that the database client communication uses UTF-8 encoding, which is essential for handling a wide range of characters.

2.  **Set Default Transaction Isolation Level:**

    ```sql
    ALTER ROLE project1_user SET default_transaction_isolation TO 'read committed';
    ```

    This sets the transaction isolation level to "read committed," a common and suitable level for most web applications. It ensures that transactions only see committed data, preventing dirty reads.

3.  **Set Default Time Zone to UTC:**

    ```sql
    ALTER ROLE project1_user SET timezone TO 'UTC';
    ```

    Setting the time zone to UTC (Coordinated Universal Time) is a best practice for server applications to avoid time zone-related issues.

4.  **Grant Database Privileges:**

    Grant all privileges on the `project1` database to the `project1_user`.

    ```sql
    GRANT ALL PRIVILEGES ON DATABASE project1 TO project1_user;
    ```

### 4.5. Exiting PostgreSQL Command Line

Type `\q` and press Enter to exit the `psql` prompt.

## 5. Setting Up Virtual Environments and User Accounts for Your Project

### 5.1. Creating Project Directory

We will create a dedicated directory to house our Django project files. A common location is within `/webapps`.

```bash
sudo mkdir /webapps
```

Navigate into this directory:

```bash
cd /webapps
```

Create a directory for your first project, `project1`:

```bash
sudo mkdir project1
```

Navigate into the project directory:

```bash
cd project1
```

### 5.2. Creating a Virtual Environment

It's best practice to isolate Python project dependencies within a **virtual environment**.

> **Virtual Environment:** A self-contained directory that isolates Python dependencies for a specific project. This prevents conflicts between different project requirements.

Create a virtual environment named `env` within the `project1` directory:

```bash
python3 -m venv env
```

### 5.3. Creating a System User Group

Create a system group named `webapps` to manage permissions for web applications.

```bash
sudo groupadd --system webapps
```

### 5.4. Creating a System User for the Project

Create a dedicated system user for your `project1` project. This user will own the project files and run the application.

```bash
sudo useradd -d /webapps/project1 -s /bin/bash -g webapps --system project1_user
```

Let's break down this command:

*   `sudo useradd`: Command to add a new user.
*   `-d /webapps/project1`: Sets the home directory for the user to `/webapps/project1`.
*   `-s /bin/bash`: Sets the default shell to Bash.
*   `-g webapps`: Adds the user to the `webapps` group.
*   `--system`: Creates a system user (typically used for services).
*   `project1_user`: The username for the new user.

## 6. Setting Up Requirements Files

A **requirements file** lists all the Python packages your project depends on. This ensures that the server environment has the necessary packages installed.

> **Requirements File (requirements.txt):** A text file that lists Python packages and their versions required for a project. It's used by `pip` to install all dependencies.

### 6.1. Creating `requirements.txt` Locally

On your local development machine, navigate to your Django project's root directory (where `manage.py` is located).

If you haven't already, generate a `requirements.txt` file using `pip freeze`:

```bash
pip freeze > requirements.txt
```

This command captures all currently installed packages in your local environment and saves them to `requirements.txt`.

### 6.2. Adding Necessary Packages to `requirements.txt`

Edit the `requirements.txt` file and add the following packages, ensuring specific versions if necessary for compatibility:

```txt
Django==your_django_version  # Replace with your Django version
gunicorn==21.2.0
psycopg2-binary==2.9.9
envparse==0.2.0
```

*   `gunicorn`: The Gunicorn WSGI server we'll use in production.
*   `psycopg2-binary`: A PostgreSQL adapter for Python (binary version for easier installation).
*   `envparse`: A library for parsing environment variables. We'll use this to manage sensitive settings like secret keys and database passwords in production.

## 7. Setting Up Production Settings File

We'll create a separate settings file specifically for the production environment. This allows us to have different configurations for development and production.

### 7.1. Creating `settings_prod.py`

In your Django project's settings directory (e.g., `project1/project1/`), create a new file named `settings_prod.py`.

Copy the contents of your main `settings.py` file (e.g., `project1/project1/settings.py`) into `settings_prod.py`.

### 7.2. Modifying `settings_prod.py` for Production

Make the following modifications in `settings_prod.py`:

1.  **Import `os` and `envparse`:**

    ```python
    import os
    from envparse import env

    env.read_envfile() # Optionally read from .env file
    ```

2.  **Secret Key from Environment Variable:**

    Replace the hardcoded `SECRET_KEY` with:

    ```python
    SECRET_KEY = env('SECRET_KEY', default='') # Get from environment variable or default to empty string
    ```

3.  **Debug Mode Disabled:**

    Set `DEBUG = False` for production.

4.  **Allowed Hosts:**

    Configure `ALLOWED_HOSTS` to include your domain name:

    ```python
    ALLOWED_HOSTS = ['project1.codewithstein.com'] # Replace with your domain
    ```

5.  **Database Configuration for PostgreSQL:**

    Modify the `DATABASES` setting to use PostgreSQL. Read database credentials from environment variables for security:

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'project1', # Database name
            'USER': 'project1_user', # Database user
            'PASSWORD': env('DB_PASSWORD', default=''), # Database password from environment variable
            'HOST': 'localhost',
            'PORT': '', # Default PostgreSQL port
        }
    }
    ```

## 8. Sending Code to GitHub

Using Git and GitHub is a recommended way to manage and transfer your code to the server.

### 8.1. Creating a GitHub Repository

1.  Go to [github.com](https://github.com) and log in to your account.
2.  Click the "+" button and select "New repository."
3.  Name your repository (e.g., `project1`).
4.  Choose "Public" or "Private" as desired.
5.  Initialize with a README file (optional).
6.  Click "Create repository."

### 8.2. Initializing Git Locally and Creating `.gitignore`

On your local machine, in your Django project's root directory:

1.  **Initialize Git:**

    ```bash
    git init
    ```

2.  **Create `.gitignore` file:**

    Create a file named `.gitignore` in your project's root and add the following entries to exclude unnecessary files from version control:

    ```gitignore
    *.pyc
    __pycache__/
    env/
    db.sqlite3
    *.sqlite3
    *.log
    *.DS_Store # macOS specific
    ```

3.  **Add and Commit Initial Code:**

    ```bash
    git add .
    git commit -m "Initial commit"
    ```

### 8.3. Linking Local Repository to GitHub and Pushing Code

1.  **Add Remote Origin:**

    Copy the repository URL from your GitHub repository page. Then, run:

    ```bash
    git remote add origin your_repository_url # Replace with your GitHub repository URL
    ```

2.  **Push Code to GitHub:**

    ```bash
    git push -u origin main
    ```

    You might be prompted for your GitHub username and a personal access token instead of your password (as password authentication is deprecated for Git operations). Generate a personal access token with `repo` scope in your GitHub settings (Settings -> Developer settings -> Personal access tokens -> Tokens (classic)).

## 9. Getting Code from GitHub to the Server

Now, we'll clone your GitHub repository onto your Digital Ocean server.

1.  **SSH into your server** (if you're not already connected).
2.  **Navigate to the project directory:**

    ```bash
    cd /webapps/project1
    ```

3.  **Clone the repository:**

    ```bash
    git clone your_repository_url . # Clone into the current directory (.)
    ```

    Replace `your_repository_url` with your GitHub repository URL.

## 10. Setting Up Environment Variables on the Server

We need to create a `.env` file on the server to store sensitive information like the `SECRET_KEY` and database password.

1.  **Create `.env` file:**

    ```bash
    vi .env
    ```

2.  **Add Environment Variables:**

    Press `i` to enter insert mode in `vi` and add the following lines, replacing placeholders with your actual secret key and database password:

    ```env
    SECRET_KEY=your_very_long_and_secure_secret_key
    DB_PASSWORD=project1_password
    ```

    Press `Esc` to exit insert mode, then type `:wq` and press Enter to save and quit `vi`.

## 11. Installing Requirements on the Server

Now, install the Python packages listed in `requirements.txt` within the virtual environment on the server.

1.  **Activate the virtual environment:**

    ```bash
    source env/bin/activate
    ```

    You should see `(env)` prepended to your terminal prompt, indicating the virtual environment is active.

2.  **Install requirements:**

    ```bash
    pip install -r requirements.txt
    ```

## 12. Initializing the Database (Migrations)

Run Django migrations to create the database schema in PostgreSQL.

```bash
python manage.py migrate --settings=project1.settings_prod
```

This command applies migrations defined in your Django apps to the PostgreSQL database, creating the necessary tables.

## 13. Configuring Gunicorn

Gunicorn will serve our Django application. We need to create a Gunicorn start script.

### 13.1. Creating `gunicorn_start` Script

1.  **Create the script file:**

    ```bash
    touch env/bin/gunicorn_start
    vi env/bin/gunicorn_start
    ```

2.  **Add Script Content:**

    Press `i` to enter insert mode and paste the following script into `gunicorn_start`:

    ```bash
    #!/bin/bash

    NAME="project1"                      # Name of the application
    DJANGO_DIR=/webapps/project1/project1   # Django project directory
    SOCKFILE=/webapps/project1/run/gunicorn.sock  # Socket file
    USER=project1_user                 # User to run as
    GROUP=webapps                      # Group to run as
    NUM_WORKERS=3                       # Number of worker processes
    DJANGO_SETTINGS_MODULE=project1.settings_prod # Django settings module
    DJANGO_WSGI_MODULE=project1.wsgi      # WSGI module name

    # Activate the virtual environment
    cd $DJANGO_DIR
    source ../env/bin/activate
    export DJANGO_SETTINGS_MODULE=$DJANGO_SETTINGS_MODULE
    export PYTHONPATH=$DJANGO_DIR:$PYTHONPATH

    # Create run directory if it doesn't exist
    RUNDIR=$(dirname $SOCKFILE)
    test -d $RUNDIR || mkdir -p  $RUNDIR

    # Start Gunicorn
    exec env/bin/gunicorn \
         --name $NAME \
         --workers $NUM_WORKERS \
         --user=$USER --group=$GROUP \
         --bind=unix:$SOCKFILE \
         --log-level=debug \
         --log-file=- \
         $DJANGO_WSGI_MODULE:application
    ```

    Press `Esc`, then `:wq` and Enter to save and quit.

3.  **Make the script executable:**

    ```bash
    chmod +x env/bin/gunicorn_start
    ```

### 13.2. Testing Gunicorn

Try running the Gunicorn script to ensure it starts correctly:

```bash
env/bin/gunicorn_start
```

If it starts without errors, press `Ctrl+C` to stop it.

### 13.3. Setting Ownership

Ensure the project files and directories are owned by the `project1_user`:

```bash
sudo chown -R project1_user:webapps /webapps/project1
```

## 14. Configuring Supervisor

Supervisor will manage our Gunicorn process, ensuring it runs continuously.

### 14.1. Creating Supervisor Configuration File

1.  **Create the configuration file:**

    ```bash
    sudo vi /etc/supervisor/conf.d/project1.conf
    ```

2.  **Add Configuration:**

    Press `i` to insert mode and add the following configuration:

    ```ini
    [program:project1]
    command=/webapps/project1/env/bin/gunicorn_start
    user=project1_user
    autostart=true
    autorestart=true
    redirect_stderr=true
    stdout_logfile=/webapps/project1/log/supervisor.log

    environment=LANG=en_US.UTF-8,LC_ALL=en_US.UTF-8
    ```

    Press `Esc`, then `:wq` and Enter to save and quit.

3.  **Create Log Directory:**

    ```bash
    sudo mkdir /webapps/project1/log
    sudo chown project1_user:webapps /webapps/project1/log
    ```

### 14.2. Rereading and Updating Supervisor

Tell Supervisor to reread its configuration and update the processes:

```bash
sudo supervisorctl reread
sudo supervisorctl update
```

### 14.3. Checking Supervisor Status

Verify that Supervisor is running your Gunicorn process:

```bash
sudo supervisorctl status project1
```

You should see the status as `RUNNING`.

## 15. Configuring Nginx

Nginx will act as a reverse proxy, handling incoming requests and forwarding them to Gunicorn. It will also serve static and media files.

### 15.1. Creating Nginx Configuration File

1.  **Navigate to Nginx sites-available directory:**

    ```bash
    cd /etc/nginx/sites-available/
    ```

2.  **Create configuration file:**

    ```bash
    sudo vi project1.conf
    ```

3.  **Add Nginx Configuration:**

    Press `i` to insert mode and add the following configuration, replacing `project1.codewithstein.com` with your actual domain name:

    ```nginx
    upstream project1_app_server {
        server unix:/webapps/project1/run/gunicorn.sock fail_timeout=0;
    }

    server {
        listen 80;
        server_name project1.codewithstein.com; # Replace with your domain

        access_log /webapps/project1/log/nginx_access.log;
        error_log /webapps/project1/log/nginx_error.log;

        location /static/ {
            alias /webapps/project1/project1/static/; # Adjust path if needed
        }

        location /media/ {
            alias /webapps/project1/project1/media/; # Adjust path if needed
        }

        location / {
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_pass http://project1_app_server;
        }
    }
    ```

    Press `Esc`, then `:wq` and Enter to save and quit.

4.  **Create Nginx Log Directory and Set Permissions:**

    ```bash
    sudo mkdir /webapps/project1/log
    sudo chown project1_user:webapps /webapps/project1/log
    ```

### 15.2. Enabling Nginx Site

1.  **Create a symbolic link:**

    ```bash
    sudo ln -s /etc/nginx/sites-available/project1.conf /etc/nginx/sites-enabled/
    ```

2.  **Remove default Nginx configuration (optional):**

    ```bash
    sudo rm /etc/nginx/sites-enabled/default
    ```

### 15.3. Testing Nginx Configuration and Restarting

1.  **Test Nginx configuration:**

    ```bash
    sudo nginx -t
    ```

    If the test is successful ("test is successful"), proceed.

2.  **Restart Nginx:**

    ```bash
    sudo systemctl restart nginx
    ```

Now, your Django application should be accessible in your web browser using your domain name (e.g., `http://project1.codewithstein.com`).

## 16. Setting Up SSL with Let's Encrypt (Certbot)

To enable HTTPS and secure your website, we'll use Let's Encrypt and Certbot.

1.  **Run Certbot for Nginx:**

    ```bash
    sudo certbot --nginx -d project1.codewithstein.com # Replace with your domain
    ```

    Certbot will automatically configure Nginx to use the SSL certificate. Follow the prompts, providing your email address and agreeing to the terms of service.

2.  **Automatic Nginx Configuration:**

    Certbot will modify your Nginx configuration file (`/etc/nginx/sites-available/project1.conf`) to include SSL settings and redirect HTTP traffic to HTTPS.

3.  **Verify HTTPS:**

    Open your website in a browser using `https://project1.codewithstein.com`. You should see a padlock icon in the address bar, indicating a secure HTTPS connection.

Congratulations! You have successfully deployed your Django project on a Digital Ocean server with Nginx, Gunicorn, PostgreSQL, Supervisor, and SSL using Let's Encrypt. You can now adapt these steps for deploying multiple Django projects on the same server by repeating the process for each project, ensuring unique database names, users, project directories, Gunicorn configurations, Supervisor configurations, and Nginx configurations. Remember to adjust domain names and project-specific settings accordingly.
