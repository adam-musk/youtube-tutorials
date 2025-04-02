---
layout: "../../layouts/BlogPost.astro"
title: "Svelte Crash Course: Building Dynamic User Interfaces"
pubDate: "2025-03-08 15:51:17.760513"
youtubeVideoID: "3TVy6GdtNuQ"
---

# Svelte Crash Course: Building Dynamic User Interfaces

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/3TVy6GdtNuQ" frameborder="0" allowfullscreen></iframe>

## Introduction to Svelte

This chapter provides a comprehensive introduction to Svelte, a modern approach to building web applications. We will explore what Svelte is, how it differs from traditional frameworks like React, and the advantages it offers. We will also set up a development environment and begin building a practical project to solidify our understanding.

### What is Svelte?

Svelte is fundamentally a **compiler** that transforms your code into highly optimized JavaScript.

> **Compiler:** In computer science, a compiler is a special program that translates source code written in a programming language (the source language) into another computer language (the target language, often machine code or bytecode). In the context of Svelte, it takes Svelte code and compiles it into optimized JavaScript.

While technically a compiler, Svelte is often referred to and functions much like a front-end framework. It empowers developers to create reusable user interface (UI) components, manage application logic, and handle styling, similar to frameworks like React, Vue, and Angular. Svelte is well-suited for building **Single Page Applications (SPAs)**, offering a modern and efficient approach to web development.

> **Single Page Application (SPA):** A web application that loads a single HTML page and dynamically updates the content as the user interacts with it, without requiring full page reloads. This provides a more fluid and responsive user experience.

### Svelte vs. React: Compiler vs. Virtual DOM

A key distinction between Svelte and frameworks like React lies in their operational mechanisms. Svelte operates at **compile time**, processing your code and generating optimized, vanilla JavaScript before it even reaches the browser. This contrasts sharply with React's approach, which relies on a **Virtual DOM** for runtime interpretation.

> **Virtual DOM (Virtual Document Object Model):** A programming concept where a virtual representation of a UI is kept in memory and synced with the real DOM.  React uses the Virtual DOM to efficiently update the actual DOM by comparing the virtual representation with the previous state and applying only the necessary changes.

React's Virtual DOM, while powerful, introduces runtime overhead.  It involves maintaining a virtual representation of the UI, comparing it to the actual DOM, and then updating the DOM as needed. Svelte, by contrast, eliminates this overhead by performing the bulk of the work during compilation.  This results in leaner, faster, and more efficient JavaScript code delivered to the browser.

### Advantages of Using Svelte

Choosing Svelte for front-end development offers several compelling advantages:

*   **Optimized JavaScript Code:** Svelte's compiler produces highly optimized JavaScript with minimal overhead. This leads to faster loading times and improved runtime performance.
*   **No Virtual DOM:** By eliminating the Virtual DOM, Svelte avoids the performance bottlenecks associated with runtime UI interpretation and reconciliation.
*   **Performance Benefits:**  While performance can vary based on specific application needs and benchmarks, Svelte generally exhibits faster performance compared to frameworks employing a Virtual DOM.
*   **Built-in Animations and Transitions:** Svelte provides intuitive and easy-to-use mechanisms for incorporating animations and transitions directly into your UI components, enhancing user experience.
*   **Evolving Ecosystem:** Svelte boasts a growing ecosystem, including:
    *   **SvelteKit:** A framework for building server-side rendered Svelte applications, analogous to Next.js for React.
        > **Server-Side Rendering (SSR):**  Rendering web application pages on the server instead of in the browser.  SSR can improve initial load times and SEO (Search Engine Optimization).
    *   **Svelte Native:** A tool for building native mobile applications using Svelte.
*   **Ease of Use and Learning Curve:**  Svelte is often praised for its simplicity and ease of learning, particularly for developers familiar with HTML, CSS, and JavaScript. It often requires less code to achieve the same functionality compared to some other frameworks.

### Prerequisites

Before diving into Svelte development, a solid understanding of the following concepts is essential:

*   **JavaScript Fundamentals:** A strong grasp of core JavaScript concepts is crucial. This includes:
    *   Functions
    *   Loops
    *   Asynchronous programming (Promises, `async/await`)
    *   Array methods (e.g., `forEach`, `map`, `filter`)
    *   Fetch API (for making network requests)
