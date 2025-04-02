---
layout: "../../layouts/BlogPost.astro"
title: "Creating Desktop Games with JavaScript: A Practical Guide Using Capl and Tori"
pubDate: "2025-02-28 15:30:53.132370"
youtubeVideoID: "fyqRSaSJf0I"
index: 56
---

# Creating Desktop Games with JavaScript: A Practical Guide Using Capl and Tori

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/fyqRSaSJf0I" frameborder="0" allowfullscreen></iframe>


## Introduction: Bridging Web and Desktop Game Development with JavaScript

JavaScript, traditionally known as the language of the web, is rapidly expanding its horizons. While primarily used for creating interactive websites and web applications, advancements in technology now allow JavaScript to venture into desktop application development, including game creation. This chapter will guide you through the process of developing a desktop game using JavaScript, leveraging the power of the **Tori** framework and the **Capl** game library.

> **Tori:** Tori is a framework that enables developers to build desktop applications using web technologies like JavaScript, HTML, and CSS. It allows you to package web applications as native desktop applications for various operating systems.

We will explore how to utilize Tori to create installable games for Windows PCs, overcoming the limitations of web-based game storage and distribution.  This approach offers unique advantages, particularly for games requiring robust save systems and distribution outside of the browser environment.

This chapter assumes a foundational understanding of JavaScript. No prior experience with Tori or Capl is necessary, as we will comprehensively explain each concept as we progress. By the end of this chapter, you will have a functional desktop game built in JavaScript, equipped with saving capabilities and ready for distribution.

## 1. Setting Up Your Development Environment: Prerequisites and Installation

Before diving into game development, it's essential to set up your development environment. This section outlines the necessary prerequisites and installation steps, primarily focused on a Windows environment, which is often the target platform for desktop game distribution.

### 1.1 Essential Prerequisites

To follow along with this chapter, ensure you have the following software installed on your system:

*   **Node.js and npm (Node Package Manager):** These are fundamental for JavaScript development, enabling you to manage project dependencies and run development tools. Ensure Node.js is installed and that `npm` is available in your command line.

    > **npm (Node Package Manager):** npm is a package manager for Node.js. It is used to install, manage, and share JavaScript packages and libraries, simplifying the process of incorporating external tools and functionalities into your projects.

*   **Rust:** Although we won't be writing Rust code directly in this tutorial, Tori itself is built with Rust.  Rust is required as part of the Tori development toolchain.

*   **Webview2 Runtime:** Tori utilizes the system's web view to render applications, offering a lightweight alternative to embedding a full browser like Electron. On Windows, Tori relies on Webview2.

    > **Webview2 Runtime:** Webview2 Runtime is a Microsoft component that allows applications to embed web technologies (HTML, CSS, JavaScript) within native applications. It uses the Microsoft Edge (Chromium-based) rendering engine and is essential for Tori applications on Windows.

### 1.2 Installing Prerequisites on Windows

Follow the official Tori documentation for detailed instructions on setting up your Windows environment. Key steps include:

