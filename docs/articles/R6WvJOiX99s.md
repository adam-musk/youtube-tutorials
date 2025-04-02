---
layout: "../../layouts/BlogPost.astro"
title: "Building a Kirby-like Platformer Game with TypeScript and Kaboom.js"
pubDate: "2025-03-02 14:15:29.007624"
youtubeVideoID: "R6WvJOiX99s"
index:
---

# Building a Kirby-like Platformer Game with TypeScript and Kaboom.js

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/R6WvJOiX99s" frameborder="0" allowfullscreen></iframe>

This chapter will guide you through the process of creating a 2D platformer game similar to Kirby, using TypeScript and the Kaboom.js library. We will cover project setup, asset loading, level design, character implementation, enemy creation, and game mechanics. This tutorial assumes a basic understanding of TypeScript and Node.js.

## 1. Introduction to Kaboom.js and Project Setup

Kaboom.js is a JavaScript library designed for making games quickly and easily. It's particularly well-suited for 2D games and integrates seamlessly with TypeScript.

> **Kaboom.js:** A simple and fun JavaScript library for making games in the browser. It is designed to be beginner-friendly and offers a wide range of features for 2D game development.

This tutorial utilizes **Vite** as a bundler for project setup. Unlike traditional setups involving `index.html` and script tags, Vite simplifies the process and offers features like hot module replacement and optimized builds.

> **Bundler:** A tool in web development that combines and packages JavaScript modules, CSS, and other assets into optimized bundles for deployment. This process often includes tasks like minification and code transformation.

### 1.1 Prerequisites

*   **Basic understanding of TypeScript:** Familiarity with TypeScript syntax, types, and concepts is essential.
*   **Node.js and npm (Node Package Manager):** Node.js runtime environment and npm for package management are required.

### 1.2 Setting up the Project with Vite

1.  **Open a terminal:** Navigate to the directory where you want to create your project.
2.  **Run the Vite create command:** Execute the following command in your terminal:

    ```bash
    npm create vite@latest .
    ```

    The `.` at the end specifies that the project should be scaffolded in the current directory.
3.  **Select template:** When prompted, choose the following options:
    *   **Vanilla** template
    *   **TypeScript** template
4.  **Project files:** After successful execution, you should have a basic project structure with files like `package.json`, `tsconfig.json`, and a `src` folder.
5.  **Clean up:**
    *   Delete `vite.svg` (optional).
    *   Delete all files within the `src` folder, but keep the `src` folder itself.

### 1.3 Installing Dependencies

1.  **Navigate to the project directory:** Ensure you are in the newly created project directory in your terminal.
2.  **Install dependencies:** Run the command:

    ```bash
    npm install
    ```

    This command installs all the dependencies listed in your `package.json` file.
3.  **Install Kaboom.js:** Install the Kaboom.js library specifically using:

    ```bash
    npm install kaboom
    ```

    This makes Kaboom.js available for import and use in your project.

### 1.4 Project File Structure

Create the following files within the `src` folder to organize your project:

*   `constants.ts`:  For storing constant values like game scale and resolution.
*   `entities.ts`:  To define game entities like players, enemies, and projectiles, along with their logic.
*   `kaboom-cx.ts`:  To initialize the Kaboom.js context and export it for use in other files.
*   `main.ts`:  The main entry point of your game application.
*   `state.ts`:  For managing the global game state, such as scene transitions and game over conditions.
*   `utils.ts`:  For utility functions, in this case, primarily for map loading and processing.

## 2. Initializing Kaboom.js Context

The `kaboom-cx.ts` file is crucial for setting up the Kaboom.js environment.

1.  **Import Kaboom:** In `kaboom-cx.ts`, import the Kaboom function:

    ```typescript
    import kaboom from 'kaboom';
    ```

2.  **Initialize and Export Context:** Initialize Kaboom with desired configurations and export the context.

    ```typescript
    import kaboom from 'kaboom';

    export const k = kaboom({
        width: 256,
        height: 144,
        letterbox: true,
        global: false,
        scale: 4,
    });
    ```

    *   `width`: Sets the width of the game canvas in pixels.
    *   `height`: Sets the height of the game canvas in pixels.  The resolution (256x144) is chosen to resemble the Game Boy, but with a wider 16:9 aspect ratio.
    *   `letterbox: true`: Ensures the canvas scales proportionally to different screen sizes while maintaining the aspect ratio, adding letterboxing if necessary.
    *   `global: false`: Prevents Kaboom.js functions from being globally available.  This enforces using the exported context `k` for all Kaboom.js operations, promoting better code organization and avoiding namespace pollution.
    *   `scale: 4`:  Scales the game up by a factor of 4. This is used both to enlarge the game visually and as a workaround for a pixel rendering issue in Kaboom.js.

3.  **Define Scale Constant (constants.ts):** Create a constant for the game scale in `constants.ts`.

    ```typescript
    export const SCALE = 4;
    ```

    Import this `SCALE` constant into `kaboom-cx.ts` and use it to set the `scale` option and also multiply the `width` and `height` options (though in this example, the multiplication is applied later to the resolution values, not directly in the `kaboom()` initialization).

## 3. Loading Game Assets (main.ts)

Assets like sprites and tile sets are essential for game visuals. Kaboom.js provides functions to load these assets.

### 3.1 Asynchronous Game Setup

To manage asset loading efficiently, especially for map data from external sources, an asynchronous `gameSetup` function is used in `main.ts`.

```typescript
import * as k from './kaboom-cx';

async function gameSetup() {
    // Asset loading logic will go here
    await loadAssets(); // Function to load sprites and level data
    k.k.go('level1'); // Transition to the 'level1' scene after setup
}

gameSetup();
```

Using `async` and `await` ensures that assets are fully loaded before the game scene starts, preventing issues like missing sprites or incomplete level data. This is particularly important for fetching external JSON map data.

