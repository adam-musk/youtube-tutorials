---
layout: "../../layouts/BlogPost.astro"
title: "Creating an Interactive Developer Portfolio as a 2D Game"
pubDate: "2025-03-02 14:25:12.854469"
youtubeVideoID: "wy_fSStEgMs"
index:
---

# Creating an Interactive Developer Portfolio as a 2D Game

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/wy_fSStEgMs" frameborder="0" allowfullscreen></iframe>

This chapter will guide you through the process of building a unique and engaging developer portfolio by transforming it into a 2D interactive game. This approach offers a refreshing alternative to traditional, static portfolios, allowing potential employers and collaborators to explore your skills and projects in an immersive and memorable way.

## Introduction to the Project

This project demonstrates how to create a 2D developer portfolio designed as a game environment.  Instead of presenting information through standard web pages, users can navigate a virtual space and interact with objects to learn more about the developer's qualifications and experience.

### Project Overview

The core idea is to create a 2D game world, in this case, a house, which represents the developer's portfolio. Within this world, different objects are linked to specific aspects of the developer's profile.  For example:

*   A diploma on the wall represents a Computer Science degree.
*   A resume placed on a table links to an online resume document.
*   Text displays provide additional information about the developer.

This interactive approach aims to be more engaging than a typical portfolio website.  While some developers have explored 3D portfolios, this project focuses on a 2D implementation, leveraging the simplicity and accessibility of 2D game development.

### Technology Stack

This project utilizes the following technologies:

*   **JavaScript:** The primary programming language for building the game logic and interactivity.

    > **JavaScript**
    >
    > A high-level, interpreted programming language primarily used to make web pages interactive. It is also used server-side with Node.js and in other environments.

*   **Kaboom.js:** A JavaScript library specifically designed for creating 2D games in a simple and intuitive manner.

    > **Kaboom.js**
    >
    > A fast and fun JavaScript library for making 2D games. It prioritizes ease of use and rapid prototyping, making it suitable for beginners and experienced developers alike.

*   **HTML (HyperText Markup Language) and CSS (Cascading Style Sheets):**  Used for creating the user interface (UI) elements, particularly the text boxes and interactive text within the game.

    > **HTML (HyperText Markup Language)**
    >
    > The standard markup language for documents designed to be displayed in a web browser. It provides the structure and content of a webpage.
    >
    > **CSS (Cascading Style Sheets)**
    >
    > A style sheet language used for describing the presentation of a document written in a markup language like HTML. CSS controls the visual appearance of web pages.

*   **Responsive Design Principles:** Employed to ensure the portfolio game is accessible and functional across various screen sizes and devices, including mobile devices.

    > **Responsive Design**
    >
    > An approach to web design that aims to make web pages render well on a variety of devices and screen sizes by using flexible grids and layouts, images and CSS media queries.

### User Interaction and Responsiveness

A key consideration is making the portfolio game interactive and responsive to user input, particularly for mobile devices.

*   **Mouse and Touch Input:** The game is designed to be interacted with using both mouse clicks and touch input on touchscreens.
*   **HTML and CSS for UI Responsiveness:** Utilizing HTML and CSS for the UI elements ensures that text boxes and other interactive elements are responsive and adapt to different screen aspect ratios, crucial for mobile compatibility.

## Setting up the Development Environment

To begin developing this portfolio game, you will need to set up your development environment. This involves installing necessary software and initializing a project structure.

### Software Requirements

*   **VS Code (Visual Studio Code):** A popular and versatile code editor, recommended for this project.

    > **VS Code (Visual Studio Code)**
    >
    > A source code editor developed by Microsoft for Windows, Linux and macOS. It includes support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring.

*   **Node.js:** A JavaScript runtime environment required for using development tools and package managers.

    > **Node.js**
    >
    > An open-source, cross-platform, back-end JavaScript runtime environment that runs on the V8 engine and executes JavaScript code outside a web browser. Node.js is often used for building server-side and networking applications.

### Project Initialization with Vite

This project utilizes Vite, a build tool that streamlines JavaScript development and offers several advantages over traditional script tag inclusion.

*   **Vite (Vit):** A fast and opinionated web dev build tool that serves your code via native ES modules during development and bundles it with Rollup for production.

    > **Vite (Vit)**
    >
    > A build tool that aims to provide a faster and leaner development experience for modern web projects. It leverages native ES modules and other modern web technologies to achieve this speed.

