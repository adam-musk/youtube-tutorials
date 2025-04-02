---
layout: "../../layouts/BlogPost.astro"
title: "React Fundamentals: A Crash Course for Beginners"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "jLS0TkAHvRg"
channel: ""
index: 18
---

# React Fundamentals: A Crash Course for Beginners

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/jLS0TkAHvRg" frameborder="0" allowfullscreen></iframe>

## Introduction to React

Welcome to the React Fundamentals Crash Course, designed for individuals with no prior experience in React. This course aims to equip complete beginners with a solid understanding of React's core concepts, enabling you to embark on your journey as a front-end web developer. React is a highly sought-after JavaScript library in the web development industry, making this a valuable skill to acquire.

This course is a continuation of HTML, CSS, and JavaScript crash courses. Therefore, familiarity with these foundational web technologies is essential before proceeding.  A basic understanding of modern JavaScript (ES2015+) features will also be beneficial but not strictly required.

This crash course will focus on fundamental concepts relevant to beginners. React is a vast library with advanced topics that can be overwhelming initially.  We will concentrate on the essential knowledge needed to get started and build a foundation for further exploration.

We will be using **React version 18**, the latest stable release as of March 29th, 2022. While version 18 introduces new features, we will only cover those pertinent to beginners, ensuring the focus remains on core fundamentals without unnecessary complexity.

This is a comprehensive crash course, and its length reflects the depth of content covered. It is recommended to learn at your own pace, pausing and practicing as needed.  **Coding along with the examples is strongly encouraged** as it is the most effective way to learn and solidify your understanding.

By the end of this course, you will have a robust grasp of React fundamentals, setting you up for further learning and practical application.

## What is React?

React is defined as:

> React is an **open-source JavaScript library** for building user interfaces.
> It is specifically designed for creating interactive and dynamic web UIs.

Let's break down this definition into key components:

*   **JavaScript Library, Not a Framework:** React is specifically a library, focusing on a singular purpose: building user interfaces (UIs). It excels at this task, offering tools and patterns for efficient UI development. Unlike frameworks, which provide a more comprehensive structure for entire applications, React concentrates on the view layer.

    > **Library vs. Framework:** A **library** is a collection of pre-written code that provides specific functionalities, allowing developers to pick and choose what they need. A **framework** is a more comprehensive structure that dictates the architecture of an application and provides a complete set of tools and guidelines.

*   **Building User Interfaces:** React's primary focus is on creating rich and interactive user interfaces for web applications. It manages the view layer of your application, handling how users interact with and perceive your web application.

While React excels at UI development, it does not inherently handle other aspects of web application development such as routing or HTTP requests. However, React boasts a vibrant **ecosystem**:

> **Ecosystem:** In the context of software, an **ecosystem** refers to a collection of related tools, libraries, frameworks, and community resources that work together harmoniously and extend the functionality of a core technology.

This ecosystem ensures React integrates seamlessly with other libraries to build comprehensive, enterprise-scale web applications.

## Why Learn React?

There are compelling reasons to learn React, both practical and technical:

*   **Job Market Demand:** React is one of the most popular UI libraries in the web development industry. Proficiency in React significantly enhances your employability and opens doors to numerous front-end developer roles.

*   **Strong Community Support:** React benefits from a large and active community. This vast community provides abundant resources, including articles, tutorials, and solutions on platforms like Stack Overflow, ensuring you can find help and guidance when facing challenges.

*   **Component-Based Architecture:** React employs a **component-based architecture**:

    > **Component-Based Architecture:** A software design approach that structures an application as a collection of independent, reusable, and encapsulated modules called **components**. Each component is responsible for a specific part of the UI and functionality.

    This architecture offers several advantages:
    *   **Modularity:** Applications are broken down into smaller, manageable, and encapsulated parts (components), simplifying development and maintenance.
    *   **Composability:** Components can be combined and nested to create complex user interfaces from simpler building blocks.
    *   **Reusability:** Components are designed to be reusable across different parts of an application or even in different projects, promoting code efficiency and consistency.

