---
layout: "../../layouts/BlogPost.astro"
title: "Building a Desktop Application with Electron: A Step-by-Step Guide"
pubDate: "2025-03-01 14:14:56.603689"
youtubeVideoID: "ML743nrkMHw"
index:
---

# Building a Desktop Application with Electron: A Step-by-Step Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/ML743nrkMHw" frameborder="0" allowfullscreen></iframe>


This chapter will guide you through the process of creating a desktop application using Electron, a powerful framework for building cross-platform applications with web technologies. We will develop a simple image resizing application to illustrate key Electron concepts and functionalities. This project serves as an excellent starting point for understanding Electron and building more complex desktop applications.

## 1. Introduction to Electron

Electron is a versatile framework that allows developers to build desktop applications for Windows, macOS, and Linux using web technologies such as HTML, CSS, and JavaScript.  This means you can leverage your existing web development skills to create native desktop applications. Many popular applications are built using Electron, demonstrating its capabilities and widespread adoption. Examples include:

*   **VS Code:** A widely used source code editor.
*   **Atom:** Another popular, customizable text editor.
*   **Postman:** A tool for API development and testing.
*   **Slack:** A popular communication platform for teams.

> **Electron:** An open-source framework developed by GitHub for building cross-platform desktop applications with HTML, CSS, and JavaScript. It allows developers to use web technologies to create native-like applications that can run on Windows, macOS, and Linux.

Electron is a favorite technology for many developers due to its cross-platform nature and the accessibility of web development skills. This chapter will guide you through building a practical project to get hands-on experience with Electron.

## 2. Project Overview: Image Resizer Application

In this chapter, we will build an "Image Resizer" application. This application will allow users to:

*   Select an image file from their computer.
*   Specify desired width and height dimensions for the image.
*   Resize the image and save the resized version to a designated output folder.

This application offers simple yet fundamental functionality, making it an ideal project for beginners to grasp the core concepts of Electron development. It will cover essential aspects such as:

*   The **main process** and **renderer process** architecture in Electron.
*   Creating application menus.
*   Handling user input and events.
*   Inter-process communication (IPC).

> **Main Process:** In Electron, the main process acts as the application's entry point and manages the application lifecycle. It is responsible for creating and managing browser windows (renderer processes), handling system events, and interacting with the operating system.

> **Renderer Process:** Renderer processes are responsible for displaying the user interface of an Electron application. Each browser window in an Electron application runs in its own renderer process, which is essentially a Chromium instance rendering web content (HTML, CSS, and JavaScript).

## 3. Prerequisites

To follow along with this chapter, you will need:

*   **Basic JavaScript knowledge:**  A solid understanding of JavaScript is essential. Prior experience with Node.js is not strictly required for this project, although familiarity can be beneficial.
*   **Node.js and npm (Node Package Manager) installed:** Electron applications are built using Node.js, and npm is used to manage project dependencies. Ensure you have Node.js and npm installed on your system. You can download them from the official Node.js website.
*   **A code editor:**  VS Code is recommended, but you can use any code editor of your choice.

It is recommended to set aside some dedicated time to focus on learning and building this application alongside the instructions provided.

## 4. Setting Up the Project

Let's begin by setting up our project environment.

### 4.1. Creating the Project Folder

1.  Create a new, empty folder on your computer named `image-resizer-electron`.
2.  Open this folder in your code editor (e.g., VS Code).
3.  Open the integrated terminal within your code editor.

### 4.2. Initializing `package.json`

We need to initialize a `package.json` file, which is essential for Node.js projects to manage dependencies and project information.

1.  In the terminal, run the command: `npm init`
2.  You will be prompted to answer a series of questions. For this project, you can use the following:
    *   **package name:** `image-resizer-electron` (or as desired)
    *   **version:** `1.0.0` (or as desired)
    *   **description:** `App to resize image dimensions`
    *   **entry point:** `main.js` (Crucially, this file will be the entry point for the main process in Electron.)
    *   **author:** Your Name (or as desired)
    *   **license:** `MIT` (or as desired)