### 3.2 Loading Sprites

Spritesheets, which contain multiple sprite frames in a single image, are common in 2D game development. Kaboom.js's `loadSprite` function handles loading and slicing spritesheets.

```typescript
async function loadAssets() {
    k.k.loadSpriteAtlas("kirbylike", 'assets/kirbylike.png', {
        'kirbyidle': { x: 0, y: 0, width: 16, height: 16 },
        'kirbyinhale': { x: 16, y: 0, width: 16, height: 16 },
        'kirbyfull': { x: 32, y: 0, width: 16, height: 16 },
        'kirbywalk': { x: 48, y: 0, width: 16, height: 16, frames: 9, animSpeed: 0.1 },
        'kirbyjump': { x: 144, y: 0, width: 16, height: 16 },
        'kirbyfall': { x: 160, y: 0, width: 16, height: 16 },
        'star': { x: 176, y: 0, width: 16, height: 16 },
        'flame': { x: 192, y: 0, width: 16, height: 16, frames: 6, animSpeed: 0.1 },
        'guy': { x: 288, y: 0, width: 16, height: 16, frames: 4, animSpeed: 0.1 },
        'bird': { x: 352, y: 0, width: 16, height: 16, frames: 4, animSpeed: 0.1 },
        'cloud': { x: 384, y: 0, width: 16, height: 16 },
        'hill': { x: 400, y: 0, width: 16, height: 16 },
        'grass': { x: 432, y: 0, width: 16, height: 16 },
        'sign': { x: 448, y: 0, width: 16, height: 16 },
        'door': { x: 464, y: 0, width: 16, height: 16 },
    });
    k.k.loadSprite("level1", 'assets/level-1.png');
}
```

*   `k.k.loadSpriteAtlas("kirbylike", 'assets/kirbylike.png', {...})`: Loads a spritesheet named "kirbylike" from the `assets/kirbylike.png` file. The second argument is a configuration object defining individual sprites within the sheet, including their positions (`x`, `y`), dimensions (`width`, `height`), and animation properties (`frames`, `animSpeed`).
*   `k.k.loadSprite("level1", 'assets/level-1.png')`: Loads a single sprite named "level1" from `assets/level-1.png`. This will be used for the level background image.

    > **Sprite:** A 2D image or animation frame used in games to represent characters, objects, or visual elements.
    > **Spritesheet (or Sprite Atlas):** A single image file containing multiple sprites arranged in a grid. This is an efficient way to load and manage numerous sprites.

## 4. Level Design with Tiled and JSON Export

**Tiled** is a powerful and free tile map editor. It's used to design game levels visually and export them in various formats, including JSON, which is ideal for Kaboom.js.

> **Tiled:** A free and open-source tile map editor. It allows game developers to create levels using tilesets and layers, and export them in various formats suitable for game engines.

### 4.1 Using Tiled Editor

1.  **Install Tiled:** Download and install Tiled from its official website.
2.  **Configure Font Size (Optional):** If using a high-resolution monitor, adjust the interface font size in Tiled's preferences (Edit > Preferences > Themes > Use custom interface font) for better visibility.
3.  **Create a New Map:**
    *   File > New > New Map.
    *   Set map dimensions (e.g., 27x20 tiles).
    *   Set tile size (e.g., 16x16 pixels).
4.  **Import Tile Set:**
    *   Tile Sets > New Tile Set.
    *   Browse to your `assets/kirbylike.png` file as the source.
    *   Set tile size to 16x16 pixels.
5.  **Create Layers:** Tiled supports different layer types:
    *   **Tile Layers:** For background, platforms, clouds, and other tile-based elements. Create layers for "background," "clouds," and "platforms."
    *   **Object Layers:** For colliders, spawn points, and other game logic elements. Create layers for "colliders" and "spawn points."
6.  **Draw the Level:** Use the tile sets and layers to visually design your level within Tiled.
    *   **Background Layer:** Draw the background elements (hills, ground, etc.).
    *   **Clouds Layer:** Add cloud tiles for visual depth.
    *   **Platforms Layer:** Create platforms for the player to jump on.
    *   **Colliders Layer:** Use rectangle objects to define collision areas for platforms and level boundaries. Name the exit collider object as "exit".
    *   **Spawn Points Layer:** Use point objects (pins) to mark spawn locations for:
        *   `player`: Player starting position.
        *   `flame`: Flame enemy spawn points.
        *   `bird`: Bird enemy spawn points.
        *   `guy`: Guy enemy spawn points.
7.  **Save the Map:** File > Save As... Save the map as `level-1.json` in the `public` folder of your project.
8.  **Export Level Image:** For optimized rendering, export the visible layers (hide "spawn points" and "colliders" layers) as a single PNG image:
    *   File > Export As Image...
    *   Save as `level-1.png` in the `public` folder, ensuring "Only include visible layers" is checked and other options are unchecked.

    > **Tile Set:** A collection of tiles (small images) used to construct tile maps in game development.
    > **Tile Map:** A level or game world created by arranging tiles from a tile set on a grid.
    > **Layer:** A level in a tile map editor can be composed of multiple layers. Layers can be of tile type, object type, or image type, allowing for organized level design.
    > **Collider:** An invisible shape used for collision detection in games. Colliders define the boundaries of objects for interaction and physics.
    > **Spawn Point:** A designated location in a game level where characters or objects are created or appear.

## 5. Loading and Rendering the Level (utils.ts & main.ts)

To display the level created in Tiled, we need to load the JSON data and the exported PNG image in Kaboom.js.

### 5.1 `makeMap` Utility Function (utils.ts)

Create a utility function `makeMap` in `utils.ts` to handle loading and processing the Tiled JSON map data.

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';

