---
layout: "../../layouts/BlogPost.astro"
title: "Vue.js 3 and the Composition API: Building an Expense Tracker - An Educational Guide"
description: ""
pubDate: "2025-02-28"
youtubeVideoID: "hNPwdOZ3qFU"
channel: ""
index: 32
---

# Vue.js 3 and the Composition API: Building an Expense Tracker - An Educational Guide

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/hNPwdOZ3qFU" frameborder="0" allowfullscreen></iframe>

This chapter will guide you through the process of building a simple expense tracker application using Vue.js 3, specifically leveraging the Composition API and the script setup syntax. This project, originally part of a "20 Vanilla JavaScript Projects" course and later adapted for React, serves as an excellent practical example for understanding modern Vue.js development.

## 1. Introduction to Vue.js 3 and the Composition API

Vue.js is a progressive JavaScript framework for building user interfaces. Known for its ease of use and flexibility, Vue.js has become a popular choice for front-end development.  Version 3 of Vue.js introduced significant improvements, most notably the **Composition API**.

> **Vue.js:** A progressive JavaScript framework used for building user interfaces and single-page applications. It is designed to be incrementally adoptable and focuses on the view layer.

Traditionally, Vue.js components were structured using the **Options API**.

> **Options API:**  The original way to structure Vue.js components, where component logic is organized into options like `data`, `methods`, `computed`, and `watch`. This approach groups related logic by option type.

However, Vue.js 3 emphasizes the Composition API as a more organized and efficient way to manage component logic.

### 1.1 Understanding the Composition API

The Composition API is a set of APIs that allows you to author Vue.js components using imported functions instead of declaring options. It aims to improve code reusability, readability, and especially **reactivity**.

> **Reactivity:** In front-end frameworks, reactivity refers to the automatic updating of the user interface (UI) when the underlying data changes. This eliminates the need for manual DOM manipulation.

**Key Benefits of the Composition API:**

*   **Improved Logic Organization:**  The Composition API allows you to group related logic together, regardless of the option type. This leads to more maintainable and understandable code, especially in complex components.
*   **Enhanced Reusability:**  Logic can be extracted into reusable functions (composables), promoting code sharing across components.
*   **Better Readability:**  Code becomes more linear and easier to follow as logic is organized by feature rather than option.
*   **Simplified Reactivity:**  The Composition API provides straightforward ways to establish reactivity, making UI updates more predictable and efficient.

The Composition API contrasts with the Options API by moving away from organizing code by options (like `data`, `methods`, `computed`) and instead focusing on organizing code by *logical features*. This approach often results in cleaner and more scalable component structures.

### 1.2 Project Overview: Expense Tracker Application

This project involves building a web application to track income and expenses.  The application will feature:

*   **Total Balance Display:**  Shows the overall financial balance.
*   **Income and Expense Balances:** Displays separate balances for total income and total expenses.
*   **Transaction History:** A list of all transactions, visually differentiated as income (green border) or expense (red border). Each transaction will include a delete option.
*   **Add Transaction Form:** A form to input new income or expense transactions with descriptions and amounts.
*   **Local Storage Persistence:** Data will be saved in the browser's local storage, ensuring data persistence across sessions.
*   **Toast Notifications:**  Using **View Toastify** to provide user feedback upon adding or deleting transactions.

> **View Toastify:** A Vue.js library used for displaying elegant and non-intrusive notification messages (toasts) to the user.

This project provides a practical context to learn and apply the concepts of Vue.js 3 and the Composition API.

## 2. Project Setup

To begin, ensure you have **Node.js** and **npm** (Node Package Manager) installed on your system. These are essential tools for JavaScript development and managing project dependencies.

> **Node.js:** A JavaScript runtime environment that allows you to run JavaScript code outside of a web browser. It is essential for modern web development tooling.

> **npm (Node Package Manager):** A package manager for JavaScript. It is used to install, manage, and share JavaScript packages and libraries.