3.  Confirm the details by typing `yes` and pressing Enter.

This will generate a `package.json` file in your project directory.

### 4.3. Adding Product Name

Open the `package.json` file in your code editor. Add a `productName` property to the JSON object. This name will be displayed in the application menu, especially on macOS.

```json
{
  "name": "image-resizer-electron",
  "version": "1.0.0",
  "description": "App to resize image dimensions",
  "main": "main.js",
  "author": "Your Name",
  "license": "MIT",
  "productName": "Image Resizer"
}
```

### 4.4. Installing Dependencies

We need to install the necessary packages for our Electron application.

1.  In the terminal, run the following command to install Electron, `resize-img` (for image resizing functionality), and `toastify-js` (for user notifications):

    ```bash
    npm install electron resize-img toastify-js
    ```

    *   **electron:** The core Electron framework.
    *   **resize-img:** A Node.js package to handle image resizing.
    *   **toastify-js:** A JavaScript library to create toast notifications for user feedback.

After installation, you will find these packages listed under `dependencies` in your `package.json` file.

## 5. Structuring the Application: Main and Renderer Processes

Electron applications typically consist of two main processes: the main process and the renderer process.

*   **Main Process (main.js):**  This is the backend of your application. It manages the application lifecycle, creates windows, handles system events, and performs backend tasks like image resizing in our case.
*   **Renderer Process (renderer/index.html, renderer/renderer.js):** This is the frontend of your application, responsible for the user interface. It displays web pages and interacts with the user.

### 5.1. Creating `main.js` (Main Process)

1.  Create a new file named `main.js` in the root of your project directory.
2.  For now, let's add a simple `console.log` to verify it's running:

    ```javascript
    // main.js
    console.log("Hello from the main process!");
    ```

### 5.2. Modifying `package.json` for the Start Script

We need to configure the `start` script in `package.json` to launch our Electron application.

1.  Open `package.json`.
2.  Modify the `scripts` section to include a `start` script that uses Electron to run `main.js`:

    ```json
    "scripts": {
      "start": "electron ."
    },
    ```

    This script will execute Electron, using the current directory (`.`) as the path to your application, which will run `main.js` by default as specified in the `main` property.

### 5.3. Running the Application for the First Time

1.  In the terminal, run the command: `npm start`

    This command executes the `start` script we just defined. You should see "Hello from the main process!" logged in your terminal. This confirms that Electron is running and executing your `main.js` file as a Node.js process. To stop the running process, press `Ctrl+C` (or `Cmd+C` on macOS) in the terminal.

## 6. Creating the Main Window

Now let's create the main application window, which will be the user interface of our Image Resizer.

### 6.1. Importing Modules in `main.js`

1.  Open `main.js`.
2.  Import the `app` and `BrowserWindow` modules from Electron. We also need the `path` module for handling file paths.

    ```javascript
    // main.js
    const { app, BrowserWindow } = require('electron');
    const path = require('path');
    ```

    > **require():** In Node.js and Electron's main process, `require()` is a function used to import modules. It allows you to load and use external libraries, built-in modules, or other JavaScript files within your application.

### 6.2. Creating the `createMainWindow` Function

Create a function named `createMainWindow` that will handle the creation of the main application window.

```javascript
// main.js
const { app, BrowserWindow } = require('electron');
const path = require('path');

let mainWindow; // Declare mainWindow in the global scope

function createMainWindow() {
  mainWindow = new BrowserWindow({
    title: 'Image Resizer',
    width: 500,
    height: 600,
  });

  mainWindow.loadFile(path.join(__dirname, 'renderer', 'index.html'));
}
```

*   **`new BrowserWindow(options)`:**  This creates a new application window. The `options` object allows you to configure various window properties like title, width, height, etc.
*   **`mainWindow.loadFile(filePath)`:** This method loads an HTML file into the browser window. `path.join(__dirname, 'renderer', 'index.html')` constructs the absolute path to your `index.html` file located in the `renderer` folder. `__dirname` refers to the directory where `main.js` is located.