*   **Node Package Manager (npm):** Familiarity with npm for installing packages, managing project dependencies, and running development scripts is necessary.

    > **Node Package Manager (npm):** A package manager for the JavaScript programming language. It is the default package manager for the Node.js JavaScript runtime environment. npm is used to install, share, and manage dependencies for JavaScript projects.

## Svelte Components: Building Blocks of UI

Like other modern front-end frameworks, Svelte utilizes a component-based architecture. Components are reusable, self-contained units of UI, encapsulating markup, logic, and styling.

### Component Structure

Svelte components are similar in structure to Vue.js components, offering a clear and organized way to build user interfaces. Key characteristics of Svelte components include:

*   **File Extension:** Svelte components are saved with the `.svelte` file extension.
*   **Structure:** A typical Svelte component file is structured into three main sections:
    *   **`<script>` tags (Logic):**  JavaScript code for component logic, variables, and functions is placed within `<script>` tags at the top of the file.
    *   **HTML Markup (Output):**  HTML code defining the component's output, rendered in the middle section of the file.  Dynamic content and expressions are embedded using curly braces `{}`.
    *   **`<style>` tags (Styling):** CSS styles specific to the component are enclosed within `<style>` tags at the bottom of the file. These styles are scoped to the component by default.

### Getting Started with Svelte: Project Setup

Several methods exist to initiate a Svelte project. While **SvelteKit** offers advanced features like server-side rendering and routing, the simplest approach for a basic Single Page Application is using the `degit` scaffolding tool.

> **Scaffolding Tool:** A programming utility that generates basic project structures, files, and configurations, allowing developers to quickly start a new project with a pre-defined setup. `degit` is a tool specifically designed for scaffolding projects from GitHub repositories.

**Using `degit`:**

1.  **Open your terminal** and navigate to the directory where you want to create your project.
2.  **Run the following command:**

    ```bash
    npx degit sveltejs/template svelte-feedback-app
    ```

    *   `npx` allows you to run npm packages without installing them globally.
    *   `degit sveltejs/template` instructs `degit` to clone the Svelte.js template repository from GitHub.
    *   `svelte-feedback-app` is the desired name for your project folder.

3.  **Navigate into the project directory:**

    ```bash
    cd svelte-feedback-app
    ```

4.  **Install dependencies:**

    ```bash
    npm install
    ```

This process sets up a basic Svelte project with essential configurations, a development server, and a module bundler.

### Project Structure Overview

After setting up the project, the directory structure will contain:

*   **`public` folder:** Contains static assets like `index.html`, global CSS (`global.css`), and the bundled JavaScript and CSS output for production.
    *   `index.html`: The main HTML file for the Single Page Application.  Svelte UI will be bound to the `<body>` element within this file.
    *   `bundle.js`: The compiled and bundled JavaScript code for the application, generated after building the project.
    *   `global.css`:  File for global CSS styles that apply across the entire application.
    *   `bundle.css`: CSS styles extracted from Svelte components, bundled for production.
*   **`src` folder:** Contains the source code of your Svelte application.
    *   `main.js`: The entry point of the application, responsible for initializing the main `App` component and mounting it to the `document.body`.
    *   `App.svelte`: The root component of your application.
*   **`scripts` folder:**  May contain scripts for tasks like setting up TypeScript.
*   **`package.json`:** Defines project dependencies, scripts for development and production, and project metadata.
*   **`rollup.config.js` (or `vite.config.js`):** Configuration file for the **module bundler**, specifying how modules are bundled for production. Rollup is the default bundler, but Vite is another popular alternative.

    > **Module Bundler:** A tool that combines and packages JavaScript modules, along with their dependencies, into single or a few files that are optimized for browser loading. Rollup and Vite are popular module bundlers used in modern web development.

**Development and Build Scripts (defined in `package.json`):**

*   `npm run dev`: Starts the **development server** using Rollup with **live reload**. This server hosts your application during development, automatically rebuilding and refreshing the browser when code changes are detected.
    > **Development Server:** A local server used during development to host and serve web application files. It typically provides features like hot reloading and proxying to simplify the development workflow.
    > **Live Reload:** A development server feature that automatically refreshes the browser whenever changes are made to the project's source code, providing immediate feedback during development.
*   `npm run build`: Compiles your Svelte code into optimized JavaScript and CSS for production, creating a `build` folder within the `public` directory.
*   `npm run serve`:  Serves the production-ready `public` folder, simulating a production environment.

**VS Code Extension:**

For Visual Studio Code users, installing the "Svelte for VS Code" extension is highly recommended. This extension provides features like:

*   Syntax highlighting for `.svelte` files.
*   Code formatting.
*   Auto-completions.
*   Emmet support within Svelte components.

## Svelte Fundamentals: Core Concepts

Let's explore some fundamental Svelte concepts through practical examples within the `App.svelte` component.

### Reactive Declarations (`$:` syntax)

Svelte introduces the concept of **reactive declarations** using the `$:`. This syntax allows you to create variables that automatically update whenever their dependencies change.

```svelte
<script>
  let firstName = 'Brad';
  let lastName = 'Traversy';

  $: name = `${firstName} ${lastName}`; // Reactive declaration

  // ... rest of script
</script>

<h1>Hello {name}</h1>
```

In this example, `name` is a reactive variable. Whenever `firstName` or `lastName` changes, `name` will automatically re-evaluate and update the displayed greeting in the `<h1>` tag.

### Event Handling

Svelte simplifies event handling within components. You can directly attach event listeners to HTML elements using the `on:` directive.

```svelte
<script>
  let color = 'blue';

  function toggleColor() {
    color = color === 'blue' ? 'red' : 'blue';
  }
</script>

<h1 style="color: {color}">Hello</h1>
<button on:click={toggleColor}>Click</button>
```

Here, `on:click={toggleColor}` attaches a click event listener to the `<button>`. When the button is clicked, the `toggleColor` function is executed, changing the `color` variable and reactively updating the `<h1>` style.

### Conditional Rendering (`{#if}`)

Svelte provides a straightforward syntax for conditional rendering using `{#if}`, `{:else}`, and `{:else if}` blocks.

```svelte
<script>
  let showText = false;

  function toggleText() {
    showText = !showText;
  }
</script>

<button on:click={toggleText}>Toggle Text</button>

{#if showText}
  <p>This text is conditionally rendered.</p>
{:else}
  <p>No text to show.</p>
{/if}
```

The `{#if showText}` block conditionally renders the first `<p>` element when `showText` is true. Otherwise, the `{:else}` block renders the second `<p>` element.

### List Rendering (`{#each}`)

Rendering lists of data in Svelte is handled using the `{#each}` block.

```svelte
<script>
  let users = [
    { id: 1, name: 'John' },
    { id: 2, name: 'Sarah' },
    { id: 3, name: 'Bob' }
  ];

  function addUser() {
    users = [...users, { id: 4, name: 'Gen' }];
  }
</script>

<button on:click={addUser}>Add User</button>

{#each users as user (user.id)}
  <h3>{user.id}: {user.name}</h3>
{/each}
```

The `{#each users as user (user.id)}` block iterates over the `users` array. For each `user`, it renders an `<h3>` element displaying the user's `id` and `name`. The `(user.id)` part specifies a unique key for each item, which is important for efficient list updates.

## Building a Feedback Application: Practical Project

To solidify our understanding of Svelte, we will build a practical feedback application. This project will demonstrate component creation, state management, event handling, and more.

### Project Overview: Feedback App

The feedback application will allow users to:

*   Select a rating (1-10).
*   Provide text-based feedback.
*   Submit feedback.
*   View a list of submitted feedback items.
*   See statistics: total number of feedback items and average rating.
*   Delete individual feedback items.

This project will involve creating several Svelte components and implementing core application logic.

### Setting up the Project

If you haven't already, follow the steps outlined in "Getting Started with Svelte: Project Setup" to create a new Svelte project named `svelte-feedback-app` using `degit`.

### Component Breakdown

Our feedback application will be structured using the following components:

*   **`Card.svelte`:** A reusable container component to provide a consistent card-like styling with rounded corners and padding.
*   **`FeedbackItem.svelte`:**  Displays a single feedback item, including the rating, feedback text, and a delete button.
*   **`FeedbackList.svelte`:** Renders a list of `FeedbackItem` components, handling the display of all feedback items.
*   **`FeedbackStats.svelte`:**  Displays statistics about the feedback data, such as the total number of reviews and the average rating.
*   **`FeedbackForm.svelte`:**  Provides a form for users to submit feedback, including rating selection and text input.
*   **`RatingSelect.svelte`:** A component specifically for selecting a rating using stylized radio buttons.
*   **`Button.svelte`:** A reusable button component with customizable styles (primary, secondary, disabled).

### Implementing Core Features

Let's walk through the implementation of key features in our feedback application, component by component.

#### Card Component (`Card.svelte`)