*   **Installing Node.js:** Download and install Node.js from the official website ([https://nodejs.org/](https://nodejs.org/)). This installation typically includes npm.
*   **Installing Rust:** Follow the instructions on the official Rust website ([https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)) to install Rust using `rustup`.
*   **Ensuring Webview2 Runtime is Available:** On newer Windows versions (Windows 11 and some Windows 10 versions), Webview2 Runtime may be pre-installed. If not, the Tori installer will handle its installation when you build your game for distribution.

> **Electron:** Electron is another popular framework for building desktop applications with web technologies. Unlike Tori, Electron packages a full Chromium browser with each application, leading to larger application sizes but ensuring consistent rendering across platforms.

**Note:** While this tutorial primarily focuses on Windows, you can adapt the principles and code for macOS or Linux, though the final executable will be platform-specific.

## 2. Project Initialization: Setting Up a Tori Project with Capl

With the prerequisites in place, we can now initialize our Tori project and integrate the Capl game library.

### 2.1 Creating the Tori Project

1.  **Open your terminal or command prompt.**
2.  **Navigate to the directory where you want to create your project.**
3.  **Run the following command:**

    ```bash
    npm create t-a@latest .
    ```

    The `.` at the end specifies that the project files should be created in the current directory.

4.  **Follow the prompts:**

    *   **Package name:** Choose a name for your project (e.g., `creby-game`).
    *   **Choose your frontend framework:** Select `React`. (We will remove React later, but it provides a convenient project structure with Vite).
    *   **Choose your frontend language:** Select `JavaScript`.
    *   **Choose your package manager:** Select `npm`.

This command uses `create-tori-app`, the official Tori project initializer, to set up a basic Tori project structure with React and JavaScript.

### 2.2 Removing React Dependencies

Since we are focusing on a simpler game structure and won't be utilizing React's component-based architecture for this project, we can remove the React dependencies to streamline our project.

1.  **Navigate to your project directory in the terminal.**
2.  **Run the following commands to uninstall React and related packages:**

    ```bash
    npm uninstall react react-dom
    npm uninstall @vitejs/plugin-react
    ```

3.  **Modify `vite.config.js`:** Open the `vite.config.js` file in your project's root directory and remove or comment out any lines related to React plugins. The `plugins` array in `vite.config.js` should be empty or removed.

### 2.3 Installing Capl

Now, install the Capl game library as a project dependency.

1.  **In your project directory in the terminal, run:**

    ```bash
    npm install capl@0.1.7-u3000
    ```

    We are installing a specific version (`0.1.7-u3000`) to ensure consistency with this tutorial. Pinning versions is good practice to avoid unexpected issues due to library updates.

2.  **Verify Installation:** Check your `package.json` file. Under `dependencies`, you should now see `capl` with the specified version.

### 2.4 Configuring `package.json` Scripts

For convenience, modify the scripts in your `package.json` file to align with common development workflows for Tori projects.

1.  **Open `package.json` in your project directory.**
2.  **Modify the `scripts` section to the following:**

    ```json
    "scripts": {
      "dev": "tori dev",
      "dev:browser": "vite",
      "build": "tori build",
      "build:browser": "vite build",
      "preview": "vite preview"
    },
    ```

    *   `dev`:  Runs the Tori development environment, launching your application as a desktop window.
    *   `dev:browser`: Runs the Vite development server, allowing you to view your application in a web browser.
    *   `build`: Builds the desktop application executable.
    *   `build:browser`: Builds the web application bundle using Vite.
    *   `preview`:  Previews the built web application in a browser.

### 2.5 Setting up `index.html` and `main.js`

Prepare your entry point files for the game logic.

1.  **Clean up `index.html`:** Open `public/index.html`. Remove the existing content within the `<head>` and `<body>` tags.  A minimal `index.html` might look like this:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Creby Game</title>
    </head>
    <body>
        <script type="module" src="/src/main.js"></script>
    </body>
    </html>
    ```

2.  **Create `main.js`:** Create a new file named `main.js` in the `src` directory. This file will be the main entry point for your game logic.

3.  **Basic Capl Initialization in `main.js`:** Add the following code to `src/main.js` to initialize Capl and create a basic canvas:

    ```javascript
    import kaboom from 'capl' // Note: kaboom is still the import name

    kaboom({
      width: 1280,
      height: 720,
      letterbox: true,
      global: false,
      scale: 2,
    });

    // Your game code will go here
    ```

    > **Canvas:** In web and game development, a canvas is an HTML element that acts as a drawing surface. JavaScript can be used to dynamically render graphics, animations, and games onto the canvas.

    > **Letterbox:** Letterbox is a technique used to maintain the aspect ratio of a game or video when displayed on a screen with a different aspect ratio. It adds black bars at the top and bottom or sides to prevent distortion.

4.  **Run the Development Server:** In your terminal, run:

    ```bash
    npm run dev
    ```

    This should launch your Tori application. You should see a window with a black background (due to default canvas styling) representing your Capl canvas. Pressing F12 will open the developer console, useful for debugging.

## 3. Core Game Structure: Scenes, Assets, and Utilities

With the project set up, we can start building the game's core structure. This involves organizing our game logic into scenes, loading assets, and creating utility functions.

### 3.1 Game Scenes: Start Menu and Main Game

Organize your game into distinct scenes to manage different game states (e.g., menu, gameplay, game over).

1.  **Define Scenes in `main.js`:** In `main.js`, define two scenes: `start` (for the menu) and `main` (for the actual game).

    ```javascript
    import kaboom from 'capl'; // Ensure this import remains
    // ... (Capl initialization) ...

    scene("start", () => {
      // Logic for the start menu scene
    });

    scene("main", () => {
      // Logic for the main game scene
    });

    go("start"); // Start the game with the 'start' scene
    ```

    > **Scene:** In game development, a scene represents a distinct part of the game, such as a menu screen, a gameplay level, or a cutscene. Scenes help organize game logic and assets, allowing for a modular and manageable game structure.

2.  **Create Utility Functions in `utils.js`:** Create a new file named `utils.js` in the `src` directory to house reusable utility functions. For now, create a function to set a background color.

    ```javascript
    // src/utils.js
    export function makeBackground(k, hexColor) {
      k.add([
        k.rect(k.width(), k.height()),
        k.color(k.hex(hexColor)),
        k.fixed(), // Optional: Make background fixed relative to camera
        k.layer('bg'), // Optional: Assign to a background layer
      ]);
    }

    export function goToGame(k) {
        k.go("main");
    }

    export function computeRank(score) {
        if (score > 30) return "S";
        if (score > 20) return "A";
        if (score > 10) return "B";
        if (score > 2) return "C";
        return "D";
    }
    ```

3.  **Implement Background in `start` Scene:** In `main.js`, import `makeBackground` from `utils.js` and use it in your `start` scene to set a background color.

    ```javascript
    // main.js
    import kaboom from 'capl';
    import { makeBackground, goToGame } from './utils'; // Import utils

    // ... (Capl initialization) ...

    scene("start", () => {
      makeBackground(k, "#87CEEB"); // Example: Light blue background
      // ... rest of start scene logic ...
    });

    // ... (main scene definition and go("start")) ...
    ```

    > **Hexadecimal Color:** Hexadecimal color codes are a way to represent colors using a six-digit combination of numbers and letters (0-9 and A-F). Each pair of digits represents the intensity of red, green, and blue, respectively.

4.  **Style Body Background (Optional):** To remove white bars around the canvas, add a style tag in `public/index.html` to set the body background color to black:

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        </head>
    <body>
        <style>
          body { background-color: black; }
        </style>
        <script type="module" src="/src/main.js"></script>
    </body>
    </html>
    ```

### 3.2 Loading Game Assets

Game assets like sprites (images) and sounds are crucial for creating engaging games. Capl provides functions to easily load these assets.

1.  **Create an `assets` folder:** Create a folder named `assets` in the `public` directory of your project. Place all your game assets (images and sounds) inside this folder. For this Flappy Bird style game, you'll need:

    *   `background.png`
    *   `clouds.png`
    *   `creby.png` (or your player sprite)
    *   `obstacles.png`
    *   `confirm.wav` (or your confirm sound)
    *   `hit.wav`
    *   `jump.wav`
    *   `colliders_data.json`
    *   `icon.png` (optional for Windows icon)

2.  **Load Assets in `main.js`:** In `main.js`, within the Capl initialization block, use `loadSprite()` and `loadSound()` to load your assets.

    ```javascript
    import kaboom from 'capl';
    // ... (import utils etc.) ...

    kaboom({
      // ... (Capl initialization options) ...
      loadSprite: {
        "creby": "/assets/creby.png",
        "obstacles": "/assets/obstacles.png",
        "background": "/assets/background.png",
        "clouds": "/assets/clouds.png",
      },
      loadSound: {
        "jump": "/assets/jump.wav",
        "hit": "/assets/hit.wav",
        "confirm": "/assets/confirm.wav",
      }
    });

    // ... (scene definitions and go("start")) ...
    ```

    > **Sprite:** A sprite is a 2D image or animation used in games, often representing characters, objects, or background elements. Game engines efficiently render and manipulate sprites to create visual game content.

3.  **Implement Fullscreen Toggle (F11):** To enable fullscreen functionality using the F11 key, you'll need to interact with the Tori API.

    *   **Modify `tori.conf.json`:** Open `tori.conf.json` in your project's root. Under the `tori.allowlist` section, add permissions for `fs` (file system) and `window` with `setFullscreen`:

        ```json
        "allowlist": {
          "fs": {
            "readFile": true,
            "writeFile": true,
            "scope": ["$APP_LOCALDATA/*"]
          },
          "window": {
            "setFullscreen": true
          }
        },
        ```

    *   **Add Event Listener in `main.js`:** In `main.js`, import `appWindow` from `@tori.js/api` and add an event listener for the "keydown" event to toggle fullscreen on F11 press. Place this outside of any scene definition, at the top level of your `main.js` file.

        ```javascript
        import kaboom from 'capl';
        import { appWindow } from '@tori.js/api'; // Import appWindow
        // ... (import utils etc.) ...

        document.addEventListener('keydown', async (event) => {
          if (event.code === 'F11') {
            if (await appWindow.isFullscreen()) {
              await appWindow.setFullscreen(false);
            } else {
              await appWindow.setFullscreen(true);
            }
          }
        });

        kaboom({
          // ... (Capl initialization options) ...
        });

        // ... (scene definitions and go("start")) ...
        ```

## 4. Building the Start Menu Scene

The start menu scene is the first screen players see when launching the game. It typically includes the game title, a play button, and potentially other options.

### 4.1 Creating the Background and Map

1.  **Implement Background in `start` Scene (if not already done):** Ensure you have the `makeBackground` function called in your `start` scene to set a background color.

2.  **Create a `map` Game Object:** In the `start` scene's function in `main.js`, create a parent game object named `map`. This will serve as a container for background elements like the background sprite and clouds.

    ```javascript
    scene("start", () => {
      makeBackground(k, "#87CEEB");

      const map = k.add([
        k.sprite("background"),
        k.pos(0, 0),
        k.scale(4), // Example scale factor
        k.fixed(), // Optional: Make map fixed relative to camera
      ]);

      // ... (rest of start scene logic) ...
    });
    ```

    > **Game Object:** In Capl (and other game engines), a game object is a fundamental entity in a game scene. It can represent characters, objects, backgrounds, or any element that interacts within the game world. Game objects are composed of components that define their properties and behaviors.

    > **Components:** Components in Capl are reusable modules that define specific functionalities or properties of game objects. Examples include `sprite` (for rendering images), `pos` (for position), `area` (for collision detection), and `body` (for physics). Components are added to game objects using the `add` function.

3.  **Add Clouds as a Child of `map`:** Create clouds as a child game object of the `map` to make their movement relative to the background.

    ```javascript
    scene("start", () => {
      // ... (makeBackground and map creation) ...

      const clouds = map.add([
        k.sprite("clouds"),
        k.pos(0, 0),
        k.scale(4),
        k.pos(), // Positional component for setting position later
        { speed: 5 }, // Custom speed property
      ]);

      clouds.onUpdate(() => {
        clouds.move(clouds.speed, 0);
        if (clouds.pos().x > 700) {
          clouds.pos = k.vec2(-500, 0);
        }
      });

      // ... (rest of start scene logic) ...
    });
    ```

    > **`onUpdate()`:** `onUpdate()` is a Capl method that is called every frame (typically 60 times per second). It allows you to execute code that updates game object properties or performs actions based on game logic, creating animations and dynamic behavior.

### 4.2 Creating the Player Character

We'll create a reusable player character component that can be used in both the start menu and the main game scene.

1.  **Create `player.js`:** Create a new file named `player.js` in the `src` directory.

2.  **Implement `makePlayer` Function:** In `player.js`, export a function `makePlayer(k)` that defines the player game object.

    ```javascript
    // src/player.js
    import kaboom from 'capl';

    export function makePlayer(k) {
      const player = k.make([
        k.sprite("creby"),
        k.area({ shape: k.rect(8, 5), offset: k.vec2(0, 1.5) }),
        k.anchor("center"),
        k.scale(4),
        k.body(),
        {
          isDead: false,
          speed: 600,
          inputControllers: [],
          setControls() {
            const jumpLogic = () => {
              k.play("jump");
              player.jump(player.jumpForce);
            };

            this.inputControllers.push(k.onKeyPress("space", jumpLogic));
            this.inputControllers.push(k.onClick(jumpLogic));
            this.inputControllers.push(k.onGamepadButtonPress("south", jumpLogic));
          },
          disableControls() {
            this.inputControllers.forEach(controller => controller.cancel());
            this.inputControllers = [];
          }
        }
      ]);

      player.jumpForce = 600;
      player.setControls(); // Initially set controls

      return player;
    }
    ```

    > **`make()` vs. `add()`:** `make()` and `add()` are both Capl functions for creating game objects. `make()` creates a game object but does not immediately add it to the current scene. `add()` creates and adds a game object to the scene, making it visible and active. `make()` is useful for creating reusable game object templates or for objects that need to be added to the scene later.

    > **`area()` Component:** The `area()` component in Capl enables collision detection for game objects. It defines a hitbox, which is a shape that represents the object's collision boundaries. The `shape` property defines the hitbox shape (e.g., rectangle, circle), and `offset` allows you to adjust the hitbox position relative to the sprite.

    > **`anchor()` Component:** The `anchor()` component in Capl defines the point around which a game object is positioned and scaled. By default, the anchor is at the top-left corner. Setting `anchor("center")` makes the center of the sprite the origin point.

    > **`body()` Component:** The `body()` component in Capl adds physics properties to a game object, enabling it to be affected by gravity, collisions, and other physics forces. It provides methods like `jump()` for implementing jumping behavior.

    > **`onKeyPress()`, `onClick()`, `onGamepadButtonPress()`:** These are Capl input event handlers. `onKeyPress()` triggers a function when a specific key is pressed. `onClick()` triggers a function when the canvas is clicked. `onGamepadButtonPress()` triggers a function when a specific gamepad button (like "south") is pressed.

    > **Gamepad "South Button":** In Capl, "south" refers to the bottom button on a standard gamepad controller layout. This naming convention allows for controller-agnostic input handling, as button labels may vary between Xbox, PlayStation, and other controllers.

3.  **Add Player to `start` Scene:** In `main.js`, import `makePlayer` from `player.js` and add the player to the `start` scene.

    ```javascript
    // main.js
    import kaboom from 'capl';
    import { makeBackground, goToGame } from './utils';
    import { makePlayer } from './player'; // Import makePlayer

    // ... (Capl initialization and scene("start") logic) ...

    scene("start", () => {
      // ... (makeBackground, map, clouds) ...

      const player = k.add(makePlayer(k));
      player.pos = k.vec2(k.center().x - 100, k.center().y + 50); // Example position

      // ... (rest of start scene logic) ...
    });

    // ... (main scene definition and go("start")) ...
    ```

### 4.3 Creating the Play Button and Scene Transition

1.  **Create the Play Button:** In the `start` scene in `main.js`, create a play button game object.

    ```javascript
    scene("start", () => {
      // ... (makeBackground, map, clouds, player) ...

      const playButton = k.add([
        k.rect(120, 40, { radius: 3 }),
        k.color(k.rgb(50, 50, 50)),
        k.pos(k.center().x + 100, k.center().y + 50),
        k.anchor("center"),
        k.area(),
        k.outline(2, k.rgb(100, 100, 100)),
      ]);

      playButton.add([
        k.text("Play", { size: 24 }),
        k.color(k.rgb(200, 200, 200)),
        k.anchor("center"),
      ]);

      // ... (rest of start scene logic) ...
    });
    ```

    > **`rect()` Component:** The `rect()` component in Capl renders a rectangle shape. You can customize its width, height, color, and other properties. The `radius` option allows you to create rounded rectangles.

    > **`text()` Component:** The `text()` component in Capl renders text on the canvas. You can customize the text content, size, font, color, and other text properties.

    > **`outline()` Component:** The `outline()` component in Capl adds an outline (border) to a game object. You can customize the outline width and color.

2.  **Implement Scene Transition Logic:** Add input event handlers to the play button to transition to the `main` scene when clicked, or when specific keys or gamepad buttons are pressed.

    ```javascript
    scene("start", () => {
      // ... (makeBackground, map, clouds, player, playButton) ...

      const startGame = () => {
        k.play("confirm");
        goToGame(k); // Use the goToGame utility function
      };

      playButton.onClick(startGame);
      k.onKeyPress("enter", startGame);
      k.onGamepadButtonPress("south", startGame);

      // ... (rest of start scene logic) ...
    });
    ```

## 5. Implementing Game Saving and Loading

Desktop games often benefit from save systems, allowing players to preserve their progress. We'll implement a simple save system to store the player's best score.

### 5.1 Creating the Save System Utility

1.  **Create `save.js`:** Create a new file named `save.js` in the `src` directory.

2.  **Implement `makeSaveSystem` Function:** In `save.js`, export a function `makeSaveSystem(saveFileName)` that encapsulates the save system logic.

    ```javascript
    // src/save.js
    import { writeTextFile, readTextFile, BaseDirectory } from '@tori.js/api';

    export function makeSaveSystem(saveFileName) {
      return {
        data: {},
        async save() {
          try {
            await writeTextFile(saveFileName, JSON.stringify(this.data), {
              dir: BaseDirectory.AppDataLocal,
            });
          } catch (e) {
            console.error("Save failed:", e);
          }
        },
        async load() {
          try {
            const contents = await readTextFile(saveFileName, {
              dir: BaseDirectory.AppDataLocal,
            });
            this.data = JSON.parse(contents);
          } catch (e) {
            console.warn("Save file not found or corrupted, using default data.");
            this.data = {}; // Default data if loading fails
          }
        },
      };
    }
    ```

    > **`@tori.js/api`:** `@tori.js/api` is the Tori JavaScript API package. It provides access to native system functionalities from JavaScript code within a Tori application, including file system operations, window management, and more.

    > **`writeTextFile()`, `readTextFile()`, `BaseDirectory`:** These are functions and enums from `@tori.js/api` for interacting with the file system. `writeTextFile()` writes text content to a file. `readTextFile()` reads text content from a file. `BaseDirectory.AppDataLocal` specifies the application's local data directory as the storage location.

    > **`JSON.stringify()`, `JSON.parse()`:** `JSON.stringify()` converts a JavaScript object into a JSON string, which is suitable for saving in text files. `JSON.parse()` converts a JSON string back into a JavaScript object when loading data.

### 5.2 Integrating Save System into `start` Scene

1.  **Import `makeSaveSystem` in `main.js`:** In `main.js`, import `makeSaveSystem` from `save.js`.

2.  **Initialize Save System in `start` Scene:** In the `start` scene's function, initialize the save system and load existing data.

    ```javascript
    // main.js
    import kaboom from 'capl';
    import { makeBackground, goToGame } from './utils';
    import { makePlayer } from './player';
    import { makeSaveSystem } from './save'; // Import makeSaveSystem

    // ... (Capl initialization and scene("start") logic) ...

    scene("start", async () => { // Make scene function async
      // ... (makeBackground, map, clouds, player, playButton) ...

      const saveSystem = makeSaveSystem("save.json");
      await saveSystem.load(); // Load saved data

      if (saveSystem.data.maxScore === undefined) {
        saveSystem.data.maxScore = 0;
        await saveSystem.save(); // Save initial maxScore
      }

      // ... (rest of start scene logic, potentially display maxScore from saveSystem.data) ...
    });

    // ... (main scene definition and go("start")) ...
    ```

    > **Asynchronous Functions (`async`, `await`):** `async` functions in JavaScript are functions that can perform asynchronous operations, such as file I/O or network requests. `await` is used inside `async` functions to pause execution until a Promise (representing an asynchronous operation) resolves, making asynchronous code easier to read and write.

### 5.3 Displaying Max Score in Start Menu (Optional)

You can display the player's max score in the start menu by retrieving it from `saveSystem.data` and using the `text()` component.

## 6. Building the Main Game Scene

The main game scene contains the core gameplay logic. For our Flappy Bird style game, this involves obstacle generation, player movement, collision detection, and scoring.

### 6.1 Scene Initialization and Assets

1.  **Basic Structure of `main` Scene:** In `main.js`, define the basic structure of the `main` scene function.

    ```javascript
    scene("main", async () => { // Make main scene async
      makeBackground(k, "#7ac0ee"); // Different background color for game

      // ... (rest of main scene logic) ...
    });
    ```

2.  **Load Collider Data:** Fetch and parse the `colliders_data.json` file to get obstacle hitbox information.

    ```javascript
    scene("main", async () => {
      makeBackground(k, "#7ac0ee");

      const response = await fetch("/assets/colliders_data.json");
      const collidersDataJson = await response.json();
      const collidersData = collidersDataJson.data; // Access the 'data' array

      // ... (rest of main scene logic) ...
    });
    ```

### 6.2 Implementing Game Objects: Map, Platforms, and Walls

1.  **Create `map` and `platforms` Game Objects:** Similar to the start menu, create a `map` game object and add platforms (obstacles) as its child.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground and collider data loading) ...

      const map = k.add([
        k.sprite("background"),
        k.pos(0, 0),
        k.scale(4),
        k.fixed(),
      ]);

      const platforms = map.add([
        k.sprite("obstacles"),
        k.pos(k.width(), 0), // Start off-screen to the right
        k.scale(4),
        k.pos(), // Positional component for setting position later
        { speed: -200 }, // Move to the left
      ]);

      platforms.onUpdate(() => {
        platforms.move(platforms.speed, 0);
        if (platforms.pos().x < -1200) {
          platforms.pos = k.vec2(k.width(), 0);
          platforms.speed -= 10; // Increase speed over time
        }
      });

      // ... (rest of main scene logic) ...
    });
    ```

2.  **Add Hitboxes to Platforms:** Iterate through the `collidersData` and create child game objects for each hitbox, adding them to the `platforms` game object.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms) ...

      for (const collider of collidersData) {
        platforms.add([
          k.rect(collider.width, collider.height),
          k.pos(collider.x, collider.y),
          k.area(),
          k.body({ isStatic: true }),
          k.color(k.rgba(0, 0, 0, 0)), // Make hitbox invisible
          k.layer('obstacle'), // Assign to obstacle layer
          k.tag('obstacle'), // Tag for collision detection
        ]);
      }

      // ... (rest of main scene logic) ...
    });
    ```

    > **`body({ isStatic: true })`:** The `body()` component with `isStatic: true` creates a static physics body. Static bodies do not move in response to forces or collisions, making them suitable for obstacles and platforms in games.

    > **`tag()` Component:** The `tag()` component allows you to assign tags (string identifiers) to game objects. Tags are used for grouping game objects and efficiently identifying them in collision detection or other game logic scenarios.