export async function makeMap(context: k.KaboomCtx, name: string) {
    const mapData = await fetch(`./${name}.json`).then(res => res.json());
    const map = k.k.make([
        k.k.sprite(name),
        k.k.scale(SCALE),
        k.k.pos(0, 0),
    ]);

    const spawnPoints: Record<string, { x: number, y: number }[]> = {};

    for (const layer of mapData.layers) {
        if (layer.name === 'colliders') {
            for (const collider of layer.objects) {
                const childCollider = k.k.add([
                    k.k.area({ shape: new k.k.Rect(k.k.vec2(0, 0), collider.width, collider.height), collisionIgnore: ['platform', 'exit'] }),
                    collider.name !== 'exit' ? k.k.body({ isStatic: true }) : null,
                    k.k.pos(collider.x, collider.y),
                    collider.name !== 'exit' ? 'platform' : 'exit',
                ]);
                map.add(childCollider);
            }
        } else if (layer.name === 'spawn points') {
            for (const spawnPoint of layer.objects) {
                if (spawnPoints[spawnPoint.name]) {
                    spawnPoints[spawnPoint.name].push({ x: spawnPoint.x, y: spawnPoint.y });
                } else {
                    spawnPoints[spawnPoint.name] = [{ x: spawnPoint.x, y: spawnPoint.y }];
                }
            }
        }
    }

    return { map, spawnPoints };
}
```

*   `fetch(`./${name}.json`).then(res => res.json())`: Fetches the JSON map data from the `public` folder using the `name` parameter (e.g., "level-1").

    > **JSON (JavaScript Object Notation):** A lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate. It is often used for configuration files and data transfer over the internet.

*   `k.k.make(...)`: Creates a Kaboom.js game object for the map itself.
    *   `k.k.sprite(name)`: Adds the sprite component, using the `name` (e.g., "level-1") to reference the loaded PNG image.
    *   `k.k.scale(SCALE)`: Applies the game's scale factor to the map sprite.
    *   `k.k.pos(0, 0)`: Sets the map's position to the top-left corner (0, 0).
*   **Collider Processing:** Iterates through the "colliders" layer in the JSON data. For each collider object:
    *   `k.k.area({...})`: Adds an area component to define the collider's shape and collision behavior.
        *   `shape: new k.k.Rect(...)`: Creates a rectangular shape based on the collider's width and height from Tiled.
        *   `collisionIgnore: ['platform', 'exit']`: Specifies tags to ignore during collision detection.
    *   `collider.name !== 'exit' ? k.k.body({ isStatic: true }) : null`: Conditionally adds a body component with `isStatic: true` for platform colliders. Static bodies do not move or respond to forces, making them suitable for platforms and walls. The exit collider does not need a body component.

        > **Component:** In Kaboom.js (and ECS architectures), a component is a data container that adds specific functionalities or attributes to a game object. Examples include SpriteComponent, PosComponent, AreaComponent, BodyComponent, etc.
        > **Static Body:** In physics engines, a static body is an object that is fixed in place and does not move or react to forces or collisions. It is often used for level geometry like platforms and walls.

    *   `k.k.pos(collider.x, collider.y)`: Sets the collider's position based on the coordinates from Tiled.
    *   `collider.name !== 'exit' ? 'platform' : 'exit'`: Assigns tags "platform" or "exit" to the collider game object for collision identification.
    *   `map.add(childCollider)`: Adds the created collider as a child of the map game object. This ensures that colliders are rendered and positioned relative to the map.
*   **Spawn Point Processing:** Iterates through the "spawn points" layer. For each spawn point object:
    *   Extracts the spawn point's name (e.g., "player," "flame") and position (`x`, `y`).
    *   Stores the spawn point data in the `spawnPoints` object, grouping spawn points by their names.
*   `return { map, spawnPoints }`: Returns the created map game object and the `spawnPoints` data.

### 5.2 Integrating `makeMap` into the Scene (main.ts)

In `main.ts`, within the `level1` scene, call the `makeMap` function to load and add the level to the scene.

```typescript
import * as k from './kaboom-cx';
import { makeMap } from './utils';
import { makePlayer, setControls } from './entities';

k.k.scene('level1', async () => {
    k.k.setGravity(2100);

    // Background Rectangle
    k.k.add([
        k.k.rect(k.k.width(), k.k.height()),
        k.k.color('#a0c4ff'),
        k.k.fixed(),
    ]);

    // Load Level Layout and Spawn Points
    const { map: levelLayout, spawnPoints: level1SpawnPoints } = await makeMap(k.k, 'level-1');
    k.k.add(levelLayout);

    // Create Player
    const player = makePlayer(k.k, level1SpawnPoints.player[0].x, level1SpawnPoints.player[0].y);
    k.k.add(player);
    setControls(k.k, player);

    // Camera Follow Logic
    k.k.camScale(0.7);
    k.k.onUpdate(() => {
        if (player.pos.x < levelLayout.pos.x + 432) {
            k.k.camPos(player.pos.x + 500, 850);
        }
    });
});