The `Card` component will be a simple wrapper to apply consistent styling to other components.

```svelte
<div class="card">
  <slot />
</div>

<style>
  .card {
    background-color: white;
    border-radius: 15px;
    padding: 40px 50px;
    margin: 20px 0;
    position: relative; /* For absolute positioning of elements within */
    color: #333;
  }
</style>
```

> **Slot:** A placeholder within a component's template that allows content to be inserted from the parent component. The `<slot>` element in `Card.svelte` indicates where the content passed within the `<Card>` tags in parent components will be rendered.

The `<slot />` element acts as a placeholder where content passed between the `<Card>` tags in a parent component will be injected.

#### Feedback Item Component (`FeedbackItem.svelte`)

The `FeedbackItem` component will display individual feedback entries.

```svelte
<script>
  import Card from './Card.svelte';
  import { createEventDispatcher } from 'svelte';

  export let item; // Prop to receive feedback item data

  const dispatch = createEventDispatcher();

  function handleDelete(id) {
    dispatch('delete-feedback', id); // Dispatch custom event
  }
</script>

<Card>
  <div class="num-display">{item.rating}</div>
  <button class="close" on:click={() => handleDelete(item.id)}>X</button>
  <div class="text-display">{item.text}</div>
</Card>

<style>
  .num-display { /* ... styling for rating number ... */ }
  .close { /* ... styling for delete button ... */ }
  .text-display { /* ... styling for feedback text ... */ }
</style>
```

*   **`export let item;`**: Declares `item` as a **prop**, allowing `FeedbackList` to pass feedback data to `FeedbackItem`.
    > **Prop (Property):**  A mechanism for passing data from a parent component to a child component. In Svelte, props are declared using `export let` in the child component.
*   **`createEventDispatcher()`**:  A function from Svelte used to create a **custom event dispatcher** within the component.
    > **Event Dispatcher:** A function that allows a component to emit custom events that can be listened to by parent components. This is a mechanism for child components to communicate with their parents.
*   **`dispatch('delete-feedback', item.id)`**: Dispatches a custom event named `delete-feedback` when the delete button is clicked, passing the `item.id` as data.
*   The component uses the `Card` component to wrap its content and includes styling for displaying the rating number, delete button, and feedback text.

#### Feedback List Component (`FeedbackList.svelte`)

The `FeedbackList` component will render a list of `FeedbackItem` components.

```svelte
<script>
  import FeedbackItem from './FeedbackItem.svelte';
  import { fade, scale } from 'svelte/transition'; // Import transitions

  export let feedback = []; // Prop to receive feedback data
</script>

{#each feedback as fb (fb.id)}
  <div in:scale out:fade={{ duration: 200 }}> {/* Apply transitions */}
    <FeedbackItem item={fb} on:delete-feedback /> {/* Render FeedbackItem and forward event */}
  </div>
{/each}

{#if feedback.length === 0}
  <p>No Feedback Yet</p>
{/if}
```

*   **`export let feedback = [];`**: Declares `feedback` as a prop to receive the array of feedback items from the parent component (`App.svelte` initially).
*   **`{#each feedback as fb (fb.id)}`**: Iterates over the `feedback` array to render a `FeedbackItem` for each item.
*   **`<div in:scale out:fade={{ duration: 200 }}`**: Applies **transitions** to the `<div>` wrapping the `FeedbackItem`. `scale` is used for the "in" transition (when added), and `fade` is used for the "out" transition (when removed).
    > **Transition:**  Visual effects that animate the appearance or disappearance of elements in the DOM. Svelte provides built-in transitions like `fade`, `scale`, and `slide`, and allows for customization of duration and easing.
*   **`on:delete-feedback`**:  **Event forwarding**.  This line ensures that any `delete-feedback` events dispatched by `FeedbackItem` components within the list are automatically forwarded up to the parent component of `FeedbackList` (which is `App.svelte` initially).

#### Feedback Stats Component (`FeedbackStats.svelte`)

The `FeedbackStats` component will display feedback statistics.

```svelte
<script>
  export let feedback = []; // Prop to receive feedback data

  $: average = feedback.length > 0
    ? feedback.reduce((total, item) => total + item.rating, 0) / feedback.length
    : 0;

  $: count = feedback.length;
</script>

<div class="feedback-stats">
  <h4>Reviews: {count}</h4>
  <h4>Rating Average: {average.toFixed(1)}</h4>
</div>

<style>
  .feedback-stats { /* ... styling for stats display ... */ }
</style>
```