### 6.3. Creating `renderer/index.html` (Renderer Process UI)

1.  Create a new folder named `renderer` in the root of your project directory.
2.  Inside the `renderer` folder, create a new file named `index.html`.
3.  Add basic HTML boilerplate code to `index.html`:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title>Image Resizer</title>
    </head>
    <body>
        <h1>Hello World from Renderer Process!</h1>
    </body>
    </html>
    ```

### 6.4. Calling `createMainWindow` when the App is Ready

We need to call `createMainWindow` function when Electron is ready to launch the application.

1.  In `main.js`, add the following code to call `createMainWindow` when the `app` emits the `ready` event:

    ```javascript
    // main.js
    const { app, BrowserWindow } = require('electron');
    const path = require('path');

    let mainWindow;

    function createMainWindow() {
      mainWindow = new BrowserWindow({
        title: 'Image Resizer',
        width: 500,
        height: 600,
      });

      mainWindow.loadFile(path.join(__dirname, 'renderer', 'index.html'));
    }

    app.whenReady().then(createMainWindow);
    ```

    *   **`app.whenReady().then(callback)`:** This ensures that `createMainWindow` is executed only after Electron has fully initialized and is ready to create windows.

### 6.5. Running the Application with the Main Window

1.  Run `npm start` in the terminal.

    You should now see a desktop window titled "Image Resizer" displaying "Hello World from Renderer Process!". This confirms that your main window is successfully created and loading the `index.html` file.

## 7. Boilerplate Code for Application Lifecycle

Electron applications require some standard boilerplate code to handle application lifecycle events correctly, especially across different operating systems (Windows, macOS).

### 7.1. Handling Window Closure (macOS vs. Windows/Linux)

macOS handles window closing differently than Windows and Linux. On macOS, closing all windows typically does not quit the application; it remains running in the background. On Windows and Linux, closing the last window usually quits the application. We need to replicate these platform-specific behaviors.

1.  In `main.js`, add the following event listeners to the `app` object:

    ```javascript
    // main.js
    const { app, BrowserWindow } = require('electron');
    const path = require('path');

    let mainWindow;
    const isMac = process.platform === 'darwin'; // Check if platform is macOS

    function createMainWindow() {
      // ... (rest of createMainWindow function)
    }

    app.whenReady().then(createMainWindow);

    app.on('window-all-closed', () => {
      if (!isMac) { // Quit app only if not on macOS
        app.quit();
      }
    });

    app.on('activate', () => {
      if (BrowserWindow.getAllWindows().length === 0) {
        createMainWindow(); // Re-create main window if none exist when activated (macOS dock icon click)
      }
    });
    ```

    *   **`process.platform === 'darwin'`:** This checks if the operating system is macOS (Darwin kernel).
    *   **`app.on('window-all-closed', callback)`:** This event is emitted when all application windows are closed.
    *   **`app.quit()`:**  This method quits the entire Electron application.
    *   **`app.on('activate', callback)`:** On macOS, this event is emitted when the application is activated, often by clicking the dock icon. We check if any windows are open and, if not, re-create the main window.

### 7.2. Declaring `isMac` Variable

To simplify platform checks throughout the code, let's declare a variable `isMac` at the top of `main.js`:

```javascript
// main.js
const { app, BrowserWindow } = require('electron');
const path = require('path');

const isMac = process.platform === 'darwin'; // Variable to check if platform is macOS
let mainWindow;