### 2.1 Creating a New Vue.js Project with Vue CLI

We will use the **Vue CLI** (Command Line Interface) to quickly scaffold a new Vue.js project.  If you don't have Vue CLI installed globally, you can use `npx` to run it directly without global installation.

> **Vue CLI (Command Line Interface):**  A command-line tool for scaffolding and managing Vue.js projects. It simplifies project setup and development workflows.

Open your terminal and navigate to the directory where you want to create your project. Then, run the following command:

```bash
npx create-vue@latest .
```

The `.` specifies that you want to create the project in the current directory. You will be prompted with a series of questions:

*   **Project name:** Choose a name for your project (e.g., `vue-expense-tracker`).
*   **Add TypeScript?** Select `No`.
*   **Add JSX Support?** Select `No`.
*   **Add Vue Router for Single Page Application development?** Select `No` (for this project, a router is not needed).
*   **Add Pinia for state management?** Select `No` (for this project, Pinia is not necessary).
*   **Add Vitest for Unit testing?** Select `No`.
*   **Add Cypress for E2E testing?** Select `No`.
*   **Add ESLint for code linting?** Select `No`.

After answering these questions, the Vue CLI will generate the basic project structure.  Navigate into your project directory (if you created a subdirectory project) and install the project dependencies using npm:

```bash
npm install
```

To start the development server and see your application in the browser, run:

```bash
npm run dev
```

This will launch a development server, typically accessible at `http://localhost:5173` (the port number may vary).

### 2.2 File Structure Overview

Let's examine the key files and folders in the generated Vue.js project:

*   **`package.json`:** This file contains metadata about your project, including dependencies (libraries your project relies on) and scripts (commands to run development tasks). You'll see `vue` listed under `dependencies` and `vite` under `devDependencies`.

    > **package.json:** A JSON file at the root of a Node.js project that describes the project's dependencies, scripts, and other metadata. It is essential for managing project dependencies and build processes.

*   **`vite.config.js`:**  Configuration file for **Vite**, the development server and build tool used by Vue.js. You can customize development server settings here if needed, like changing the port number.

    > **Vite:** A fast build tool and development server for modern web development. It provides features like hot module replacement and optimized builds.

*   **`index.html`:** The main HTML file for your **Single Page Application (SPA)**. It includes a `<div id="app">` where your Vue.js application will be mounted.

    > **Single Page Application (SPA):** A web application that loads a single HTML page and dynamically updates the content as the user interacts with it, without requiring full page reloads.

*   **`src/main.js`:** The entry point for your Vue.js application. It initializes the Vue application, mounts the main component (`App.vue`), and imports global CSS.

*   **`src/App.vue`:** The root component of your application. It serves as the container for all other components and defines the overall application structure.

*   **`src/assets/`:**  Directory to store assets like CSS files and images.

*   **`src/components/`:**  Directory to store reusable Vue.js components.

*   **`public/`:** Directory for public assets like `favicon.ico` which are served directly without processing by Vite.

### 2.3 Cleaning Up and Setting Up Basic Styles

To start with a clean slate, perform the following cleanup:

1.  **Delete files in `src/assets`:** Delete `base.css`, `logo.svg`, and `main.css`.
2.  **Delete files in `src/components`:** Delete `HelloWorld.vue` and `icons/`.
3.  **Modify `src/App.vue`:** Remove all existing content within the `<template>` and `<script>` tags. Replace the content with:

    ```vue
    <template>
      <div>My App</div>
    </template>

    <script setup>
    </script>

    <style scoped>
    </style>
    ```

4.  **Create `src/assets/style.css`:** Create a new file named `style.css` in the `src/assets` folder. Copy the CSS styles provided in the transcript (or from the linked GitHub repository) and paste them into this file.

5.  **Import `style.css` in `src/main.js`:**  Modify `src/main.js` to import your newly created CSS file:

    ```javascript
    import './assets/style.css'

    import { createApp } from 'vue'
    import App from './App.vue'

    createApp(App).mount('#app')
    ```