*   **Declarative Nature:** React is **declarative**:

    > **Declarative Programming:** A programming paradigm where you express *what* you want to achieve without explicitly describing *how* to achieve it. You describe the desired outcome, and the system figures out the steps to get there.

    In React, you describe the desired UI state in your code, and React, along with **React DOM**:

    > **React DOM:** A package that serves as the entry point to the DOM and server renderers for React. It is responsible for rendering React components in the web browser's Document Object Model (DOM).

    abstracts away the complexities of directly manipulating the browser's Document Object Model (DOM). React handles the intricate updates and rendering processes, making UI creation more intuitive and less error-prone.

In essence, learning React is a valuable investment, enhancing your skillset and opening opportunities in the dynamic field of web development.

## Setting Up Your Development Environment

To begin developing React applications, you need to set up your development environment. This involves installing three essential tools:

1.  **Web Browser:** A modern web browser is necessary to view and interact with your React applications. Google Chrome is recommended, but any modern browser such as Firefox, Safari, or Edge will suffice.

2.  **Node.js:** Node.js is a JavaScript runtime environment that is crucial for React development.

    *   **Installation:**
        *   Navigate to [nodejs.org](https://nodejs.org/).
        *   Download and install the **LTS (Long-Term Support)** version, which is the recommended stable release.
        *   Follow the installation prompts, typically accepting the default settings.

3.  **Code Editor:** A code editor provides a user-friendly environment for writing and managing code. **Visual Studio Code (VS Code)** is a highly recommended and popular choice for React development.

    *   **Installation:**
        *   Navigate to [code.visualstudio.com](https://code.visualstudio.com/).
        *   Download and install VS Code for your operating system.
        *   After installation, open VS Code and install the **Prettier** extension from the Extensions panel. Prettier automatically formats your code, improving readability and consistency.

Once these tools are installed, create a new folder on your computer to house your React projects (e.g., "react-crash-course"). Open this folder in VS Code.

## Creating Your First React Application

React applications are often created using **Create React App**:

> **Create React App (CRA):** A command-line interface tool provided by Facebook (now Meta) that simplifies the process of setting up a new React project. It automatically configures the build process, development server, and other essential tools, allowing developers to start building React applications quickly without complex configurations.

Create React App streamlines the setup process, allowing you to focus on writing React code rather than configuration.

Follow these steps to create your first React application:

1.  **Open Integrated Terminal:** In VS Code, open the integrated terminal by selecting **View > Terminal**.

2.  **Run Create React App Command:** In the terminal, execute the following command:

    ```bash
    npx create-react-app react-demo
    ```

    > **npx:** **npx** is a package runner tool that comes with **npm** (Node Package Manager). It allows you to execute Node.js packages without installing them globally. In this case, it runs `create-react-app` directly from the npm registry.

    This command will create a new folder named "react-demo" containing a pre-configured React application. This process may take a few moments as it sets up the project structure and installs necessary dependencies.

3.  **Navigate to Project Folder:** Once the command completes, navigate into the newly created project folder:

    ```bash
    cd react-demo
    ```

4.  **Start the Development Server:** Start the React development server with the command:

    ```bash
    npm start
    ```

    > **npm (Node Package Manager):** **npm** is the default package manager for Node.js. It is used to install, manage, and share JavaScript packages. The `npm start` command typically runs a script defined in the `package.json` file to start the development server for a React application.

    This command will compile your React application and automatically open it in your default web browser, usually at **`localhost:3000`**:

    > **localhost:** **localhost** is a hostname that refers to the computer you are currently using. In web development, **localhost:3000** typically indicates that a web server is running on your local machine, and port **3000** is the specific port number being used to access the application.

    You should see the default React application running, displaying the message "Edit `src/App.js` and save to reload."

5.  **Modify `App.js`:** In VS Code, expand the "src" folder in your project and open the `App.js` file.  Locate the text within the `return` statement and change it to "Hello World". Save the file (Ctrl+S or Cmd+S).

6.  **Observe Changes in Browser:**  As soon as you save `App.js`, the browser will automatically refresh, and you should now see "Hello World" displayed in the browser window.

Congratulations! You have successfully created and run your first React application.

## Understanding the Application Folder Structure

Let's explore the structure of a React application created with Create React App. At the root level, you'll find several folders and files:

### Key Files

*   **`package.json`:** This file is the heart of your Node.js project and, therefore, your React application. It contains:
    *   **Dependencies:** Lists the libraries your project relies on, including `react` and `react-dom` (version 18 in this case). These are essential for building React applications.
    *   **Scripts:** Defines commands you can run using `npm`, such as `start` (to run the development server), `build` (to create a production build), and `test` (to run tests).
    *   **`eslintConfig`:** Configuration for **ESLint**:

        > **ESLint:** A popular **linting** tool for JavaScript and JSX. **Linting** is the process of statically analyzing code to identify potential errors, stylistic inconsistencies, and code quality issues. ESLint helps maintain code consistency and catch potential bugs early in development.

    *   **`browserslist`:** Specifies the browsers your application should support, ensuring compatibility across different browser environments.

*   **`package-lock.json` or `yarn.lock`:** These files (one will be present depending on whether you use npm or Yarn package manager) ensure consistent dependency installation across different environments. They lock down the specific versions of dependencies used, preventing unexpected issues due to dependency updates. You generally don't need to directly interact with these files.

*   **`.gitignore`:**  This file specifies intentionally untracked files that Git should ignore. This commonly includes dependency folders (`node_modules`), build output, and other non-essential files.

*   **`README.md`:** A standard **readme** file:

    > **Readme File:** A text file, typically named `README.md` (using Markdown formatting), that provides essential information about a project. It usually includes a project description, instructions for setup and usage, and other relevant details for users and developers.

    It usually contains basic information about your React application.

### Key Folders

*   **`node_modules`:** This folder houses all the **dependencies**:

    > **Dependencies:** In software development, **dependencies** are external libraries, packages, or modules that a project relies on to function correctly. These are typically installed and managed using package managers like npm or Yarn.

    listed in `package.json`. It's created when you run `npx create-react-app` or `npm install`. This folder can be quite large and is usually ignored by version control (as specified in `.gitignore`).

*   **`public`:** The **public folder**:

    > **Public Folder:** In web applications, the **public folder** is a directory that contains static assets that are directly served to the web browser without any processing. This typically includes HTML files, images, and other assets that don't require server-side rendering or compilation.

    contains static assets for your application.
    *   **`index.html`:** This is the **single HTML file** for your entire single-page application (SPA).

        > **Single Page Application (SPA):** A web application that loads a single HTML page and dynamically updates the content within that page as the user interacts with the application. SPAs provide a more fluid and responsive user experience compared to traditional multi-page applications.

        In React SPAs, you will typically only have one `index.html` file.  The UI dynamically changes within this page, but it's this single file that is served to the browser. You generally won't modify this file extensively, mainly making adjustments in the `<head>` section if needed.  Crucially, within the `<body>` tag, you'll find a `<div>` element with the `id="root"`.

        ```html
        <div id="root"></div>
        ```
        This `<div>` is the **root DOM node**:

        > **Root DOM Node:** The **root DOM node** is a specific HTML element in the `index.html` file that serves as the container where React will render and manage the entire user interface of your application. In Create React App, this is typically a `<div>` element with the `id="root"`.

        React will take control of this `<div>` at runtime and render your application's UI inside it.

    *   **`manifest.json`, `favicon.ico`, `logo*.png`:** These files are related to **Progressive Web Apps (PWAs)**:

        > **Progressive Web App (PWA):** A type of web application that is designed to provide a user experience similar to native mobile applications, but delivered through web technologies. PWAs offer features like offline capabilities, push notifications, and installability on users' devices.

        PWAs are beyond the scope of this beginner course.
    *   **`robots.txt`:** This file is used for **search engine optimization (SEO)**:

        > **Search Engine Optimization (SEO):** The practice of optimizing a website or web page to improve its visibility in search engine results pages (SERPs). This involves various techniques to make it easier for search engines to find, crawl, and index a website's content.

        and is not specific to React.

*   **`src`:** The **source folder**:

    > **Source Folder:** In software projects, the **source folder** (often named `src` or `source`) is the directory where the source code files of the application are stored. This includes JavaScript files, CSS files, and other assets that are essential for building the application's logic and user interface.

    is where you will spend most of your development time. It contains the source code of your React application.
    *   **`index.js`:** This is the **entry point** of your React application.

        > **Entry Point:** The **entry point** of an application is the starting point where the execution of the program begins. In a React application created with Create React App, `index.js` is the file that initializes the React application and renders the root component into the DOM.

        It's the first JavaScript file that gets executed.  Within `index.js`, you'll find:
        *   The **root component**, which is the `App` component (from `App.js`).
        *   The **DOM element** that React will control, identified by `id="root"` in `index.html`. React renders the `App` component into this **root DOM node**.

    *   **`App.js`:** This file contains the **`App` component**:

        > **App Component:** In React applications created with Create React App, the **App component** is the root component of the application. It serves as the starting point for building the user interface and typically contains or orchestrates other components to create the overall application structure.

        which is the main component of your application. It's responsible for the initial HTML displayed in the browser.  `App.js` typically includes:
        *   **JSX**: The code that defines the structure and content of the UI.
        *   **CSS Import**:  An import statement to include styling from `App.css`.
        *   **Test File Import**: Potentially, an import for `App.test.js` for unit testing.
        *   **Logo Import**: An import for `logo.svg` if used in the component.

    *   **`App.css`:**  Contains CSS styles specifically for the `App` component.

    *   **`App.test.js`:**  A file for writing **unit tests**:

        > **Unit Test:** A type of software testing where individual units or components of a software application are tested in isolation. In React, unit tests typically focus on testing individual components to ensure they function correctly and produce the expected output.

        for the `App` component.

    *   **`index.css`:**  Contains global CSS styles that are applied to the `<body>` tag and are referenced in `index.js`.

    *   **`logo.svg`:**  The React logo in SVG format, often referenced in the `App` component.

    *   **`reportWebVitals.js` & `setupTests.js`:** These files are related to performance analytics and testing setup, respectively. As a beginner, you can generally ignore these initially.

### Application Startup Flow

When you run `npm start`, the following sequence of events occurs:

1.  **`index.html` is served:** The `index.html` file from the `public` folder is served to the browser. This file contains the **root DOM node** (`<div id="root"></div>`).

2.  **`index.js` takes control:** The browser executes `index.js`. This script uses the **React DOM library** to:
    *   Identify the **root DOM node** in `index.html`.
    *   Render the **`App` component** into this **root DOM node**.

3.  **`App` component renders UI:** The `App` component, defined in `App.js`, contains the JSX that describes the UI. React renders this JSX into the **root DOM node**, making it visible in the browser.

### React 18 Update in `index.js`

The transcript mentions a necessary update in `index.js` for React 18 compatibility.  Create React App might install version 18, but the default `index.js` might still use an older API. To ensure you're using React 18 features, make the following changes in `src/index.js`:

```javascript
import React from 'react';
// Comment out the following line:
// import ReactDOM from 'react-dom';
// Replace it with:
import { createRoot } from 'react-dom/client';
import App from './App';
import './index.css';

// Comment out:
// ReactDOM.render(
//   <React.StrictMode>
//     <App />
//   </React.StrictMode>,
//   document.getElementById('root')
// );

// Replace with:
const container = document.getElementById('root');
const root = createRoot(container); // Create a root.
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

This modification updates the root API to use `createRoot` from `react-dom/client`, enabling React 18 features in your application.  If you are following this tutorial some time after the video's publication, Create React App might have already been updated, and this step might not be necessary.

## Components: The Building Blocks of React UI

React applications are built using **components**.

> **Component (in React):** A **component** is a reusable and independent building block of a React user interface. It is a self-contained unit that encapsulates its own logic, styling, and rendering. Components can be composed together to create complex UIs.

Think of components as modular, reusable pieces of your UI.  A website can be decomposed into sections like:

*   Header
*   Navigation Bar (Site Nav)
*   Main Content
*   Footer

Each of these sections can be represented as a React component.  Components can be nested within each other to build complex UIs.  The top-level component that encompasses the entire application is often called the **root component**, typically named `App` in Create React App projects.

Components promote code reusability. For example, a navigation component can be reused for both the left and right side navigation, potentially with different content but the same UI structure.

### Types of Components: Function vs. Class

In React, there are two main types of components:

1.  **Function Components:**  These are simpler and more modern. They are essentially JavaScript functions that return JSX (which we'll discuss shortly) to describe the UI.  Function components are the primary type used in modern React development and are the focus of this crash course.

2.  **Class Components:** These are older, more complex components defined using JavaScript classes. While still functional, they are generally less favored for new development in 2022 and beyond.  This crash course will primarily focus on function components.

### Examining the `App` Component

Let's look at the default `App` component in `App.js`.

```javascript
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

Key observations:

*   **`.js` Extension:** `App.js` is a JavaScript file, signifying it contains JavaScript code.
*   **JavaScript Function `App`:**  The code defines a JavaScript function named `App`. This is a function component.
*   **JSX Return Value:** The `App` function returns JSX (HTML-like syntax). This JSX describes the structure of the UI. In this case, it returns:
    *   A wrapping `<div>` tag.
    *   A `<header>` tag.
    *   An `<img>` tag for the React logo.
    *   A `<p>` (paragraph) tag with instructions.
    *   An `<a>` (link) tag.
*   **`export default App;`:** The component is exported as the **default export**:

    > **Default Export:** In JavaScript modules, a **default export** is the primary export from a module. Each module can have at most one default export. When importing a default export, you can choose any name for the import.

    This allows `index.js` to import and use the `App` component.

Real-world applications can have numerous components, ranging from tens to thousands, especially in large applications like Facebook, which reportedly uses over 30,000 components.

### Creating a Function Component: `Greet` Component

Let's create a simple function component to illustrate the concept. We'll create a component named `Greet` that displays the message "Hello Vishwas".

1.  **Create `Greet.js`:** Inside the `src` folder, create a new folder named "components". Within the "components" folder, create a new file named `Greet.js`.

2.  **Define `Greet` Component:** In `Greet.js`, add the following code:

    ```javascript
    import React from 'react';

    // Function Component using function declaration
    function Greet() {
      return <h1>Hello Vishwas</h1>;
    }

    export default Greet;
    ```
    Alternatively, you can use an **arrow function**:

    > **Arrow Function:** A concise syntax for writing functions in JavaScript, introduced in ES6 (ECMAScript 2015). Arrow functions are often more compact and have lexical `this` binding, which can simplify certain JavaScript patterns.

    ```javascript
    import React from 'react';

    // Function Component using arrow function
    const Greet = () => {
      return <h1>Hello Vishwas</h1>;
    }

    export default Greet;
    ```

3.  **Import and Use `Greet` in `App.js`:**
    *   In `App.js`, remove the existing JSX within the main `<div>` (keep the outer `<div>` with `className="App"`).
    *   At the top of `App.js`, import the `Greet` component:

        ```javascript
        import Greet from './components/Greet';
        ```

    *   Within the `App` component's JSX, add the `<Greet>` component tag:

        ```javascript
        function App() {
          return (
            <div className="App">
              <Greet />
            </div>
          );
        }
        ```

4.  **View in Browser:** Save both `Greet.js` and `App.js`. In the browser, you should now see "Hello Vishwas" displayed. Your first custom function component is rendered!

### Exporting and Importing Components: Default vs. Named Exports

*   **Default Export (used in `Greet.js`):** `export default Greet;`
    *   Allows you to import the component with any name in the importing file. For example, in `App.js`, we imported it as `import Greet from './components/Greet';`. We could have named it `MyComponent` and used `<MyComponent />` instead, and it would still work because it's the default export.

*   **Named Export:**  Let's modify `Greet.js` to use a **named export**:

    ```javascript
    import React from 'react';

    export const Greet = () => { // Notice 'export' keyword
      return <h1>Hello Vishwas</h1>;
    }
    ```
    *   To import a **named export**, you must use the exact same name within curly braces in the import statement in `App.js`:

        ```javascript
        import { Greet } from './components/Greet'; // Curly braces and 'Greet' name
        ```
    *   If you try to import it with a different name without curly braces (like with default exports), it will result in an error.

This course will primarily use **named exports** for component examples, but understanding both default and named exports is crucial for working with React codebases.

## JSX: JavaScript XML

**JSX**:

> **JSX (JavaScript XML):** A syntax extension to JavaScript that allows you to write HTML-like code within JavaScript files. JSX is primarily used in React to describe the structure of user interfaces in a declarative manner. It gets transformed into regular JavaScript function calls by tools like Babel during the build process.

JSX is a core concept in React.  It may look like HTML, but it's a syntax extension to JavaScript. JSX allows you to embed HTML-like structures directly within your JavaScript code, making it easier to define the UI of your React components.

### JSX Features and Differences from HTML

*   **JavaScript Expressions:** JSX allows you to embed JavaScript expressions within your HTML-like code using curly braces `{}`. For example:

    ```jsx
    <div>{2 + 2}</div> {/* Renders '4' */}
    ```

    You can evaluate expressions, call functions, and perform conditional logic within JSX using curly braces.

*   **Attribute Naming Conventions:** JSX has some differences in attribute naming compared to standard HTML:
    *   **`class` becomes `className`:**  In HTML, you use `class` to define CSS classes. In JSX, you must use `className` because `class` is a reserved keyword in JavaScript.

        ```jsx
        // HTML
        <div class="my-class"></div>

        // JSX
        <div className="my-class"></div>
        ```

    *   **`for` becomes `htmlFor`:** Similarly, `for` attribute (used with `<label>`) becomes `htmlFor` in JSX due to `for` being a JavaScript keyword.

        ```jsx
        // HTML
        <label for="name">Name:</label>
        <input type="text" id="name" />

        // JSX
        <label htmlFor="name">Name:</label>
        <input type="text" id="name" />
        ```

    *   **CamelCase Property Naming:** JSX uses camelCase for HTML attribute names that are composed of multiple words. For example:
        *   `onclick` becomes `onClick`
        *   `tabindex` becomes `tabIndex`

    You will encounter these differences as you work with JSX.

### React Elements: JSX Under the Hood

While JSX looks like HTML, React doesn't directly work with HTML strings in the browser.  Under the hood, JSX is transformed into **React elements**:

> **React Element:** A **React element** is the smallest unit of a React application's UI. It is a plain JavaScript object that describes a DOM node or another component. React elements are lightweight descriptions of what should be rendered on the screen.

When your React component returns JSX, it's actually creating React elements. These elements are then processed by React DOM to efficiently update the actual DOM and render the UI in the browser.

For beginners, it's sufficient to understand that JSX is a convenient syntax for writing UI structures, and React handles the underlying conversion to React elements and DOM updates.

## Props: Passing Data to Components

**Props**, short for "properties":

> **Props (Properties):** In React, **props** are inputs passed down from parent components to child components. They are read-only objects that allow parent components to configure and control the behavior and appearance of their children. Props are a primary mechanism for data flow in React.

are a fundamental mechanism for passing data from parent components to child components. They make components dynamic and reusable.

### Passing Props

To pass props to a component, you specify them as attributes when you use the component tag in JSX.

Let's modify our `Greet` component to accept a `name` prop and display a personalized greeting.

1.  **Modify `Greet.js` to Accept Props:**

    ```javascript
    import React from 'react';

    const Greet = (props) => { // Add 'props' parameter
      return (
        <div>
          <h1>Hello {props.name}</h1> {/* Access 'name' prop */}
        </div>
      );
    }

    export default Greet;
    ```

    *   We added a `props` parameter to the `Greet` function component.
    *   Inside the JSX, we use `{props.name}` to access the value of the `name` prop.  `props` is an object, and `props.name` accesses the property named "name" within that object.

2.  **Pass Props from `App.js`:**

    ```javascript
    import React from 'react';
    import Greet from './components/Greet';

    function App() {
      return (
        <div className="App">
          <Greet name="Bruce" /> {/* Pass 'name' prop with value "Bruce" */}
          <Greet name="Clark" /> {/* Pass 'name' prop with value "Clark" */}
          <Greet name="Diana" /> {/* Pass 'name' prop with value "Diana" */}
        </div>
      );
    }

    export default App;
    ```

    *   In `App.js`, when we use the `<Greet>` tag, we add attributes like `name="Bruce"`, `name="Clark"`, and `name="Diana"`. These attributes become props passed to the `Greet` component.

3.  **View in Browser:** Save and view in the browser. You should see:

    ```
    Hello Bruce
    Hello Clark
    Hello Diana
    ```

    The `Greet` component is now reusable. By passing different `name` props, we can greet different people using the same component.

### Multiple Props

You can pass multiple props to a component. Let's add a `heroName` prop to our `Greet` component.

1.  **Modify `Greet.js` to Accept `heroName` Prop:**

    ```javascript
    import React from 'react';

    const Greet = (props) => {
      return (
        <div>
          <h1>Hello {props.name} also known as {props.heroName}</h1> {/* Access 'heroName' prop */}
        </div>
      );
    }

    export default Greet;
    ```

2.  **Pass `heroName` Props from `App.js`:**

    ```javascript
    import React from 'react';
    import Greet from './components/Greet';

    function App() {
      return (
        <div className="App">
          <Greet name="Bruce" heroName="Batman" /> {/* Pass 'heroName' prop */}
          <Greet name="Clark" heroName="Superman" /> {/* Pass 'heroName' prop */}
          <Greet name="Diana" heroName="Wonder Woman" /> {/* Pass 'heroName' prop */}
        </div>
      );
    }

    export default App;
    ```

3.  **View in Browser:** Save and view in the browser. You should see:

    ```
    Hello Bruce also known as Batman
    Hello Clark also known as Superman
    Hello Diana also known as Wonder Woman
    ```

### `props.children`: Rendering Dynamic Content

The `props` object also has a special property called `children`. **`props.children`**:

> **`props.children`:** A special prop in React that represents the content passed between the opening and closing tags of a component. It allows a component to render dynamic content that is provided by its parent component.

allows you to pass content between the opening and closing tags of a component and render that content within the component.

1.  **Modify `Greet.js` to Render `props.children`:**

    ```javascript
    import React from 'react';

    const Greet = (props) => {
      return (
        <div>
          <h1>Hello {props.name}</h1>
          {props.children} {/* Render 'children' prop */}
        </div>
      );
    }

    export default Greet;
    ```

2.  **Pass Children Content in `App.js`:**

    ```javascript
    import React from 'react';
    import Greet from './components/Greet';

    function App() {
      return (
        <div className="App">
          <Greet name="Bruce" heroName="Batman">
            <p>This is children props</p> {/* Content between tags becomes 'children' */}
          </Greet>
          <Greet name="Clark" heroName="Superman">
            <button>Action</button> {/* Button as children */}
          </Greet>
          <Greet name="Diana" heroName="Wonder Woman" /> {/* No children content */}
        </div>
      );
    }

    export default App;
    ```

    *   For the first two `<Greet>` components, we've added content between the opening and closing tags: a `<p>` tag and a `<button>` tag, respectively. For the third, there's no content between the tags.

3.  **View in Browser:** Save and view in the browser. You should see:

    *   For "Bruce/Batman", the paragraph "This is children props" will be rendered below the greeting.
    *   For "Clark/Superman", the "Action" button will be rendered below the greeting.
    *   For "Diana/Wonder Woman", no additional content will be rendered below the greeting because no children were passed.

### Immutability of Props

**Props are immutable**:

> **Immutable (in programming):**  **Immutable** data means that once an object is created, its state cannot be changed. Any operation that appears to modify an immutable object actually creates a new object with the modified state, leaving the original object unchanged.

This means you **cannot** modify the value of props within a component. Props are read-only from the perspective of the component receiving them.  If you attempt to modify a prop, React will throw an error.

```javascript
// Example of trying to modify a prop (will cause an error)
const Greet = (props) => {
  props.name = "Vishwas"; // This is NOT allowed - will cause an error!
  return (
    <div>
      <h1>Hello {props.name}</h1>
    </div>
  );
}
```

Props are controlled by the parent component that passes them down. Child components should not attempt to alter props.

## State: Managing Component-Local Data

**State**:

> **State (in React):** **State** is a JavaScript object that represents the internal data of a component. Unlike props, which are passed down from parent components, state is managed within the component itself. State is mutable, meaning its values can be changed, and when state changes, React automatically re-renders the component and its children to reflect the updated data in the UI.

is another crucial concept in React. It's used to manage data that can change within a component over time, triggering UI updates.

### Props vs. State: A Comparison

| Feature          | Props                                     | State                                       |
| 