*   **`export let feedback = [];`**: Declares `feedback` as a prop to receive the feedback data.
*   **`$: average = ...`**:  A reactive declaration that calculates the average rating based on the `feedback` array. It uses `reduce` to sum the ratings and divides by the length. It handles the case of an empty array to avoid division by zero.
*   **`$: count = feedback.length;`**: A reactive declaration that calculates the feedback count.
*   The component displays the `count` and `average` in `<h4>` elements with appropriate labels.

#### Feedback Form Component (`FeedbackForm.svelte`)

The `FeedbackForm` component will handle user feedback submission.

```svelte
<script>
  import RatingSelect from './RatingSelect.svelte';
  import Button from './Button.svelte';
  import Card from './Card.svelte';
  import { v4 as uuidv4 } from 'uuid'; // Import UUID library

  let text = '';
  let rating = 10; // Default rating
  let message = null;
  let btnDisabled = true;
  let min = 10;

  function handleInput() {
    if (text.trim().length <= min) {
      message = `Text must be at least ${min} characters`;
      btnDisabled = true;
    } else {
      message = null;
      btnDisabled = false;
    }
  }

  function handleSelect(event) {
    rating = +event.detail; // Update rating from RatingSelect event
  }

  function handleSubmit() {
    if (text.trim().length > min) {
      const newFeedback = {
        id: uuidv4(),
        rating: +rating,
        text: text.trim()
      };
      // Dispatch custom event to add feedback (initially)
      text = ''; // Clear input field
    }
  }
</script>

<Card>
  <form on:submit|preventDefault={handleSubmit}> {/* Prevent default form submission */}
    <header>
      <h2>How would you rate your service?</h2>
    </header>
    <RatingSelect on:rating-select={handleSelect} /> {/* RatingSelect component */}
    <div class="input-group">
      <input
        type="text"
        placeholder="Tell us something that keeps you coming back"
        on:input={handleInput}
        bind:value={text} // Two-way binding for input value
      />
      <Button type="submit" disabled={btnDisabled}>Send</Button> {/* Button component */}
    </div>

    {#if message}
      <div class="message">{message}</div>
    {/if}
  </form>
</Card>

<style>
  /* ... styling for form elements ... */
</style>
```

*   **`import { v4 as uuidv4 } from 'uuid';`**: Imports the `uuidv4` function from the `uuid` library to generate unique IDs for feedback items.
*   **`let text = ''; let rating = 10; ...`**: Declares variables to manage form state: `text` for input value, `rating` for selected rating, `message` for validation messages, `btnDisabled` to control button state, and `min` for minimum text length.
*   **`handleInput()`**: Function called on input event to perform real-time validation of the text input. It updates `message` and `btnDisabled` based on text length.
*   **`handleSelect(event)`**: Function called when the `rating-select` custom event is dispatched from `RatingSelect`. It updates the `rating` variable with the selected rating value from `event.detail`.
*   **`handleSubmit()`**: Function called on form submission (preventing default form submission using `on:submit|preventDefault`). It validates the text length again and, if valid, creates a `newFeedback` object with a unique ID, rating, and text. (Initially, this function would dispatch a custom event to add feedback).
*   **`bind:value={text}`**: **Two-way binding**. This directive creates a two-way binding between the `text` variable in the script and the `value` property of the `<input>` element. Changes in the input field update the `text` variable, and vice versa.
    > **Two-Way Binding:** A synchronization mechanism that links a variable in the component's script to an input element's value. Changes to either the variable or the input field are reflected in the other.
*   **`on:submit|preventDefault={handleSubmit}`**: Attaches a submit event listener to the `<form>` element and calls `handleSubmit` when the form is submitted. `|preventDefault` is an **event modifier** that prevents the default form submission behavior (page reload).
    > **Event Modifier:** Special suffixes that can be added to Svelte event directives (`on:`) to modify event handling behavior. `preventDefault` is a modifier that calls `event.preventDefault()` automatically.
*   The component utilizes `RatingSelect`, `Button`, and `Card` components and includes styling for form elements and validation messages.

#### Rating Select Component (`RatingSelect.svelte`)

The `RatingSelect` component provides stylized radio buttons for rating selection.