6.  **Replace `public/favicon.ico` (Optional):** You can replace the default favicon with a custom one as mentioned in the transcript, or keep the default.

After these steps, your basic Vue.js application should be set up with a basic structure and styling applied. Running `npm run dev` should display "My App" centered on the screen with the styles from `style.css`.

## 3. Component Breakdown

To structure the expense tracker application effectively, we will break down the UI into reusable components. This modular approach makes development more organized and maintainable.  Based on the application's design, we will create the following components:

*   **`Header.vue`:**  Displays the main title of the application ("Expense Tracker").
*   **`Balance.vue`:** Shows the total balance.
*   **`IncomeExpenses.vue`:** Displays the income and expense balances side-by-side.
*   **`TransactionList.vue`:**  Renders the list of transactions, including income and expenses.
*   **`AddTransaction.vue`:** Contains the form to add new transactions.

Create these component files within the `src/components` directory. Each file will have a `.vue` extension and should use PascalCase naming convention (e.g., `Header.vue`, `Balance.vue`).

### 3.1 Creating Components and Basic Structure

For each component file (`Header.vue`, `Balance.vue`, `IncomeExpenses.vue`, `TransactionList.vue`, `AddTransaction.vue`), add the basic Vue.js component structure:

```vue
<template>
  <div>
    <!-- Component Content Here -->
  </div>
</template>

<script setup>
  // Component Logic Here (Composition API)
</script>

<style scoped>
  /* Component Specific Styles Here (optional for now) */
</style>
```

**Populating Components with Basic HTML:**

Refer to the transcript or the provided GitHub repository to copy the basic HTML structure for each component.  Place this HTML within the `<template>` section of each component file. For example, in `Header.vue`, it will be a simple `<h2>` tag. In `Balance.vue`, it will be an `<h4>` and an `<h1>` for the balance amount.

**Importing and Registering Components in `App.vue`:**

To use these components in your main application, you need to import and register them in `App.vue`.  Using the `<script setup>` syntax, component registration is implicit.  Simply import the components at the top of `App.vue` and then use them in the `<template>` section.

```vue
<template>
  <div class="container">
    <Header />
    <Balance />
    <IncomeExpenses />
    <TransactionList />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';
</script>
```

Ensure you add a `div` with the class `container` in `App.vue` to match the CSS styling from `style.css`.

After completing these steps, your application should display the basic layout of the expense tracker, with hardcoded text within each component.  The next step is to implement the dynamic functionality and data handling.

## 4. Implementing Core Functionality

Now we will focus on making the application dynamic and interactive. This involves:

*   Displaying transactions in the `TransactionList` component.
*   Calculating and displaying the balance in the `Balance` component.
*   Calculating and displaying income and expenses in the `IncomeExpenses` component.
*   Implementing the "Add Transaction" form functionality.
*   Adding the "Delete Transaction" functionality.

### 4.1 Displaying Transactions in `TransactionList.vue`

We'll start by displaying a list of transactions in the `TransactionList` component.  For now, we will use hardcoded data in `App.vue` and pass it down to `TransactionList.vue` as **props**.

> **Props (Properties):** Custom attributes you can register on a component. Props allow you to pass data from parent components to child components.

**1. Define Transaction Data in `App.vue`:**

In the `<script setup>` section of `App.vue`, define a reactive array of transaction objects using `ref` from Vue.js.

```vue
<script setup>
import { ref } from 'vue';
// ... other imports

const transactions = ref([
  { id: 1, text: 'Flower', amount: -20 },
  { id: 2, text: 'Salary', amount: 300 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
]);
</script>
```

**2. Pass Transactions as Props to `TransactionList.vue`:**

In `App.vue`'s template, bind the `transactions` ref as a prop to the `<TransactionList>` component.

```vue
<template>
  <div class="container">
    <Header />
    <Balance />
    <IncomeExpenses />
    <TransactionList :transactions="transactions" /> <