// ... (rest of main.js code)
```

## 8. Development Enhancements: DevTools and Live Reloading

For a smoother development experience, we can enable DevTools to debug our renderer process and use a tool for live reloading to automatically restart the application on code changes.

### 8.1. Opening DevTools in Development Mode

Chromium DevTools is a powerful debugging tool for web technologies. We can automatically open DevTools when the application starts in development mode.

1.  In `main.js`, add the following code inside the `createMainWindow` function, after loading the file:

    ```javascript
    // main.js
    function createMainWindow() {
      mainWindow = new BrowserWindow({
        title: 'Image Resizer',
        width: 500,
        height: 600,
      });

      mainWindow.loadFile(path.join(__dirname, 'renderer', 'index.html'));

      // Open DevTools if in development mode
      if (process.env.NODE_ENV !== 'production') {
        mainWindow.webContents.openDevTools();
      }
    }
    ```

    *   **`process.env.NODE_ENV !== 'production'`:** This checks if the `NODE_ENV` environment variable is not set to 'production'. By default, when you run `npm start`, `NODE_ENV` is typically not set, effectively putting you in development mode.
    *   **`mainWindow.webContents.openDevTools()`:** This method opens the DevTools panel for the associated browser window.

2.  Modify the `width` of the `BrowserWindow` to be wider in development mode to accommodate DevTools:

    ```javascript
    // main.js
    function createMainWindow() {
      mainWindow = new BrowserWindow({
        title: 'Image Resizer',
        width: process.env.NODE_ENV !== 'production' ? 1000 : 500, // Wider window in dev mode
        height: 600,
      });
      // ... (rest of createMainWindow function)
    }
    ```

    This uses a ternary operator to set the window width to 1000 pixels in development mode and 500 pixels in production mode.

### 8.2. Using `electronmon` for Live Reloading

Restarting the application manually every time you make a code change can be tedious. `electronmon` is a helpful tool that automatically restarts your Electron application whenever changes are detected in your code.

1.  Install `electronmon` globally (or locally as a dev dependency if preferred):

    ```bash
    npm install -g electronmon
    ```

2.  Modify the `start` script in `package.json` to use `electronmon` instead of `electron`:

    ```json
    "scripts": {
      "start": "electronmon ."
    },
    ```

3.  Run `npm start`.

    Now, when you make changes to `main.js` or files in the `renderer` folder, `electronmon` will automatically restart your Electron application, providing a faster development workflow.

> **electronmon:** A development utility that automatically restarts your Electron application when code changes are detected. It streamlines the development process by eliminating the need to manually restart the application after each modification.

## 9. Implementing the User Interface (UI)

Let's integrate the provided UI theme files to visually enhance our Image Resizer application.

### 9.1. Obtaining Theme Files

1.  Download or clone the provided GitHub repository for theme files.
2.  Locate the `theme_files` folder within the repository.
3.  Copy the contents of the `theme_files` folder ( `index.html`, `about.html`, `css`, `img`, `js`) into your `renderer` folder, replacing the existing `index.html` file.

### 9.2. Renaming `script.js` to `renderer.js`

For clarity and to better represent its role as the renderer process's JavaScript file, rename `script.js` to `renderer.js` within the `renderer/js` folder.  Remember to update the script tag in `index.html` to reflect this change:

```html
    <!-- index.html -->
    <script src="./js/renderer.js"></script>