```svelte
<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  let selected = 10; // Default selected rating

  function onChange(e) {
    selected = +e.currentTarget.value; // Update selected rating
    dispatch('rating-select', selected); // Dispatch custom event
  }
</script>

<ul class="rating">
  {#each Array(10) as _, i}
    <li>
      <input
        type="radio"
        id={'num' + (i + 1)}
        name="rating"
        value={i + 1}
        checked={selected === i + 1}
        on:change={onChange}
      />
      <label for={'num' + (i + 1)}>{i + 1}</label>
    </li>
  {/each}
</ul>

<style>
  /* ... styling for rating radio buttons ... */
</style>
```

*   **`createEventDispatcher()`**: Used to create a custom event dispatcher.
*   **`let selected = 10;`**: Initializes the `selected` rating to 10 by default.
*   **`onChange(e)`**: Function called when a radio button is changed. It updates the `selected` rating and dispatches a `rating-select` custom event with the selected value.
*   **`{#each Array(10) as _, i}`**:  Uses `{#each}` to loop 10 times, creating radio buttons for ratings 1 to 10.
*   **`checked={selected === i + 1}`**: Dynamically sets the `checked` attribute of the radio button based on the `selected` value.
*   **`on:change={onChange}`**: Attaches a change event listener to each radio button, calling the `onChange` function.

#### Button Component (`Button.svelte`)

The `Button` component is a reusable button with customizable styles.

```svelte
<script>
  export let type = 'primary'; // Prop for button type (primary or secondary)
  export let disabled = false;  // Prop for disabled state
</script>

<button
  class="btn"
  class:btn-primary={type === 'primary'}
  class:btn-secondary={type === 'secondary'}
  {disabled} // Shorthand for disabled={disabled}
  on:click
  on:submit
>
  <slot />
</button>

<style>
  /* ... styling for button component ... */
</style>
```

*   **`export let type = 'primary';`**: Declares a `type` prop with a default value of 'primary'. This prop determines the button's style (primary or secondary).
*   **`export let disabled = false;`**: Declares a `disabled` prop to control the button's disabled state.
*   **`class:btn-primary={type === 'primary'} class:btn-secondary={type === 'secondary'}`**: **Class directives**. These directives conditionally add CSS classes to the button element based on the `type` prop. If `type` is 'primary', `btn-primary` class is added; if 'secondary', `btn-secondary` is added.
    > **Class Directive:** A Svelte directive (`class:`) that allows conditionally adding or removing CSS classes from an HTML element based on a boolean expression.
*   **`{disabled}`**: Shorthand syntax for `disabled={disabled}`. If `disabled` is true, the `disabled` attribute is added to the button.
*   **`on:click on:submit`**:  Forwards click and submit events. By including these, any `on:click` or `on:submit` event listeners attached to the `<Button>` component from its parent will be forwarded to the underlying `<button>` element.

#### Implementing in `App.svelte`

Finally, let's integrate these components and implement the application logic in `App.svelte`.

**Initial `App.svelte` (with prop passing and event handling):**

```svelte
<script>
  import FeedbackList from './components/FeedbackList.svelte';
  import FeedbackStats from './components/FeedbackStats.svelte';
  import FeedbackForm from './components/FeedbackForm.svelte';

  let feedback = [ // Initial feedback data
    { id: 1, rating: 10, text: 'Great service!' },
    { id: 2, rating: 8, text: 'Good experience overall.' },
    { id: 3, rating: 9, text: 'Will recommend to others.' }
  ];

  function deleteFeedback(event) {
    feedback = feedback.filter(item => item.id !== event.detail);
  }

  function addFeedback(event) {
    feedback = [event.detail, ...feedback];
  }
</script>

<main class="container">
  <FeedbackForm on:add-feedback={addFeedback} />
  <FeedbackStats feedback={feedback} />
  <FeedbackList feedback={feedback} on:delete-feedback={deleteFeedback} />
</main>

<style>
  .container { /* ... styling for container ... */ }
</style>
```

*   **`import` statements**: Imports the necessary components.
*   **`let feedback = [...]`**: Initializes the `feedback` array with sample data.
*   **`deleteFeedback(event)`**: Function to handle `delete-feedback` custom events from `FeedbackList`. It filters the `feedback` array, removing the item with the specified ID from `event.detail`.
*   **`addFeedback(event)`**: Function to handle `add-feedback` custom events from `FeedbackForm`. It adds the new feedback item from `event.detail` to the beginning of the `feedback` array.
*   **Component instantiation**:  Instantiates `FeedbackForm`, `FeedbackStats`, and `FeedbackList` components.
    *   `on:add-feedback={addFeedback}`: Listens for the `add-feedback` custom event from `FeedbackForm` and calls the `addFeedback` function.
    *   `feedback={feedback}`: Passes the `feedback` array as a prop to `FeedbackStats` and `FeedbackList`.
    *   `on:delete-feedback={deleteFeedback}`: Listens for the `delete-feedback` custom event from `FeedbackList` and calls the `deleteFeedback` function.