*   **Bundler:** Vite acts as a bundler, which processes and prepares your JavaScript code for the browser.

    > **Bundler**
    >
    > A tool that takes JavaScript and related assets and bundles them together into a smaller number of files, often optimized for browser performance. Bundlers handle module resolution, code transformation, and optimization.

**Steps to Initialize the Project:**

1.  **Open VS Code:** Launch VS Code and open a new folder where you want to create your project.
2.  **Open Terminal:** Open the integrated terminal within VS Code (usually by going to `View > Terminal`).
3.  **Run Vite Project Creation Command:** In the terminal, type the following command and press Enter:

    ```bash
    npm create vite@latest .
    ```

    > **npm install**
    >
    > A command used by the Node Package Manager (npm) to install packages and dependencies for a Node.js project. These packages are typically listed in the `package.json` file.

    This command uses `npm`, the Node Package Manager, to execute `create-vite`, Vite's project scaffolding tool. The `.` specifies that the project should be created in the current folder.

4.  **Framework Selection:**  Vite will prompt you to select a framework. Choose "vanilla" for vanilla JavaScript, meaning no specific framework like React or Vue.js will be used.
5.  **Install Kaboom.js:** Once the project is created, navigate into the project directory in the terminal (if you aren't already there) and run the following command to install the Kaboom.js library:

    ```bash
    npm install kaboom
    ```

    This command adds Kaboom.js as a dependency to your project.  You can verify this by checking the `package.json` file, which lists your project's dependencies.

    > **package.json**
    >
    > A JSON file that is the heart of a Node.js project. It records important metadata about a project such as the name, version, dependencies, and scripts.

### Project Structure and File Setup

After initializing the project and installing Kaboom.js, you'll need to organize your project files and remove unnecessary boilerplate code.

*   **Boilerplate:** Pre-written code or templates that are automatically generated when starting a new project. Boilerplate is meant to be customized and form the foundation of your application.

**Steps to Structure the Project:**

1.  **Remove Boilerplate Files:** Delete the following files generated by Vite as they are not needed for this project:
    *   `main.js` (in the `src` folder, you will create a new one later)
    *   `counter.js` (in the `src` folder)
    *   `vite.svg` (in the `public` folder)
    *   `style.css` (in the `src` folder)

2.  **Create Folders:** Create the following folders at the root of your project directory:
    *   `src`: This folder will house your JavaScript source code.

        > **Source Folder (SRC)**
        >
        > A common directory in software projects that contains the source code files. In web development, this often includes JavaScript, CSS, and other assets that are processed by build tools.
    *   `public`: This folder will store public assets like images, fonts, and the game map data.

        > **Public Folder**
        >
        > A directory in a web project that contains static assets that are served directly to the browser without processing. This includes images, fonts, and other files that don't need to be bundled.

3.  **Create `vite.config.js`:** Create a file named `vite.config.js` at the root of your project. This file will contain Vite configuration settings.

    > **v config.js**
    >
    > A configuration file for Vite projects. It allows developers to customize Vite's behavior, such as setting up plugins, defining build options, and configuring server settings.

    Add the following code to `vite.config.js`:

    ```javascript
    import { defineConfig } from 'vite'

    export default defineConfig({
      base: './',
      build: {
        minify: 'terser',
      },
    })
    ```

    This configuration does the following:

    *   **`import { defineConfig } from 'vite'`**: Imports the `defineConfig` function from Vite, which is used to define the configuration object.
    *   **`export default defineConfig({...})`**: Exports the configuration object as the default export, making it accessible to Vite.
    *   **`base: './'`**: Specifies the base URL for public assets. Setting it to `'./'` ensures assets are referenced relative to the HTML file, which is important for deployment.
    *   **`build: { minify: 'terser' }`**: Configures the build process to use `terser` for code minification.

        > **Transpile/Compile**
        >
        > The process of converting code from one language or language version to another. In web development, this often refers to converting modern JavaScript code (ES6+) into code that can run in older browsers (ES5).
        >
        > **Optimizations/Minification**
        >
        > Techniques used to reduce the size and improve the performance of code. Minification specifically involves removing unnecessary characters (like whitespace and comments) from code without changing its functionality.

        > **Import statements**
        >
        > A feature in modern JavaScript (ES modules) that allows you to include and use code from other modules or files. This promotes modularity and code organization.

        > **Export default**
        >
        > A way to export a single value, such as a function, class, or object, as the main export from a JavaScript module. It's commonly used when a module primarily exports one thing.

        > **Define config**
        >
        > A function provided by Vite to help define the configuration object in `vite.config.js`. It provides type hinting and autocompletion for configuration options.

        > **Base (in vite config)**
        >
        > In Vite's configuration, the `base` option specifies the base URL for all public assets. It affects how paths are generated when building the project, especially important for deployment in subdirectories.

        > **npm run build**
        >
        > A command used to build a production-ready version of a project using npm scripts defined in `package.json`. For Vite projects, this command typically bundles and optimizes the code for deployment.

        > **Assets**
        >
        > Static files required by a web application, such as images, fonts, and other non-code resources. Vite handles assets in the `public` directory, making them directly accessible in the browser.

        > **Minification (turer, esbuild)**
        >
        > Code minification is the process of removing unnecessary characters from code to reduce its size and improve loading times. `terser` and `esbuild` are different JavaScript minifiers; `terser` is chosen here due to compatibility with Kaboom.js.

        > **Dev dependency**
        >
        > In `package.json`, dev dependencies are packages that are only needed during development and not in the final production build. `terser` is added as a dev dependency because it's used for building the project, not for running it in the browser.

        The `minify: 'terser'` option is crucial because of a known issue with Kaboom.js and the default minifier (`esbuild`) in Vite. Using `terser` ensures that the built game functions correctly. You will need to install `terser` as a development dependency by running:

        ```bash
        npm install -D terser
        ```

4.  **Create `main.js` in `src`:** Create a new file named `main.js` inside the `src` folder. This will be your main JavaScript file where you will write the game logic.

    > **main.js**
    >
    > A common name for the primary JavaScript file in a project. It often serves as the entry point for the application's logic and is where execution begins.

5.  **Modify `index.html`:** Open the `index.html` file at the root of your project and make the following modifications:

    *   **Add Style Tag:** Inside the `<head>` or `<body>` tag (ideally in `<body>` for clarity in this project), add a `<style>` tag. This is where you will write your CSS styles for the game.

        > **index.html**
        >
        > The main HTML file of a web project, typically the entry point that is loaded when a user accesses the website or application. It structures the content and links to other resources like JavaScript and CSS files.

        > **style tag**
        >
        > An HTML tag used to embed Cascading Style Sheets (CSS) directly within an HTML document. Styles defined within `<style>` tags apply to the elements in the HTML document.

    *   **Modify Script Tag:** Locate the `<script>` tag in `index.html` that imports `main.js`. Change the `src` attribute to point to the correct path within the `src` folder:

        ```html
        <script type="module" src="./src/main.js"></script>
        ```

        > **script tag**
        >
        > An HTML tag used to embed or link to executable scripts, typically JavaScript, within an HTML document. The `src` attribute specifies the path to an external script file, and `type="module"` indicates it's a JavaScript module.

    *   **Canvas Element:** Inside the `<body>` tag, add a `<canvas>` element with the ID "game". This is where Kaboom.js will render the game. Also, create a `<div>` element with the ID "ui" to contain HTML-based UI elements.

        ```html
        <body>
          <canvas id="game"></canvas>
          <div id="ui"></div>
          <script type="module" src="./src/main.js"></script>
        </body>
        ```

        > **canvas**
        >
        > An HTML element that provides a resolution-dependent bitmap canvas which can be used for rendering graphics, game visuals, or other visual images on the fly via scripting (usually JavaScript).

        > **ID (of elements)**
        >
        > In HTML, the `id` attribute is used to uniquely identify an element within a document. It's used by CSS and JavaScript to target and manipulate specific elements.

6.  **Create `KaboomCtx.js` in `src`:** Create a new file named `KaboomCtx.js` (or `KaboomContext.js`) inside the `src` folder. This file will be dedicated to setting up the Kaboom.js context.

    > **Kaboom context.js (CTX)**
    >
    > A dedicated JavaScript file (often named `KaboomCtx.js` or similar) used to initialize and configure the Kaboom.js game engine. It encapsulates the Kaboom.js context and makes it easily accessible throughout the project.

    Add the following code to `KaboomCtx.js`:

    ```javascript
    import kaboom from 'kaboom';

    export const K = kaboom({
      global: false,
      touchToMouse: true,
      canvas: document.getElementById('game'),
    });
    ```

    This code initializes Kaboom.js with the following configurations:

    *   **`import kaboom from 'kaboom';`**: Imports the Kaboom.js library.
    *   **`export const K = kaboom({...});`**: Initializes Kaboom.js and exports the context object as `K`.
    *   **`global: false`**: Prevents Kaboom.js functions from being globally available, promoting better code organization and preventing naming conflicts.
    *   **`touchToMouse: true`**: Enables touch input to be translated into mouse events, making the game playable on touch devices.
    *   **`canvas: document.getElementById('game')`**:  Tells Kaboom.js to use the `<canvas>` element with the ID "game" for rendering.

        > **Global property (in Kaboom config)**
        >
        > A configuration option in Kaboom.js that determines whether Kaboom.js functions are made globally available in the JavaScript environment. Setting `global: false` restricts them to the exported context, improving code organization.
        >
        > **Touch to Mouse property**
        >
        > A Kaboom.js configuration option (`touchToMouse: true`) that automatically translates touch events on touch devices into mouse events. This allows developers to write code primarily for mouse input while ensuring compatibility with touchscreens.
        >
        > **Canvas property**
        >
        > A Kaboom.js configuration option that specifies which HTML `<canvas>` element Kaboom.js should use for rendering the game. It's set using `canvas: document.getElementById('yourCanvasId')`.

7.  **Create `constants.js` in `src`:** Create a new file named `constants.js` inside the `src` folder. This file will store project-wide constants, such as scale factors and dialogue data.

    > **Constant.js**
    >
    > A JavaScript file dedicated to storing constant values used throughout a project. This improves code maintainability by centralizing configuration values like scale factors, game settings, or dialogue data.

8.  **Create `utils.js` in `src`:** Create a new file named `utils.js` inside the `src` folder. This file will house utility functions, such as the dialogue display function.

    > **Utils.js**
    >
    > A JavaScript file used to store utility functions that are used across different parts of a project. These functions are typically reusable and perform common tasks, such as displaying dialogues or handling game logic.

9.  **Public Assets:** Create a folder named `assets` inside the `public` folder. This folder will contain game assets like fonts and sprite sheets.

    > **assets**
    >
    > In web development, the `assets` directory within the `public` folder (or similar) is commonly used to store static files like images, fonts, and sounds that are directly served to the browser without processing by build tools.

    *   **Font File:** Download the `monogram.ttf` font file (link provided in the video description) and place it inside the `public/assets` folder.

        > **monogram.ttf**
        >
        > A TrueType Font (TTF) file named "monogram". In this context, it's used as the font for text elements within the developer portfolio game, providing a pixel-art style.

    *   **Sprite Sheet:** Download the `SpriteSheet.png` sprite sheet image (link provided in the video description) and place it inside the `public/assets` folder.

        > **Sprite sheet**
        >
        > A single image file that contains multiple smaller images, called sprites, arranged in a grid. Sprite sheets are commonly used in 2D game development to efficiently load and manage game graphics.

    *   **Tiled Map Files:** Download the `map.json` and `map.png` files (links provided in the video description) and place them directly inside the `public` folder. These files represent the game map created with Tiled.

        > **tiled**
        >
        > A popular open-source tile map editor used for creating 2D game levels. Tiled allows developers to visually design game maps and export them in formats that can be used by game engines like Kaboom.js.
        >
        > **map.json**
        >
        > A JSON file that stores the data for a tile map created with Tiled. It contains information about layers, tilesets, objects, and other map properties, used by game engines to render and interact with the map.

With these steps completed, your project environment is set up, and you are ready to begin implementing the game logic and content.

## Loading Assets and Setting up the Game Scene

With the project structure in place, the next step is to load the necessary assets (sprites and map) and set up the initial game scene in Kaboom.js.

### Loading Sprites

Sprites are essential visual components in 2D games. Kaboom.js provides functions to easily load and manage sprites.

1.  **Open `main.js`:** Navigate to and open the `main.js` file in your `src` folder.
2.  **Import Kaboom Context:** Import the Kaboom context (`K`) that you exported from `KaboomCtx.js`:

    ```javascript
    import { K } from './KaboomCtx.js';
    ```

3.  **Load Sprite Sheet:** Use the `loadSprite` function from Kaboom.js to load the `SpriteSheet.png` image. Add this code within your `main.js` file:

    ```javascript
    K.loadSprite('spriteSheet', 'assets/SpriteSheet.png', {
      sliceX: 39,
      sliceY: 27,
      anims: {
        'idleDown': { from: 536, to: 536 },
        'walkDown': { from: 536, to: 539, loop: true, speed: 8 },
        'walkUp': { from: 563, to: 566, loop: true, speed: 8 },
        'walkSide': { from: 550, to: 553, loop: true, speed: 8 },
      },
    });
    ```

    > **Sprite**
    >
    > A 2D image or graphic that is used as a building block in 2D games. Sprites can represent characters, objects, or elements of the game environment.
    >
    > **Frames**
    >
    > Individual images within a sprite sheet that, when played in sequence, create animation. In Kaboom.js, frames are referenced by their index in the sprite sheet.
    >
    > **Slice X, Slice Y**
    >
    > Parameters in Kaboom.js's `loadSprite` function that define how a sprite sheet should be divided into individual frames. `sliceX` specifies the number of frames horizontally, and `sliceY` vertically.
    >
    > **anims property**
    >
    > An option within Kaboom.js's `loadSprite` function used to define animations for a sprite. It maps animation names (like 'idleDown', 'walkUp') to frame sequences and animation properties.
    >
    > **Idle down animation**
    >
    > An animation state for a character when they are stationary and facing downwards. In this project, it consists of a single frame (frame 536).
    >
    > **Frame number**
    >
    > An index that identifies a specific frame within a sprite sheet. Frame numbers are used in Kaboom.js to specify which frame to display or include in an animation sequence.

    **Explanation of the `loadSprite` function call:**

    *   **`'spriteSheet'`**:  This is the key or name you assign to the loaded sprite sheet. You will use this key to reference the sprite sheet later in your code.
    *   **`'assets/SpriteSheet.png'`**: This is the path to the `SpriteSheet.png` file in your `public/assets` folder. Vite allows you to access files in the `public` folder directly by their path from the root.
    *   **`{ ... }`**: This is an options object that configures how Kaboom.js should interpret the sprite sheet:
        *   **`sliceX: 39`**: Specifies that the sprite sheet is divided into 39 columns of frames horizontally.
        *   **`sliceY: 27`**: Specifies that the sprite sheet is divided into 27 rows of frames vertically.
        *   **`anims: { ... }`**: Defines animation sequences for the sprite sheet:
            *   **`'idleDown': { from: 536, to: 536 }`**: Defines the 'idleDown' animation, which uses only frame 536 (meaning it's a static image).
            *   **`'walkDown': { from: 536, to: 539, loop: true, speed: 8 }`**: Defines the 'walkDown' animation, using frames 536 to 539, set to loop continuously (`loop: true`) at a speed of 8 frames per second (`speed: 8`).
            *   **`'walkUp'`, `'walkSide'`**: Similar animation definitions for walking up and sideways, using different frame ranges from the sprite sheet.

    The frame numbers (e.g., 536, 539, 563) were determined using the **Tiled editor**.

    > **Tiled editor**
    >
    > A cross-platform tile map editor, often simply referred to as "Tiled". It is used to create tile-based levels for games and provides tools for drawing maps, placing objects, and setting properties.

### Creating the Game Scene

Kaboom.js uses scenes to organize different parts of your game, such as menus, levels, or in this case, the main game environment.

1.  **Define the Main Scene:**  Use the `scene` function from Kaboom.js to define a scene named "main". Make this function asynchronous (`async`) as it will load the map data.

    ```javascript
    K.scene('main', async () => {
      // Scene code will go here
    });
    ```

2.  **Set the Default Scene:** Use the `go` function to set "main" as the default scene that Kaboom.js should load when the game starts.

    ```javascript
    K.go('main');
    ```

3.  **Set Background Color:** Within the "main" scene function, set the background color using `setBackground`.

    ```javascript
    K.scene('main', async () => {
      K.setBackground(K.Color.fromHex('#300b47'));
      // ... rest of scene code
    });
    ```

4.  **Load Map Data:** Fetch the `map.json` file using the `fetch` API and parse it as JSON.

    ```javascript
    K.scene('main', async () => {
      K.setBackground(K.Color.fromHex('#300b47'));

      const mapData = await fetch('map.json').then((res) => res.json());
      const layers = mapData.layers;

      // ... rest of scene code
    });
    ```

    > **Fetch API**
    >
    > A modern JavaScript interface for making network requests. It provides a way to retrieve resources from servers, such as JSON data or images, and is commonly used for loading game assets.

5.  **Load Map Sprite:** Load the `map.png` image as a sprite using `loadSprite`.

    ```javascript
    K.scene('main', async () => {
      K.setBackground(K.Color.fromHex('#300b47'));

      const mapData = await fetch('map.json').then((res) => res.json());
      const layers = mapData.layers;

      K.loadSprite('map', 'map.png');

      // ... rest of scene code
    });
    ```

6.  **Add Map Game Object:** Create and add the map game object to the scene using `K.add`.

    ```javascript
    K.scene('main', async () => {
      K.setBackground(K.Color.fromHex('#300b47'));

      const mapData = await fetch('map.json').then((res) => res.json());
      const layers = mapData.layers;

      K.loadSprite('map', 'map.png');

      const map = K.add([
        K.sprite('map'),
        K.pos(0, 0),
        K.scale(4), // Assuming scale factor is 4
      ]);

      // ... rest of scene code
    });
    ```

    > **Game object (in Kaboom JS)**
    >
    > The fundamental building block in Kaboom.js for creating game entities. Game objects are composed of components that define their behavior and properties, such as sprite, position, area, and body.
    >
    > **Components (in Kaboom JS)**
    >
    > Reusable modules that define specific behaviors and properties of game objects in Kaboom.js. Components are added to game objects as an array and include built-in components like `sprite`, `pos`, `area`, `body`, and custom components.
    >
    > **Entity Component System**
    >
    > A design pattern used in game development where game entities (objects) are composed of reusable components. Each component provides specific functionality, and entities are created by combining different components. Kaboom.js uses an ECS architecture.
    >
    > **Make function (Kaboom JS)**
    >
    > A Kaboom.js function used to create a game object without immediately adding it to the scene. It's useful for pre-configuring game objects before adding them to the active scene.
    >
    > **Add function (Kaboom JS)**
    >
    > A Kaboom.js function used to add a game object to the current scene. It takes an array of components as input and returns the created game object instance.
    >
    > **Sprite component**
    >
    > A Kaboom.js component that renders a sprite (image) for a game object. It's added using `K.sprite('spriteName')`, where 'spriteName' is the key of a sprite loaded with `loadSprite`.
    >
    > **Positional component**
    >
    > A Kaboom.js component that defines the position of a game object in the game world. It's added using `K.pos(x, y)` and allows you to set and manipulate the object's 2D coordinates.
    >
    > **Scale component**
    >
    > A Kaboom.js component that scales a game object. It's added using `K.scale(factor)` or `K.scale(xFactor, yFactor)` and allows you to resize the object visually.
    >
    > **Scale factor**
    >
    > A numerical value used to multiply the size of an object. In this project, a scale factor of 4 is used to enlarge the pixel art graphics to a more visible size.

    **Explanation of the Map Game Object Creation:**

    *   **`K.add([...])`**: Adds a new game object to the scene.
    *   **`K.sprite('map')`**: Adds the Sprite component, using the sprite named 'map' (loaded from `map.png`). This makes the map image visible.
    *   **`K.pos(0, 0)`**: Adds the Positional component, setting the map's position to the top-left corner of the canvas (coordinates 0, 0).
    *   **`K.scale(4)`**: Adds the Scale component, scaling the map up by a factor of 4 in both dimensions. This makes the pixel art map larger and more visible.

7.  **Run the Development Server:**  In your terminal, run the command `npm run dev`. This will start the Vite development server. Open the provided local URL in your web browser (usually `http://localhost:5173/`) to view your game. You should now see the map background displayed.

With these steps, you have successfully loaded the map sprite and displayed it in your Kaboom.js game scene. The next chapter will focus on adding the player character and implementing movement.