k.k.start('level1');
```

*   `const { map: levelLayout, spawnPoints: level1SpawnPoints } = await makeMap(k.k, 'level-1')`: Calls `makeMap` to load the level data for "level-1". It uses object destructuring with renaming (`map: levelLayout`, `spawnPoints: level1SpawnPoints`) to assign the returned values to more descriptive variable names.
*   `k.k.add(levelLayout)`: Adds the map game object (`levelLayout`) to the scene, rendering the level image and its child colliders.

## 6. Implementing the Player Character (entities.ts)

The `entities.ts` file houses the logic for game entities.  Let's start by creating the player character.

### 6.1 `makePlayer` Function

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';

export type PlayerGameObject = k.GameObject<k.SpriteComp | k.AreaComp | k.BodyComp | k.PosComp | k.ScaleComp | k.DoubleJumpComp | k.HealthComp | k.OpacityComp> & {
    speed: number;
    direction: 'left' | 'right';
    isFull: boolean;
    isInhaling: boolean;
};

export function makePlayer(context: k.KaboomCtx, posX: number, posY: number): PlayerGameObject {
    const player = k.k.make([
        k.k.sprite('kirbyidle', { anim: 'kirbyidle' }),
        k.k.area({ shape: new k.k.Rect(k.k.vec2(4, 5.9), 8, 10) }),
        k.k.body(),
        k.k.pos(posX * SCALE, posY * SCALE),
        k.k.scale(SCALE),
        k.k.doubleJump(10),
        k.k.health(3),
        k.k.opacity(1),
        {
            speed: 120,
            direction: 'right',
            isFull: false,
            isInhaling: false,
        },
        'player',
    ]);

    player.onCollide('enemy', async (enemy) => {
        if (player.isInhaling && enemy.isSwallowable) {
            player.isInhaling = false;
            k.k.destroy(enemy);
            player.isFull = true;
            return;
        }

        if (player.hp() <= 0) {
            k.k.destroy(player);
            k.k.go('level1');
            return;
        }

        player.hurt(1);
        await k.k.tween(0.5, (t) => {
            player.opacity = k.k.lerp(1, 0, t);
        }, k.k.easings.linear);

        await k.k.tween(0.5, (t) => {
            player.opacity = k.k.lerp(0, 1, t);
        }, k.k.easings.linear);
    });

    player.onCollide('exit', () => {
        k.k.go('level2'); // Placeholder, level 2 is not implemented in this tutorial.
    });

    // Inhale Effect and Zone (defined later in the transcript)
    const inhaleEffect = k.k.add([ /* ... inhale effect object ... */ ]);
    const inhaleZone = k.k.add([ /* ... inhale zone object ... */ ]);

    k.k.onUpdate(() => { /* ... inhale zone and effect update logic ... */ });
    k.k.onUpdate(() => { /* ... respawn logic if player falls ... */ });

    return player as PlayerGameObject;
}
```

*   **`PlayerGameObject` Type:** Defines a TypeScript type `PlayerGameObject` to ensure type safety for the player object. It specifies that the player object is a Kaboom.js `GameObject` with specific components (`SpriteComp`, `AreaComp`, etc.) and custom properties (`speed`, `direction`, `isFull`, `isInhaling`).

    > **TypeScript Type:** In TypeScript, a type defines the kind of values that can be assigned to a variable or used in a function. It helps in catching type-related errors during development and improves code readability.