3.  **Create Top and Bottom Walls:** Add invisible rectangular game objects at the top and bottom of the screen to act as boundaries.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms, platform hitboxes) ...

      k.add([
        k.rect(k.width(), 1),
        k.pos(0, 0),
        k.area(),
        k.body({ isStatic: true }),
        k.color(k.rgba(0, 0, 0, 0)), // Invisible
        k.tag('obstacle'),
      ]);

      k.add([
        k.rect(k.width(), 1),
        k.pos(0, k.height() - 1),
        k.area(),
        k.body({ isStatic: true }),
        k.color(k.rgba(0, 0, 0, 0)), // Invisible
        k.tag('obstacle'),
      ]);

      // ... (rest of main scene logic) ...
    });
    ```

### 6.3 Adding the Player and Collision Detection

1.  **Add Player to `main` Scene:** Add the player game object to the `main` scene.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms, walls) ...

      const player = k.add(makePlayer(k));
      player.pos = k.vec2(600, 250);

      // ... (rest of main scene logic) ...
    });
    ```

2.  **Implement Collision Detection:** Use `player.onCollide()` to handle collisions between the player and obstacles.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms, walls, player) ...

      let score = 0;

      player.onCollide("obstacle", () => {
        if (!player.isDead) {
          k.play("hit");
          platforms.speed = 0;
          player.disableControls();
          player.isDead = true;
          // ... (create score box and game over logic - see next section) ...
        }
      });

      // ... (rest of main scene logic, including score increment logic) ...
    });
    ```

    > **`onCollide()` Method:** `onCollide()` is a method available on game objects with the `area()` component. It allows you to define a callback function that is executed when the game object collides with another game object that has a specific tag.

### 6.4 Implementing Scoring and Game Over

1.  **Implement Score Increment:** Use `k.loop()` to increment the score every second.

    ```javascript
    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms, walls, player, collision detection) ...

      let score = 0;

      k.loop(1, () => { // Run every 1 second
        if (!player.isDead) {
          score++;
        }
      });

      // ... (collision detection and rest of main scene logic) ...
    });
    ```

    > **`k.loop()` Function:** `k.loop(time, callback)` is a Capl function that executes a callback function repeatedly at a specified time interval (in seconds). It is useful for implementing timed events or actions in a game.

2.  **Create Score Box Utility (`scorebox.js`):** Create a new file `scorebox.js` in `src` to implement the score display box that appears when the game is over.

    ```javascript
    // src/scorebox.js
    import kaboom from 'capl';
    import { goToGame, computeRank } from './utils';
    import { makeSaveSystem } from './save';

    export async function makeScoreBox(k, pos, score) {
      const saveSystem = makeSaveSystem("save.json");
      await saveSystem.load();

      if (score > (saveSystem.data.maxScore || 0)) {
        saveSystem.data.maxScore = score;
        await saveSystem.save();
      }

      const container = k.make([
        k.pos(pos),
        k.fixed(), // Optional: Make score box fixed relative to camera
      ]);

      const box = container.add([
        k.rect(240, 180, { radius: 6 }),
        k.color(k.rgb(80, 80, 80)),
        k.anchor("center"),
        k.outline(2, k.rgb(120, 120, 120)),
      ]);

      box.add([
        k.text("Game Over!", { size: 24 }),
        k.color(k.rgb(220, 220, 220)),
        k.pos(0, -60),
        k.anchor("center"),
      ]);

      box.add([
        k.text(`Previous Best: ${saveSystem.data.maxScore || 0}`, { size: 16 }),
        k.color(k.rgb(180, 180, 180)),
        k.pos(0, -20),
        k.anchor("center"),
      ]);

      box.add([
        k.text(`Current Score: ${score}`, { size: 16 }),
        k.color(k.rgb(180, 180, 180)),
        k.pos(0, 10),
        k.anchor("center"),
      ]);

      box.add([
        k.text(`Rank: ${computeRank(score)}`, { size: 16 }),
        k.color(k.rgb(180, 180, 180)),
        k.pos(0, 40),
        k.anchor("center"),
      ]);

      const restartButton = box.add([
        k.rect(100, 30, { radius: 4 }),
        k.color(k.rgb(50, 50, 50)),
        k.pos(0, 90),
        k.anchor("center"),
        k.area(),
        k.outline(1, k.rgb(100, 100, 100)),
      ]);

      restartButton.add([
        k.text("Play Again", { size: 14 }),
        k.color(k.rgb(200, 200, 200)),
        k.anchor("center"),
      ]);

      const restartGame = () => {
        k.play("confirm");
        goToGame(k); // Use goToGame utility function
      };

      restartButton.onClick(restartGame);
      k.onKeyPress("enter", restartGame);
      k.onGamepadButtonPress("south", restartGame);

      return container;
    }
    ```

3.  **Import and Call `makeScoreBox` in `main.js`:** In `main.js`, import `makeScoreBox` and call it within the `player.onCollide()` callback to display the score box when the player collides with an obstacle.

    ```javascript
    // main.js
    import kaboom from 'capl';
    import { makeBackground, goToGame } from './utils';
    import { makePlayer } from './player';
    import { makeSaveSystem } from './save';
    import { makeScoreBox } from './scorebox'; // Import makeScoreBox

    // ... (scene("main") logic) ...

    scene("main", async () => {
      // ... (makeBackground, collider data loading, map, platforms, walls, player, score increment) ...

      let score = 0;

      player.onCollide("obstacle", () => {
        if (!player.isDead) {
          k.play("hit");
          platforms.speed = 0;
          player.disableControls();
          player.isDead = true;
          k.add(await makeScoreBox(k, k.center(), score)); // Call makeScoreBox
        }
      });

      // ... (score increment and rest of main scene logic) ...
    });

    // ... (go("start") call) ...
    ```

## 7. Building and Distributing Your Game

With the game logic implemented, the final step is to build your desktop application and prepare it for distribution.

### 7.1 Building the Executable

1.  **Run the Build Command:** In your terminal, navigate to your project directory and run the build command:

    ```bash
    npm run build
    ```

    This command will compile your project and package it into an executable file. The build process may take some time, especially for the first build.

2.  **Locate the Executable:** After the build process completes successfully, the executable file will be located in the `src-tori/target/release/bundle` directory within your project. You will find installer files like `.msi` (for Windows Installer) and `.nsis.zip` (for NSIS installer).

    > **MSI (Microsoft Installer):** MSI is a file format used by the Windows Installer service for installing, maintaining, and removing programs on Windows operating systems. MSI files are commonly used for distributing Windows applications.

### 7.2 Distributing Your Game

To distribute your game, you should provide users with the installer file (e.g., the `.msi` or `.nsis.zip` from the `bundle` directory). Distributing the installer ensures that necessary dependencies like Webview2 Runtime are installed on the user's machine if they are not already present.

You can distribute your game through platforms like:

*   **itch.io:** A popular platform for indie game distribution.
*   **Steam:** A major platform for game distribution, though it has a more involved submission and approval process.
*   **Your own website or file sharing services.**

### 7.3 Setting Application Description (Optional)

To customize the application description that appears when users hover over the executable, you can modify the `shortDescription` property in `tori.conf.json` within the `bundle` section.

```json
"bundle": {
    "shortDescription": "Your game description here",
    // ... other bundle configurations ...
}
```

## Conclusion: Your First Desktop Game in JavaScript

Congratulations! You have successfully built a desktop game using JavaScript with Capl and Tori. This chapter has covered the essential steps, from setting up your development environment to building and preparing your game for distribution.

By leveraging the power of JavaScript and frameworks like Tori and libraries like Capl, you can now expand your game development capabilities beyond the web browser and create engaging desktop gaming experiences. This opens new possibilities for game distribution, save systems, and reaching a wider audience.

Continue exploring the capabilities of Capl and Tori, experiment with different game mechanics, and expand your knowledge of JavaScript game development to create even more complex and compelling desktop games in the future.