#### Deleting Feedback Items

In `FeedbackItem.svelte`, we already implemented the dispatch of the `delete-feedback` custom event. In `App.svelte` (initial version), we implemented the `deleteFeedback` function to handle this event and update the `feedback` array.

#### Displaying Feedback Statistics

In `FeedbackStats.svelte`, we calculate and display the feedback count and average rating based on the `feedback` prop. In `App.svelte` (initial version), we pass the `feedback` array as a prop to `FeedbackStats`.

#### Building the Feedback Form

In `FeedbackForm.svelte`, we created the form structure, input validation, and the `handleSubmit` function (initially designed to dispatch an `add-feedback` event).

#### Form Validation

The `handleInput` function in `FeedbackForm.svelte` implements real-time validation for the feedback text input, displaying an error message and disabling the submit button if the text is too short.

#### Rating Selection Component

`RatingSelect.svelte` provides the UI for rating selection using stylized radio buttons and dispatches a `rating-select` custom event with the selected rating value.

#### Form Submission and Adding Feedback

In `FeedbackForm.svelte`, the `handleSubmit` function (initial version) was designed to dispatch an `add-feedback` custom event when the form is submitted.  In `App.svelte` (initial version), the `addFeedback` function handles this event and updates the `feedback` array.

#### State Management with Stores

To simplify state management and component communication, we can utilize Svelte **stores**. Stores are objects that hold reactive data and allow components to subscribe to and update that data.

> **Store:** In Svelte, a store is an object that holds reactive data and allows components to subscribe to changes in that data. Stores provide a centralized and efficient way to manage application state and share data between components without prop drilling or complex event handling.

**Creating a Store (`stores.js`):**

Create a new file `stores.js` in the `src` directory:

```javascript
import { writable } from 'svelte/store';

export const feedbackStore = writable([ // Initial feedback data in store
  { id: 1, rating: 10, text: 'Great service!' },
  { id: 2, rating: 8, text: 'Good experience overall.' },
  { id: 3, rating: 9, text: 'Will recommend to others.' }
]);
```

*   **`import { writable } from 'svelte/store';`**: Imports the `writable` store factory from Svelte's store module.
*   **`export const feedbackStore = writable([...]);`**: Creates a **writable store** named `feedbackStore` and initializes it with the feedback data array. `writable` stores allow components to both read and update the store's value.

**Updating Components to Use Stores:**

1.  **`App.svelte` (Store-based):**

    ```svelte
    <script>
      import FeedbackList from './components/FeedbackList.svelte';
      import FeedbackStats from './components/FeedbackStats.svelte';
      import FeedbackForm from './components/FeedbackForm.svelte';
    </script>

    <main class="container">
      <FeedbackForm /> {/* No event listener needed */}
      <FeedbackStats />  {/* No prop needed */}
      <FeedbackList />   {/* No prop needed */}
    </main>

    <style>
      .container { /* ... styling for container ... */ }
    </style>
    ```

    *   `App.svelte` is significantly simplified. It no longer needs to manage the `feedback` array or handle custom events. Components will now interact directly with the `feedbackStore`.

2.  **`FeedbackList.svelte` (Store-based):**

    ```svelte
    <script>
      import FeedbackItem from './FeedbackItem.svelte';
      import { fade, scale } from 'svelte/transition';
      import { feedbackStore } from '../stores'; // Import the store

      $: feedbackItems = $feedbackStore; // Subscribe to store using $ prefix
    </script>

    {#each feedbackItems as fb (fb.id)}
      <div in:scale out:fade={{ duration: 200 }}>
        <FeedbackItem item={fb} /> {/* No event listener needed */}
      </div>
    {/each}

    {#if $feedbackStore.length === 0} {/* Access store value directly */}
      <p>No Feedback Yet</p>
    {/if}
    ```

    *   **`import { feedbackStore } from '../stores';`**: Imports the `feedbackStore` from `stores.js`.
    *   **`$: feedbackItems = $feedbackStore;`**:  Subscribes to the `feedbackStore` using the **`$` prefix**. The `$` prefix in Svelte automatically subscribes to a store and updates the variable (`feedbackItems` in this case) whenever the store's value changes. When the component is destroyed, Svelte automatically unsubscribes from the store, preventing memory leaks.
    *   **`{#if $feedbackStore.length === 0}`**: Accesses the current value of the `feedbackStore` directly using the `$` prefix to check the length.