*   `k.k.make(...)`: Creates the player game object with the specified components:
    *   `k.k.sprite('kirbyidle', { anim: 'kirbyidle' })`: Adds the sprite component, using the "kirbyidle" sprite and playing the "kirbyidle" animation by default.
    *   `k.k.area({...})`: Adds an area component for collision detection, defining a rectangular shape for the player's hitbox.
    *   `k.k.body()`: Adds a body component, enabling physics and collision resolution.
    *   `k.k.pos(posX * SCALE, posY * SCALE)`: Sets the player's initial position, scaled by the `SCALE` constant.
    *   `k.k.scale(SCALE)`: Scales the player sprite.
    *   `k.k.doubleJump(10)`: Adds the double jump component, allowing the player to jump multiple times in the air (simulating Kirby's float ability).
    *   `k.k.health(3)`: Adds the health component, setting the player's initial health to 3.
    *   `k.k.opacity(1)`: Sets the player's initial opacity to fully visible.
    *   `{...}`: An anonymous object containing custom properties: `speed`, `direction`, `isFull`, `isInhaling`, and their initial values.
    *   `'player'`: Assigns the "player" tag to the player game object.
*   **`player.onCollide('enemy', async (enemy) => { ... })`:**  Sets up a collision event handler for collisions between the player and game objects tagged as "enemy."

    > **Event Handler:** A function that is executed when a specific event occurs, such as a collision, key press, or mouse click. In Kaboom.js, `onCollide`, `onKeyPress`, and `onUpdate` are examples of event handlers.

    *   **Inhale Logic:** Checks if the player is inhaling and the enemy is swallowable (`enemy.isSwallowable`). If both are true, it sets `player.isInhaling` to false, destroys the enemy using `k.k.destroy(enemy)`, and sets `player.isFull` to true (indicating the player has swallowed an enemy).
    *   **Damage and Respawn Logic:** If the player's health (`player.hp()`) is zero or less, it destroys the player and restarts the current level (`k.k.go('level1')`). Otherwise, it reduces the player's health by 1 (`player.hurt(1)`) and initiates a blinking effect using tweens.

        > **Tween (Short for In-Betweening):** An animation technique that smoothly transitions a property of an object from one value to another over a specified duration. Tweens are often used for animation, visual effects, and smooth transitions in games.

    *   **Blinking Effect:** Uses two `k.k.tween` calls to create a blink effect when the player takes damage. The first tween reduces opacity from 1 to 0, and the second tween increases it back from 0 to 1, both over 0.5 seconds with linear easing.

        > **Easing Function:** A function that defines the rate of change of a value in a tween over time. Linear easing means a constant rate of change, while other easing functions (e.g., ease-in, ease-out) create more dynamic and visually appealing transitions.

*   **`player.onCollide('exit', () => { ... })`:** Sets up a collision event handler for collisions with game objects tagged as "exit." When the player collides with the exit, it attempts to transition to a "level2" scene (which is a placeholder in this tutorial).
*   **Inhale Effect and Zone (Placeholder):** The code for creating the inhale effect and inhale zone game objects, as well as their update logic, is defined later in the transcript and will be added here.
*   **Respawn Logic (Placeholder):** The code for respawning the player if they fall off-screen is defined later and will be added.
*   `return player as PlayerGameObject`: Returns the created player game object, cast as the `PlayerGameObject` type for type safety.

### 6.2 Setting up Player Controls (entities.ts)

The `setControls` function in `entities.ts` handles player input and actions.

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';
import { PlayerGameObject } from './entities';

export function setControls(context: k.KaboomCtx, player: PlayerGameObject) {
    const inhaleEffectRef = k.k.get('inhaleEffect')[0];

    k.k.onKeyDown((key) => {
        switch (key) {
            case 'left':
                player.direction = 'left';
                player.flipX(true);
                player.move(-player.speed, 0);
                break;
            case 'right':
                player.direction = 'right';
                player.flipX(false);
                player.move(player.speed, 0);
                break;
            case 'z':
                if (player.isFull) {
                    player.play('kirbyinhale'); // Play inhale animation even when full (for visual consistency)
                    inhaleEffectRef.opacity = 0;
                    break;
                }
                player.isInhaling = true;
                player.play('kirbyinhale');
                inhaleEffectRef.opacity = 1;
                break;
            default:
                break;
        }
    });

    k.k.onKeyPress('space', () => {
        player.doubleJump();
    });

    k.k.onKeyRelease('z', () => {
        if (player.isFull) {
            player.play('kirbyinhale'); // Play inhale animation again when releasing 'z' after being full
            const shootingStar = k.k.add([
                k.k.sprite('star', { flipX: player.direction === 'right' }),
                k.k.area({ shape: new k.k.Rect(k.k.vec2(4, 4), 6, 6) }),
                k.k.pos(player.direction === 'left' ? player.pos.x - 80 : player.pos.x + 80, player.pos.y + 5),
                k.k.scale(SCALE),
                k.k.move(player.direction === 'left' ? k.k.LEFT : k.k.RIGHT, 400),
                'shootingStar',
            ]);

            shootingStar.onCollide('platform', () => {
                k.k.destroy(shootingStar);
            });

            player.isFull = false;
            k.k.wait(1, () => {
                player.play('kirbyidle');
            });
            return;
        }

        inhaleEffectRef.opacity = 0;
        player.isInhaling = false;
        player.play('kirbyidle');
    });
}
```

*   `inhaleEffectRef = k.k.get('inhaleEffect')[0]`: Gets a reference to the "inhaleEffect" game object using its tag. `k.k.get('inhaleEffect')` returns an array of game objects with the "inhaleEffect" tag, and `[0]` accesses the first element (assuming only one inhale effect object exists).
*   **`k.k.onKeyDown((key) => { ... })`:** Sets up a key down event handler. This function is called every frame while a key is pressed.
    *   **Left/Right Movement:** Handles 'left' and 'right' key presses to move the player horizontally using `player.move()`. `player.flipX()` flips the sprite horizontally to face the direction of movement.
    *   **Inhale (Z Key):** Handles 'z' key presses for inhaling action.
        *   If `player.isFull` is true (player has swallowed an enemy), it plays the "kirbyinhale" animation (for visual consistency) and hides the inhale effect.
        *   If `player.isFull` is false, it sets `player.isInhaling` to true, plays the "kirbyinhale" animation, and makes the inhale effect visible (`inhaleEffectRef.opacity = 1`).
*   **`k.k.onKeyPress('space', () => { ... })`:** Sets up a key press event handler for the space key. `k.k.onKeyPress` is triggered once when a key is pressed down.
    *   **Jump (Space Key):** Calls `player.doubleJump()` to initiate a jump.
*   **`k.k.onKeyRelease('z', () => { ... })`:** Sets up a key release event handler for the 'z' key. This function is called once when a key is released.
    *   **Shoot Star (Z Key Release when Full):** If `player.isFull` is true when the 'z' key is released, it:
        *   Plays the "kirbyinhale" animation again.
        *   Creates a "shootingStar" game object:
            *   `k.k.sprite('star', { flipX: player.direction === 'right' })`: Adds the "star" sprite, flipping it horizontally based on the player's direction.
            *   `k.k.area({...})`: Adds an area component for collision detection for the star.
            *   `k.k.pos(...)`: Sets the star's initial position relative to the player, adjusted based on the direction.
            *   `k.k.scale(SCALE)`: Scales the star sprite.
            *   `k.k.move(...)`: Adds a move component to propel the star left or right.
            *   `'shootingStar'`: Assigns the "shootingStar" tag.
        *   `shootingStar.onCollide('platform', () => { ... })`: Sets up a collision event handler for the shooting star. If it collides with a "platform," it destroys the shooting star.
        *   Sets `player.isFull` to false.
        *   Uses `k.k.wait(1, () => { ... })` to wait for 1 second before playing the "kirbyidle" animation again.
    *   **Stop Inhaling (Z Key Release when Not Full):** If `player.isFull` is false when the 'z' key is released, it:
        *   Hides the inhale effect (`inhaleEffectRef.opacity = 0`).
        *   Sets `player.isInhaling` to false.
        *   Plays the "kirbyidle" animation.

### 6.3 Defining Inhale Effect and Zone (entities.ts)

Add the inhale effect and inhale zone game object definitions within the `makePlayer` function, before the `onUpdate` logic:

```typescript
export function makePlayer(context: k.KaboomCtx, posX: number, posY: number): PlayerGameObject {
    // ... (previous player code) ...

    // Inhale Effect
    const inhaleEffect = k.k.add([
        k.k.sprite('kirbyinhale', { anim: 'kirbyinhale' }),
        k.k.pos(player.pos.x, player.pos.y), // Initial position (will be updated)
        k.k.scale(SCALE),
        k.k.opacity(0), // Initially hidden
        'inhaleEffect',
    ]);

    // Inhale Zone (Hitbox)
    const inhaleZone = k.k.add([
        k.k.area({ shape: new k.k.Rect(k.k.vec2(0, 0), 16, 16), isSensor: true }), // Sensor: doesn't cause physical collisions
        k.k.pos(player.pos.x, player.pos.y), // Initial position (will be updated)
        'inhaleZone',
    ]);

    k.k.onUpdate(() => {
        // Inhale Zone and Effect Update Logic
        if (player.direction === 'left') {
            inhaleZone.pos = k.k.vec2(player.pos.x - 14, player.pos.y + 8);
            inhaleEffect.pos = k.k.vec2(player.pos.x - 14, player.pos.y + 8);
            inhaleEffect.flipX(true);
        } else { // direction === 'right' or default
            inhaleZone.pos = k.k.vec2(player.pos.x + 14, player.pos.y + 8);
            inhaleEffect.pos = k.k.vec2(player.pos.x + 14, player.pos.y + 8);
            inhaleEffect.flipX(false);
        }
    });

    k.k.onUpdate(() => {
        // Respawn Logic
        if (player.pos.y > 2000) {
            k.k.go('level1');
        }
    });

    return player as PlayerGameObject;
}
```

*   **Inhale Effect Object:**
    *   `k.k.sprite('kirbyinhale', { anim: 'kirbyinhale' })`: Adds the "kirbyinhale" sprite and plays the "kirbyinhale" animation.
    *   `k.k.pos(player.pos.x, player.pos.y)`: Sets the initial position to the player's position.
    *   `k.k.scale(SCALE)`: Scales the inhale effect.
    *   `k.k.opacity(0)`: Sets the initial opacity to 0, making it invisible by default.
    *   `'inhaleEffect'`: Assigns the "inhaleEffect" tag.
*   **Inhale Zone Object:**
    *   `k.k.area({...})`: Adds an area component for collision detection.
        *   `shape: new k.k.Rect(...)`: Defines a rectangular shape for the inhale zone.
        *   `isSensor: true`: Makes the area a sensor, meaning it detects collisions but doesn't cause physical collisions (it's just for triggering events).
    *   `k.k.pos(player.pos.x, player.pos.y)`: Sets the initial position to the player's position.
    *   `'inhaleZone'`: Assigns the "inhaleZone" tag.
*   **Inhale Zone and Effect Update Logic (`k.k.onUpdate(() => { ... })`):**
    *   This `onUpdate` function runs every frame and updates the positions and `flipX` property of the `inhaleZone` and `inhaleEffect` objects based on the player's direction. It positions them slightly in front of the player, either to the left or right, depending on `player.direction`.
*   **Respawn Logic (`k.k.onUpdate(() => { ... })`):**
    *   This `onUpdate` function checks if the player's vertical position (`player.pos.y`) exceeds 2000. If it does, it means the player has fallen off-screen, and it restarts the current level using `k.k.go('level1')`.

## 7. Enemy Implementation (entities.ts & main.ts)

Let's add enemies to make the game more challenging. We'll create flame, guy, and bird enemies.

### 7.1 `makeFlameEnemy` Function (entities.ts)

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';

export type FlameEnemyGameObject = k.GameObject<k.SpriteComp | k.AreaComp | k.BodyComp | k.PosComp | k.ScaleComp | k.StateComp> & {
    isSwallowable: boolean;
};


export function makeFlameEnemy(context: k.KaboomCtx, posX: number, posY: number): FlameEnemyGameObject {
    const flame = k.k.add([
        k.k.sprite('flame', { anim: 'flame' }),
        k.k.scale(SCALE),
        k.k.pos(posX * SCALE, posY * SCALE),
        k.k.area({ shape: new k.k.Rect(k.k.vec2(0, 0), 16, 16), collisionIgnore: ['enemy'] }),
        k.k.body(),
        k.k.state('idle', ['idle', 'jump']),
        'enemy',
        'flameEnemy',
        { isSwallowable: true },
    ]);

    flame.onStateEnter('idle', async () => {
        await k.k.wait(1);
        flame.enterState('jump');
    });

    flame.onStateEnter('jump', () => {
        flame.jump(1000);
    });

    flame.onStateUpdate('jump', () => {
        if (flame.isGrounded()) {
            flame.enterState('idle');
        }
    });

    return flame as FlameEnemyGameObject;
}
```

*   **`FlameEnemyGameObject` Type:** Defines a TypeScript type for flame enemy objects, specifying components and the `isSwallowable` property.
*   `k.k.make(...)`: Creates the flame enemy game object with the following:
    *   `k.k.sprite('flame', { anim: 'flame' })`: Adds the "flame" sprite and plays the "flame" animation.
    *   `k.k.scale(SCALE)`: Scales the flame sprite.
    *   `k.k.pos(posX * SCALE, posY * SCALE)`: Sets the initial position.
    *   `k.k.area({...})`: Adds an area component, ignoring collisions with other "enemy" tagged objects.
    *   `k.k.body()`: Adds a body component for physics.
    *   `k.k.state('idle', ['idle', 'jump'])`: Adds a state component, defining the state machine with "idle" as the initial state and "idle" and "jump" as possible states.

        > **State Machine:** A behavioral design pattern used to model the states of an object and the transitions between those states based on events or conditions. In game development, state machines are often used to control the AI and behavior of characters and enemies.

    *   `'enemy'`, `'flameEnemy'`: Assigns "enemy" and "flameEnemy" tags.
    *   `{ isSwallowable: true }`: Sets the `isSwallowable` property to true, indicating this enemy can be swallowed by the player.
*   **State Machine Logic:**
    *   `flame.onStateEnter('idle', async () => { ... })`: Defines the behavior when the flame enemy enters the "idle" state. It waits for 1 second using `k.k.wait(1)` and then transitions to the "jump" state using `flame.enterState('jump')`.
    *   `flame.onStateEnter('jump', () => { ... })`: Defines the behavior when entering the "jump" state. It makes the flame enemy jump using `flame.jump(1000)`.
    *   `flame.onStateUpdate('jump', () => { ... })`: Defines the behavior that runs every frame while in the "jump" state. It checks if the flame is grounded using `flame.isGrounded()`. If grounded, it transitions back to the "idle" state.

### 7.2 `makeGuyEnemy` Function (entities.ts)

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';

export type GuyEnemyGameObject = k.GameObject<k.SpriteComp | k.AreaComp | k.BodyComp | k.PosComp | k.ScaleComp | k.StateComp> & {
    isSwallowable: boolean;
};

export function makeGuyEnemy(context: k.KaboomCtx, posX: number, posY: number): GuyEnemyGameObject {
    const guy = k.k.add([
        k.k.sprite('guy', { anim: 'guy' }),
        k.k.scale(SCALE),
        k.k.pos(posX * SCALE, posY * SCALE),
        k.k.area({ shape: new k.k.Rect(k.k.vec2(0, 0), 16, 16), collisionIgnore: ['enemy'] }),
        k.k.body(),
        k.k.state('idle', ['idle', 'left', 'right']),
        'enemy',
        'guyEnemy',
        { isSwallowable: true },
    ]);

    guy.onStateEnter('idle', async () => {
        await k.k.wait(1);
        guy.enterState('left');
    });

    guy.onStateEnter('left', async () => {
        guy.flipX(false); // Face left
        await k.k.wait(2);
        guy.enterState('right');
    });

    guy.onStateUpdate('left', () => {
        guy.move(-50, 0); // Move left
    });

    guy.onStateEnter('right', async () => {
        guy.flipX(true); // Face right
        await k.k.wait(2);
        guy.enterState('left');
    });

    guy.onStateUpdate('right', () => {
        guy.move(50, 0); // Move right
    });

    return guy as GuyEnemyGameObject;
}
```

*   **`GuyEnemyGameObject` Type:** Defines a TypeScript type for guy enemy objects.
*   `k.k.make(...)`: Creates the guy enemy game object. Similar to `makeFlameEnemy`, but with "guy" sprite, "guyEnemy" tag, and a different state machine.
*   **State Machine Logic:**
    *   States: "idle," "left," "right."
    *   "idle" state: Waits for 1 second, then transitions to "left."
    *   "left" state: Flips the sprite to face left, waits for 2 seconds, then transitions to "right." While in "left," it moves left using `guy.move(-50, 0)`.
    *   "right" state: Flips the sprite to face right, waits for 2 seconds, then transitions to "left." While in "right," it moves right using `guy.move(50, 0)`.

### 7.3 `makeBirdEnemy` Function (entities.ts)

```typescript
import * as k from './kaboom-cx';
import { SCALE } from './constants';

export type BirdEnemyGameObject = k.GameObject<k.SpriteComp | k.AreaComp | k.PosComp | k.ScaleComp | k.MoveComp | k.OffScreenComp> & {
    isSwallowable: boolean;
};

export function makeBirdEnemy(context: k.KaboomCtx, posX: number, posY: number, speed: number): BirdEnemyGameObject {
    const bird = k.k.add([
        k.k.sprite('bird', { anim: 'bird' }),
        k.k.scale(SCALE),
        k.k.pos(posX * SCALE, posY * SCALE),
        k.k.area({ shape: new k.k.Rect(k.k.vec2(0, 0), 16, 16), collisionIgnore: ['enemy'] }),
        k.k.move(k.k.LEFT, speed),
        k.k.offscreen({ destroy: true, distance: 400 }),
        'enemy',
        'birdEnemy',
        { isSwallowable: true },
    ]);

    return bird as BirdEnemyGameObject;
}
```

*   **`BirdEnemyGameObject` Type:** Defines a TypeScript type for bird enemy objects.
*   `k.k.make(...)`: Creates the bird enemy game object.
    *   `k.k.sprite('bird', { anim: 'bird' })`: Adds the "bird" sprite and animation.
    *   `k.k.scale(SCALE)`: Scales the bird sprite.
    *   `k.k.pos(posX * SCALE, posY * SCALE)`: Sets the initial position.
    *   `k.k.area({...})`: Adds an area component, ignoring collisions with other "enemy" objects.
    *   `k.k.move(k.k.LEFT, speed)`: Adds a move component to make the bird move left at the specified `speed`.
    *   `k.k.offscreen({ destroy: true, distance: 400 })`: Adds an offscreen component. When the bird is 400 pixels or more off-screen, it will be destroyed.

        > **Offscreen Component:** A Kaboom.js component that automatically destroys a game object when it moves off-screen by a specified distance. This is useful for managing performance by removing objects that are no longer visible.

    *   `'enemy'`, `'birdEnemy'`: Assigns "enemy" and "birdEnemy" tags.
    *   `{ isSwallowable: true }`: Sets `isSwallowable` to true.

### 7.4 Adding Enemies to the Scene (main.ts)

In `main.ts`, within the `level1` scene, add logic to spawn the flame, guy, and bird enemies based on the spawn points defined in Tiled.

```typescript
import * as k from './kaboom-cx';
import { makeMap } from './utils';
import { makePlayer, setControls, makeFlameEnemy, makeGuyEnemy, makeBirdEnemy, makeInhalable } from './entities';

k.k.scene('level1', async () => {
    // ... (background and level loading code) ...

    // Create Player (already present)
    const player = makePlayer(k.k, level1SpawnPoints.player[0].x, level1SpawnPoints.player[0].y);
    k.k.add(player);
    setControls(k.k, player);

    // Create Flame Enemies
    level1SpawnPoints.flame.forEach(spawn => {
        const flame = makeFlameEnemy(k.k, spawn.x, spawn.y);
        k.k.add(flame);
        makeInhalable(k.k, flame);
    });

    // Create Guy Enemies
    level1SpawnPoints.guy.forEach(spawn => {
        const guy = makeGuyEnemy(k.k, spawn.x, spawn.y);
        k.k.add(guy);
        makeInhalable(k.k, guy);
    });

    // Create Bird Enemies (Looping Spawner)
    const birdSpeeds = [100, 200, 300];
    level1SpawnPoints.bird.forEach(spawn => {
        k.k.loop(10, () => {
            const bird = makeBirdEnemy(k.k, spawn.x, spawn.y, birdSpeeds[Math.floor(Math.random() * birdSpeeds.length)]);
            k.k.add(bird);
            makeInhalable(k.k, bird);
        });
    });

    // ... (camera follow logic) ...
});

k.k.start('level1');
```

*   **Flame and Guy Enemy Spawning:** Uses `level1SpawnPoints.flame.forEach(...)` and `level1SpawnPoints.guy.forEach(...)` to iterate over the spawn points for flame and guy enemies. For each spawn point:
    *   Calls `makeFlameEnemy` or `makeGuyEnemy` to create an enemy instance at the spawn point's coordinates.
    *   Adds the created enemy to the scene using `k.k.add(enemy)`.
    *   Calls `makeInhalable(k.k, enemy)` to apply the inhalable behavior to the enemy.

### 7.5 `makeInhalable` Function (entities.ts)

The `makeInhalable` function in `entities.ts` adds the logic to make enemies inhalable by the player.

```typescript
import * as k from './kaboom-cx';
import { PlayerGameObject } from './entities';

export function makeInhalable(context: k.KaboomCtx, enemy: k.GameObject) {
    enemy.onCollide('inhaleZone', () => {
        enemy.isSwallowable = true;
    });

    enemy.onCollideEnd('inhaleZone', () => {
        enemy.isSwallowable = false;
    });

    enemy.onCollide('shootingStar', (shootingStar) => {
        k.k.destroy(enemy);
        k.k.destroy(shootingStar);
    });

    k.k.onUpdate(() => {
        const playerRef = k.k.get('player')[0] as PlayerGameObject;
        if (playerRef.isInhaling && enemy.isSwallowable) {
            if (playerRef.direction === 'right') {
                enemy.move(-800, 0);
            } else {
                enemy.move(800, 0);
            }
        }
    });
}
```

*   **`enemy.onCollide('inhaleZone', () => { ... })`:** Sets up a collision event handler for when the enemy collides with the "inhaleZone." When a collision occurs, it sets `enemy.isSwallowable = true;`.
*   **`enemy.onCollideEnd('inhaleZone', () => { ... })`:** Sets up a collision end event handler. When the collision with the "inhaleZone" ends, it sets `enemy.isSwallowable = false;`.
*   **`enemy.onCollide('shootingStar', (shootingStar) => { ... })`:** Sets up a collision event handler for when the enemy collides with a "shootingStar." When a collision occurs, it destroys both the enemy and the shooting star using `k.k.destroy(enemy)` and `k.k.destroy(shootingStar)`.
*   **`k.k.onUpdate(() => { ... })`:** Sets up an update event handler that runs every frame.
    *   `const playerRef = k.k.get('player')[0] as PlayerGameObject;`: Gets a reference to the player game object.
    *   **Inhale Movement Logic:** Checks if the player is inhaling (`playerRef.isInhaling`) and if the enemy is swallowable (`enemy.isSwallowable`). If both are true, it moves the enemy towards the player (either left or right) using `enemy.move()`, simulating the enemy being pulled into the player's mouth.

## 8. Building and Publishing the Game

To share your game, you need to build it for web deployment.

### 8.1 Vite Configuration (`vite.config.ts`)

Create a `vite.config.ts` file at the root of your project with the following configuration:

```typescript
import { defineConfig } from 'vite'

export default defineConfig({
  base: './',
  build: {
    minify: false, // Disable minification due to Kaboom.js issue
  },
})
```

*   `base: './'`:  Sets the base URL for the built application to be relative to the root directory. This is important for correct asset paths when deploying to platforms like itch.io.
*   `build: { minify: false }`: Disables JavaScript minification during the build process. This is a workaround for a known issue with Kaboom.js and minification. You may try building with `minify: true` in the future to see if the issue is resolved.

    > **Minification:** The process of removing unnecessary characters (like whitespace and comments) from code to reduce its file size, making it faster to download and execute in web browsers.

### 8.2 Building the Game

Run the following command in your terminal:

```bash
npm run build
```

This command uses Vite to build your TypeScript project.  After successful execution, a `dist` folder will be created at the root of your project. This folder contains the built game files.

### 8.3 Testing the Build (Optional)

To test the built game locally, you can use a local server like `live-server`.  Navigate into the `dist` folder in your terminal and run:

```bash
npx live-server .
```

This will start a local server, and you can access your game in a web browser.

### 8.4 Publishing to itch.io

1.  **Zip the `dist` folder:** Compress the entire `dist` folder into a ZIP file.
2.  **Create an itch.io account (or log in):** Go to itch.io and create an account or log in to your existing account.
3.  **Upload your game:**
    *   Go to your dashboard.
    *   Create a new project or edit an existing one.
    *   Upload the ZIP file containing the `dist` folder as your game's upload.
    *   Configure other game settings on itch.io as needed.

Your game is now published and playable on itch.io!

> **itch.io:** A popular online platform for indie game distribution and sales. It provides tools for game developers to host, sell, and promote their games.

## Conclusion

This chapter has provided a comprehensive guide to building a Kirby-like platformer game using TypeScript and Kaboom.js. You have learned how to set up a project with Vite, load assets, design levels with Tiled, implement player controls and mechanics, create enemies with basic AI, and build and publish your game. This foundation allows you to expand upon this project, adding more levels, enemies, features, and complexity to create a fully realized game. Remember to explore the Kaboom.js documentation and experiment with its various features to further enhance your game development skills.