```

### 9.3. Clearing `renderer.js`

For this chapter, we will write the renderer process JavaScript from scratch. Open `renderer/js/renderer.js` and clear any existing content, leaving it as an empty file.

### 9.4. Addressing Content Security Policy (CSP) Warning

When running the application with the new UI, you might see a warning message in the DevTools console related to Content Security Policy (CSP). This is a security feature of Chromium. To resolve this for development purposes, we can add a `<meta>` tag to both `index.html` and `about.html` files.

1.  Open `renderer/index.html` and `renderer/about.html`.
2.  Add the following `<meta>` tag within the `<head>` section of both files:

    ```html
    <meta http-equiv="Content-Security-Policy" content="script-src 'self'">
    ```

    > **Content Security Policy (CSP):** A security standard for web browsers that helps prevent cross-site scripting (XSS) attacks. It allows you to define a policy that controls the sources from which the browser is allowed to load resources such as scripts, stylesheets, and images.

This meta tag relaxes the CSP for scripts, allowing scripts from the same origin (`'self'`) to be executed. In a production application, a more restrictive CSP should be implemented for enhanced security.

After these steps, running `npm start` should display the themed UI for the Image Resizer application.

## 10. Customizing the Application Menu

Electron allows you to customize the default application menu, which appears at the top of the application window (on Windows and Linux) or at the top of the screen (on macOS). We will create a custom menu with "File" and "Help" menus.

### 10.1. Creating a Menu Template in `main.js`

1.  In `main.js`, import the `Menu` module from Electron:

    ```javascript
    // main.js
    const { app, BrowserWindow, Menu } = require('electron'); // Import Menu
    // ... (rest of main.js code)
    ```

2.  Below the `createMainWindow` function, create a `menuTemplate` array. This array will define the structure of our menu.

    ```javascript
    // main.js
    const { app, BrowserWindow, Menu } = require('electron');
    const path = require('path');

    // ... (isMac and mainWindow variables, createMainWindow function, app event listeners)

    const menuTemplate = [
      {
        label: 'File', // File menu
        submenu: [
          {
            label: 'Quit', // Quit menu item
            accelerator: isMac ? 'Command+W' : 'Ctrl+W', // Shortcut for quit
            click: () => {
              app.quit(); // Quit application on click
            },
          },
        ],
      },
    ];
    ```

    *   **`Menu` module:** Provides functionality to create native application menus.
    *   **`menuTemplate`:** An array of menu items that defines the structure of the application menu. Each object in the array represents a top-level menu item (like "File").
    *   **`label`:** The text displayed for the menu item.
    *   **`submenu`:** An array of submenu items that appear when a top-level menu item is clicked or hovered.
    *   **`accelerator`:** Defines a keyboard shortcut for the menu item. `isMac ? 'Command+W' : 'Ctrl+W'` sets different shortcuts for macOS (Command+W) and Windows/Linux (Ctrl+W).
    *   **`click`:** A function that is executed when the menu item is clicked. `app.quit()` terminates the application.

### 10.2. Implementing the Menu

1.  In `main.js`, inside the `app.whenReady().then()` block, after calling `createMainWindow()`, add the following code to build and set the application menu:

    ```javascript
    // main.js
    app.whenReady().then(() => {
      createMainWindow();

      // Implement Menu
      const mainMenu = Menu.buildFromTemplate(menuTemplate); // Build menu from template
      Menu.setApplicationMenu(mainMenu); // Set the application menu
    });
    ```

    *   **`Menu.buildFromTemplate(template)`:** Creates a `Menu` object from the provided `menuTemplate`.
    *   **`Menu.setApplicationMenu(menu)`:** Sets the application menu for the entire application.

2.  Run `npm start`. You should now see a "File" menu in your application's menu bar with a "Quit" option.

### 10.3. Using Menu Roles

Electron provides pre-defined "roles" for common menu items like "File," "Edit," and "View." Using roles can simplify menu creation and ensure platform-consistent behavior. Let's modify the "File" menu to use the `fileMenu` role.

1.  Modify the `menuTemplate` in `main.js` as follows:

    ```javascript
    // main.js
    const menuTemplate = [
      {
        role: 'fileMenu', // Use 'fileMenu' role for File menu
      },
    ];
    ```

    *   **`role: 'fileMenu'`:** This replaces the manual "File" menu definition with Electron's built-in "fileMenu" role, which provides standard file-related menu items like "Close Window" (instead of "Quit" in this simplified example).

2.  Run `npm start`. The "File" menu will now display items appropriate for the platform, such as "Close Window" on macOS.

### 10.4. Adding Platform-Specific Menu Items (About Menu)

On macOS, it's customary to have an "About" menu item under the application name menu. On Windows and Linux, "About" is typically placed under a "Help" menu. We need to create platform-specific menu structures to accommodate this.

1.  Modify the `menuTemplate` in `main.js` to include platform-specific "About" menus:

    ```javascript
    // main.js
    const menuTemplate = [
      ...(isMac
        ? [
            {
              label: app.name, // Application name menu on macOS
              submenu: [{ role: 'about' }], // About item under app name menu
            },
          ]
        : []), // Empty array if not macOS
      {
        role: 'fileMenu',
      },
      ...(isMac
        ? []
        : [
            {
              label: 'Help', // Help menu on Windows/Linux
              submenu: [{ role: 'about' }], // About item under Help menu
            },
          ]), // Empty array if macOS
    ];
    ```

    *   **`...(isMac ? [...] : [])`:** This uses the spread syntax (`...`) and a ternary operator to conditionally include menu items based on the `isMac` variable.
    *   **`app.name`:**  Electron provides `app.name` to get the application name, which is useful for the macOS application menu.
    *   **`role: 'about'`:**  Electron's built-in 'about' role provides a standard "About" dialog.

2.  Run `npm start`. On macOS, you should see an application name menu with an "About" item. On Windows/Linux, you should see a "Help" menu with an "About" item.

### 10.5. Creating a Custom "About" Window

Instead of using the default "About" dialog provided by the `'about'` role, let's create a custom "About" window that displays our own content from `renderer/about.html`.

1.  Create a new function `createAboutWindow` in `main.js`:

    ```javascript
    // main.js
    let aboutWindow; // Declare aboutWindow in global scope

    function createAboutWindow() {
      aboutWindow = new BrowserWindow({
        title: 'About Image Resizer',
        width: 300,
        height: 300,
        resizable: false, // Prevent window resizing
        parent: mainWindow, // Make aboutWindow a child of mainWindow
        modal: true, // Make aboutWindow modal (blocks interaction with mainWindow)
      });

      aboutWindow.loadFile(path.join(__dirname, 'renderer', 'about.html'));
    }
    ```

    *   **`resizable: false`:**  Disables window resizing for the "About" window.
    *   **`parent: mainWindow`:** Makes `aboutWindow` a child window of `mainWindow`.
    *   **`modal: true`:** Makes `aboutWindow` modal, meaning the user must interact with it before interacting with the main window.

2.  Modify the `menuTemplate` to use `createAboutWindow` for the "About" menu items instead of the `'about'` role:

    ```javascript
    // main.js
    const menuTemplate = [
      ...(isMac
        ? [
            {
              label: app.name,
              submenu: [
                {
                  label: 'About', // Custom About menu item
                  click: createAboutWindow, // Call createAboutWindow on click
                },
              ],
            },
          ]
        : []),
      {
        role: 'fileMenu',
      },
      ...(isMac
        ? []
        : [
            {
              label: 'Help',
              submenu: [
                {
                  label: 'About', // Custom About menu item
                  click: createAboutWindow, // Call createAboutWindow on click
                },
              ],
            },
          ]),
    ];
    ```

    *   **`click: createAboutWindow`:** Sets the `click` handler for the "About" menu items to call the `createAboutWindow` function.

3.  Run `npm start`. Now, clicking the "About" menu item (under the application name on macOS or under "Help" on Windows/Linux) should open a custom "About" window displaying the content from `renderer/about.html`.

## 11. Handling User Input and Image Selection (Renderer Process)

Now let's start implementing the core functionality of the Image Resizer application by handling user input in the renderer process.

### 11.1. Selecting UI Elements in `renderer.js`

1.  Create a new file `renderer.js` in the `renderer/js` folder (if it doesn't already exist).
2.  Open `renderer/js/renderer.js`.
3.  Select the necessary UI elements using their IDs from `index.html`. Add the following JavaScript code to `renderer.js`:

    ```javascript
    // renderer/js/renderer.js
    const form = document.getElementById('img-form');
    const img = document.getElementById('img');
    const outputPath = document.getElementById('output-path');
    const filename = document.getElementById('filename');
    const heightInput = document.getElementById('height');
    const widthInput = document.getElementById('width');
    ```

    This code uses `document.getElementById()` to retrieve references to the HTML elements we'll be interacting with, such as the form, image input, output path display, filename display, and width/height input fields.

### 11.2. Adding Event Listener for Image Input Change

We need to add an event listener to the image input (`img`) to detect when the user selects an image file.

1.  In `renderer/js/renderer.js`, add the following event listener code:

    ```javascript
    // renderer/js/renderer.js
    const form = document.getElementById('img-form');
    const img = document.getElementById('img');
    const outputPath = document.getElementById('output-path');
    const filename = document.getElementById('filename');
    const heightInput = document.getElementById('height');
    const widthInput = document.getElementById('width');

    img.addEventListener('change', loadImage); // Event listener for image input change
    ```

    This line adds an event listener to the `img` element that listens for the 'change' event. When the user selects a file in the image input, the `loadImage` function will be executed.

### 11.3. Implementing `loadImage` Function

Now, let's implement the `loadImage` function to handle the image selection process.

1.  In `renderer/js/renderer.js`, add the `loadImage` function:

    ```javascript
    // renderer/js/renderer.js
    const form = document.getElementById('img-form');
    const img = document.getElementById('img');
    const outputPath = document.getElementById('output-path');
    const filename = document.getElementById('filename');
    const heightInput = document.getElementById('height');
    const widthInput = document.getElementById('width');

    img.addEventListener('change', loadImage);

    function loadImage(e) {
      const file = e.target.files[0]; // Get selected file
      if (!file) {
        return; // No file selected, exit function
      }

      // Check if file is an image
      if (!isFileImage(file)) {
        alertError('Please select an image'); // Alert error if not an image
        return;
      }

      // Display form and filename
      form.style.display = 'block'; // Show the form
      filename.innerText = file.name; // Display filename

      // Get original dimensions and set input values
      const image = new Image();
      image.src = URL.createObjectURL(file); // Create object URL for image

      image.onload = function () {
        widthInput.value = this.width; // Set width input value to original width
        heightInput.value = this.height; // Set height input value to original height
      };
    }
    ```

    *   **`e.target.files[0]`:**  Gets the first file from the `files` array of the input element. Even if it's a single file input, the files are still stored in an array.
    *   **`isFileImage(file)`:** A function (to be defined later) to check if the selected file is a valid image type.
    *   **`alertError('Please select an image')`:** A function (to be defined later) to display an error message to the user.
    *   **`form.style.display = 'block'`:** Makes the image resizing form visible. Initially, it's hidden using CSS class `hidden`.
    *   **`filename.innerText = file.name`:** Displays the selected image filename in the `filename` span.
    *   **`new Image()`:** Creates a new `Image` object in JavaScript.
    *   **`URL.createObjectURL(file)`:** Creates a temporary URL that represents the selected image file in memory. This URL can be used as the `src` of an `Image` object.
    *   **`image.onload = function() { ... }`:**  An event handler that is executed when the image has fully loaded. Inside this handler, we set the `value` of the `widthInput` and `heightInput` fields to the `width` and `height` of the loaded image using `this.width` and `this.height`.

### 11.4. Implementing `isFileImage` Function

We need to implement the `isFileImage` function to verify that the selected file is indeed an image (GIF, PNG, or JPEG).

1.  In `renderer/js/renderer.js`, add the `isFileImage` function:

    ```javascript
    // renderer/js/renderer.js
    // ... (UI element selections, event listener, loadImage function)

    function isFileImage(file) {
      const acceptedImageTypes = ['image/gif', 'image/png', 'image/jpeg']; // Array of accepted image types
      return file && acceptedImageTypes.includes(file.type); // Check if file type is in accepted types
    }
    ```

    *   **`acceptedImageTypes`:** An array containing MIME types for GIF, PNG, and JPEG images.
    *   **`file && acceptedImageTypes.includes(file.type)`:** Checks if a `file` object exists and if its `type` property (MIME type) is included in the `acceptedImageTypes` array.

### 11.5. Implementing `alertError` Function (Using `toastify-js`)

Let's implement the `alertError` function using the `toastify-js` library to display user-friendly error messages.

1.  Before we can use `toastify-js` in the renderer process, we need to expose it from the preload script. Create a file `preload.js` in the root directory of your project if you haven't already.  Add the following code to `preload.js`:

    ```javascript
    // preload.js
    const { contextBridge, ipcRenderer } = require('electron');
    const os = require('os');
    const path = require('path');
    const toastify = require('toastify-js'); // Import toastify-js in preload

    contextBridge.exposeInMainWorld('os', {
      homedir: () => os.homedir(),
    });

    contextBridge.exposeInMainWorld('path', {
      join: (...args) => path.join(...args),
    });

    contextBridge.exposeInMainWorld('ipcRenderer', {
      send: (channel, data) => ipcRenderer.send(channel, data),
      on: (channel, func) => ipcRenderer.on(channel, func),
    });

    contextBridge.exposeInMainWorld('toastify', { // Expose toastify to renderer
      toast: (options) => toastify(options).showToast(),
    });
    ```

    *   **`const toastify = require('toastify-js');`:** Imports the `toastify-js` module in the preload script, making it available to be exposed to the renderer process.
    *   **`contextBridge.exposeInMainWorld('toastify', { ... });`:** Exposes an object named `toastify` to the renderer process's `window` object.
    *   **`toast: (options) => toastify(options).showToast()`:**  Exposes a `toast` function that, when called from the renderer process, will display a toast notification using `toastify-js`.

2.  In `main.js`, make sure you have configured the `preload` script for your `BrowserWindow`:

    ```javascript
    // main.js
    function createMainWindow() {
      mainWindow = new BrowserWindow({
        title: 'Image Resizer',
        width: process.env.NODE_ENV !== 'production' ? 1000 : 500,
        height: 600,
        webPreferences: {
          preload: path.join(__dirname, 'preload.js'), // Set preload script
          contextIsolation: true, // Enable context isolation for security
          nodeIntegration: true, // Enable Node.js integration in renderer (use with caution)
        },
      });
      // ... (rest of createMainWindow function)
    }
    ```

    *   **`webPreferences: { preload: path.join(__dirname, 'preload.js'), ... }`:**  Configures web preferences for the `BrowserWindow`, specifically setting the `preload` script to `preload.js`.
    *   **`contextIsolation: true`:** Enables context isolation for security, separating the renderer process's JavaScript context from the preload script's context.
    *   **`nodeIntegration: true`:** Enables Node.js integration in the renderer process, allowing you to use Node.js modules directly in the renderer (use with caution for security reasons; context isolation is recommended).

3.  In `renderer/js/renderer.js`, implement the `alertError` function using the exposed `window.toastify.toast()` function:

    ```javascript
    // renderer/js/renderer.js
    // ... (UI element selections, event listener, loadImage, isFileImage functions)

    function alertError(message) {
      window.toastify.toast({ // Use exposed toastify function from preload
        text: message,
        duration: 5000, // 5 seconds
        close: false,
        style: {
          background: 'red',
          color: 'white',
          textAlign: 'center',
        },
      });
    }
    ```

    *   **`window.toastify.toast({ ... })`:** Calls the `toast` function exposed through the preload script via `contextBridge`. This will display a red-colored toast notification with the provided error `message`.

4.  Also implement the `alertSuccess` function for success messages, similar to `alertError`, but with a green background:

    ```javascript
    // renderer/js/renderer.js
    // ... (UI element selections, event listener, loadImage, isFileImage, alertError functions)

    function alertSuccess(message) {
      window.toastify.toast({ // Use exposed toastify function from preload
        text: message,
        duration: 5000, // 5 seconds
        close: false,
        style: {
          background: 'green',
          color: 'white',
          textAlign: 'center',
        },
      });
    }
    ```

Now, when you run the application and try to select a non-image file, you should see a red toast notification displayed at the bottom of the window with the message "Please select an image."

This comprehensive educational text provides a structured and detailed guide for building an Electron application. It breaks down the process into manageable steps, explains key concepts, and includes definitions of technical terms to enhance understanding for educational purposes. This text can serve as a valuable resource for anyone learning Electron development.