3.  **`FeedbackStats.svelte` (Store-based):**

    ```svelte
    <script>
      import { feedbackStore } from '../stores';

      $: feedbackItems = $feedbackStore; // Subscribe to store

      $: average = feedbackItems.length > 0
        ? feedbackItems.reduce((total, item) => total + item.rating, 0) / feedbackItems.length
        : 0;

      $: count = feedbackItems.length;
    </script>

    <div class="feedback-stats">
      <h4>Reviews: {count}</h4>
      <h4>Rating Average: {average.toFixed(1)}</h4>
    </div>

    <style>
      .feedback-stats { /* ... styling for stats display ... */ }
    </style>
    ```

    *   `FeedbackStats` is also updated to use the `feedbackStore` directly, eliminating the need for the `feedback` prop.

4.  **`FeedbackItem.svelte` (Store-based):**

    ```svelte
    <script>
      import Card from './Card.svelte';
      import { feedbackStore } from '../stores'; // Import the store

      export let item;

      function handleDelete(id) {
        feedbackStore.update((currentFeedback) => { // Update store directly
          return currentFeedback.filter(item => item.id !== id);
        });
      }
    </script>

    <Card>
      <div class="num-display">{item.rating}</div>
      <button class="close" on:click={() => handleDelete(item.id)}>X</button>
      <div class="text-display">{item.text}</div>
    </Card>

    <style>
      /* ... styling for feedback item ... */
    </style>
    ```

    *   **`import { feedbackStore } from '../stores';`**: Imports the `feedbackStore`.
    *   **`feedbackStore.update(...)`**:  Uses the `update` method of the `feedbackStore` to modify the store's data. The `update` method takes a callback function that receives the current store value (`currentFeedback`) and returns the new store value. In this case, it filters the `currentFeedback` array to remove the item with the specified `id`.

5.  **`FeedbackForm.svelte` (Store-based):**

    ```svelte
    <script>
      import RatingSelect from './RatingSelect.svelte';
      import Button from './Button.svelte';
      import Card from './Card.svelte';
      import { v4 as uuidv4 } from 'uuid';
      import { feedbackStore } from '../stores'; // Import the store

      // ... (variables and handleInput/handleSelect functions remain the same)

      function handleSubmit() {
        if (text.trim().length > min) {
          const newFeedback = {
            id: uuidv4(),
            rating: +rating,
            text: text.trim()
          };
          feedbackStore.update((currentFeedback) => { // Update store directly
            return [newFeedback, ...currentFeedback];
          });
          text = '';
        }
      }

      // ... (rest of component template remains the same)
    </script>
    ```

    *   **`import { feedbackStore } from '../stores';`**: Imports the `feedbackStore`.
    *   **`feedbackStore.update(...)`**: In `handleSubmit`, the `update` method of `feedbackStore` is used to add the `newFeedback` item to the store. The callback function prepends the `newFeedback` item to the `currentFeedback` array.

By using stores, we have achieved a more streamlined and maintainable application architecture. Components can now access and modify the shared feedback data directly through the `feedbackStore`, eliminating prop drilling and complex event propagation.

#### Adding Transitions

Transitions enhance the user experience by providing visual feedback when elements are added or removed from the DOM. In `FeedbackList.svelte`, we already added scale-in and fade-out transitions to the `<div>` wrapping each `FeedbackItem`.

### Deployment

To deploy your Svelte application, you first need to build it for production:

```bash
npm run build
```

This command compiles your Svelte code and generates optimized files in the `public/build` directory. You can then deploy the contents of the `public` directory to a static hosting service like Vercel, Netlify, or GitHub Pages. Vercel is often recommended for its ease of use and excellent integration with SvelteKit and other modern front-end frameworks.

## Conclusion

This chapter has provided a comprehensive introduction to Svelte, covering its core concepts, component structure, and practical application through the development of a feedback application. We explored the advantages of Svelte's compiler-based approach, learned how to build reusable components, manage state effectively with stores, handle events, and add transitions for enhanced user experience. By building this project, you have gained a solid foundation for further exploration and development with Svelte.
