---
layout: "../../layouts/BlogPost.astro"
title: "Mastering React Development: Top Do's and Don'ts for JavaScript Engineers"
pubDate: "2025-03-01 14:16:00.851822"
youtubeVideoID: "4FhJkX18fS8"
index:
---

# Mastering React Development: Top Do's and Don'ts for JavaScript Engineers

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/4FhJkX18fS8" frameborder="0" allowfullscreen></iframe>


This chapter provides a comprehensive guide to enhancing your React development skills, drawing upon expert insights into best practices and common pitfalls. We will explore key principles and techniques to help you write cleaner, more efficient, and maintainable React applications.

## 1. Embrace Functional Components and Hooks

### 1.1 The Shift Away from Class Components

One of the fundamental shifts in modern React development is the move towards functional components and away from class-based components.  While class components were historically prevalent, functional components have emerged as the recommended approach for building React applications.

> **Class Components:** In React, class components are JavaScript classes that extend `React.Component` and have state and lifecycle methods. They were the original way to create stateful components in React.

> **Functional Components:** Functional components are JavaScript functions that can accept props as an argument and return JSX. With the introduction of Hooks, they can now also manage state and lifecycle effects, making them as powerful as class components.

**Key Takeaways:**

*   **Future of React:** Functional components are considered the future of React development, as evidenced by their prominence in official React documentation and new beta resources.
*   **Documentation Emphasis:**  Finding examples and documentation for class components is becoming increasingly difficult, especially on React's beta documentation sites, highlighting the focus on functional components.

### 1.2 Superior State Management with Hooks

Functional components offer a more streamlined and reactive approach to state management through the use of Hooks.

> **Hooks:** Hooks are functions in React that let you "hook into" React state and lifecycle features from within functional components. They were introduced to make state and other React features available in functional components, eliminating the need for class components for stateful logic.

**Benefits of Hooks:**

*   **Reactive State Model:** Hooks like `useState` and `useReducer` provide a built-in reactive state management model directly within React.
*   **Ecosystem of Hooks:** A vast ecosystem of hooks has emerged, addressing various needs from API interactions and external state management to CSS animations and more.
*   **Accessibility of Hooks:**  Functional components gain access to this rich ecosystem of hooks, which is not available to class-based components.
*   **Steeper Learning Curve - An Advantage:** While initially perceived as having a steeper learning curve, learning functional components and hooks first makes it easier to adapt to class components later if needed in legacy projects.

**Essential Hooks for State Management:**

*   **`useState`:**  Declares state variables within a functional component.
*   **`useReducer`:** Provides a more complex state management option, similar to Redux, for managing intricate state transitions.
*   **`useEffect`:**  Handles side effects in functional components, such as data fetching, subscriptions, or manually changing the DOM.
*   **`useCallback`:**  Memoizes functions to prevent unnecessary re-renders, particularly useful for optimizing performance with child components that rely on referential equality.
*   **`useMemo`:** Memoizes the result of a computation, ensuring that expensive calculations are only performed when their dependencies change.

## 2. Understand Functional Components as Functions, Not Templates

### 2.1 Avoiding the "Template Thinking" Trap

A common misconception among developers new to React is to think of functional components as simple templates that generate JSX and then operate independently. This "template thinking" can lead to bugs and misunderstandings about React's rendering process.

> **JSX (JavaScript XML):**  JSX is a syntax extension to JavaScript that looks similar to HTML. It is used in React to describe the user interface and is transformed into regular JavaScript function calls by tools like Babel.

**The Misconception:**

*   **Synchronous Fetch Assumption:** Developers sometimes mistakenly believe that operations within a functional component, like `fetch` API calls, block rendering and execute synchronously, waiting for completion before proceeding.
*   **Magic Re-rendering:**  There's a false impression that React magically re-runs only the JSX section of a component when state changes, implying a form of dynamic binding.

### 2.2  Functional Components Execute Like Regular JavaScript Functions

It's crucial to understand that React functional components are, at their core, just JavaScript functions. When a component re-renders, React executes the entire function body from top to bottom.

**Illustrative Example: The User List Component Bug**

Consider a `UserList` component designed to fetch and display a list of users from an API:

```javascript
function UserList() {
  const [users, setUsers] = useState([]);

  fetch('/api/users')
    .then(response => response.json())
    .then(data => setUsers(data));

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

**Breakdown of the Bug:**

1.  **Initial Render:**
    *   `useState([])` initializes `users` state as an empty array.
    *   `fetch('/api/users')` initiates an asynchronous API request.
    *   The component immediately renders with an empty list because `fetch` is asynchronous and doesn't block.

2.  **API Response and State Update:**
    *   Eventually, the API request completes, and `setUsers(data)` updates the `users` state with the fetched data.
    *   This state update triggers a re-render of the `UserList` component.

3.  **Second Render - The Infinite Loop:**
    *   The `UserList` function is executed again from the beginning.
    *   `useState([])` is called again, but React preserves the existing `users` state.
    *   Critically, `fetch('/api/users')` is called *again*, initiating a second API request.
    *   This process repeats indefinitely, creating an infinite loop of API calls.

**Why the Infinite Loop Occurs:**

*   **Asynchronous Fetch:** `fetch` is asynchronous and doesn't prevent the component from rendering immediately after being called.
*   **Re-render Triggers Re-fetch:**  Each re-render executes the `fetch` call again, leading to continuous API requests.
*   **State Setter Behavior with Arrays/Objects:**  `setUsers` checks for equality using reference comparison (`===`) for arrays and objects. Even if the *content* of the new array is the same as the old one, if they are different array *references*, it triggers a re-render.

**The Fix: Using `useEffect`**

To correct this, the `fetch` call should be placed within a `useEffect` hook with an empty dependency array (`[]`). This ensures the effect runs only once after the initial render (component mount).

```javascript
function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('/api/users')
      .then(response => response.json())
      .then(data => setUsers(data));
  }, []); // Empty dependency array - runs only once on mount

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

**Revised Mental Model: Hooks and JSX Sections**

Adopting a more accurate mental model is essential:

*   **Hooks Section:** The top part of the functional component where hooks (`useState`, `useEffect`, etc.) are defined. Operations in this section (like fetching data) should generally be wrapped in hooks.
*   **JSX Section:** The `return` statement that generates JSX to be rendered.

**Rule of Thumb:**  Anything outside the `return` statement in a functional component, especially logic involving side effects or state updates, should typically be managed within a hook unless there's a clear and specific reason not to.

## 3. Leverage TypeScript for Robust React Applications

### 3.1 Addressing Common Objections to TypeScript

TypeScript, a superset of JavaScript that adds static typing, is highly recommended for building robust and maintainable React applications. Despite its benefits, some developers express reservations. Let's address common objections:

> **TypeScript:** TypeScript is a statically typed superset of JavaScript that compiles to plain JavaScript. It provides features like static typing, classes, and interfaces, enhancing code maintainability and reducing errors.

**Common Objections and Rebuttals:**

*   **"TypeScript doesn't belong on the client-side."**
    *   **Rebuttal:**  Type safety and code robustness are valuable regardless of the environment (client or server). TypeScript enhances code reliability and maintainability, benefiting client-side React applications significantly.
*   **"TypeScript bloats runtime code."**
    *   **Rebuttal:** TypeScript's type checking occurs during compilation, not at runtime.  Type annotations are removed during compilation, resulting in standard JavaScript output with no runtime performance overhead. TypeScript does *not* inject runtime validation.
*   **"TypeScript makes code ugly."**
    *   **Rebuttal:** Code aesthetics are subjective. While TypeScript adds syntax for type annotations, it enhances code clarity and structure for many developers. The benefits in terms of error prevention and maintainability often outweigh perceived aesthetic concerns.

### 3.2 Key Areas Where TypeScript Enhances React Development

TypeScript's benefits in React development are most pronounced in two key areas:

*   **Defining Data Types:**  TypeScript excels at defining the shapes of data, particularly data received from APIs.
*   **Typing React Components:** TypeScript provides strong typing for React components, ensuring type safety for props and component structure.

### 3.3 Defining Data Types with TypeScript Interfaces

TypeScript interfaces are powerful for defining the structure of data objects, such as API payloads.

**Example: Defining a `Person` Interface**

```typescript
interface Person {
  firstName: string;
  lastName: string;
  age: number;
  address?: string | null; // Optional and possibly null
}

interface PeoplePayload {
  urls: string[];
  pageSize: number;
  people: Person[];
}
```

**Benefits of Type Definitions:**

*   **Early Error Detection:** TypeScript catches type errors during development and build time, preventing runtime issues related to incorrect data structures.
*   **Improved Code Maintainability:** Type definitions serve as documentation, making it easier to understand data structures and maintain code over time.
*   **Null Safety:**  TypeScript's optional and nullable types (e.g., `address?: string | null`) help prevent null reference errors by forcing developers to handle potentially missing or null values explicitly.

### 3.4 Typing React Components with TypeScript

TypeScript enhances React component definitions by providing type safety for props.

**Example: Converting a JavaScript Component to TypeScript**

**JavaScript (with PropTypes - Runtime Check Only):**

```javascript
import PropTypes from 'prop-types';

function MyList({ list, onClick }) {
  return (
    <ul>
      {list.map(person => (
        <li key={person.id} onClick={() => onClick(person)}>{person.name}</li>
      ))}
    </ul>
  );
}

MyList.propTypes = {
  list: PropTypes.arrayOf(PropTypes.object).isRequired,
  onClick: PropTypes.func.isRequired,
};
```

**TypeScript (Build-Time Check and Better Type Inference):**

```typescript
import React, { FC } from 'react';

interface MyListProps {
  list: Person[]; // Using the Person interface defined earlier
  onClick: (person: Person) => void; // Explicitly typed callback
}

const MyList: FC<MyListProps> = ({ list, onClick }) => {
  return (
    <ul>
      {list.map(person => (
        <li key={person.id} onClick={() => onClick(person)}>{person.firstName} {person.lastName}</li>
      ))}
    </ul>
  );
};

export default MyList;
```

**Advantages of TypeScript Component Typing:**

*   **Build-Time Type Checking:** TypeScript performs type checking during compilation, catching prop type errors before runtime, unlike PropTypes which are checked only at runtime.
*   **Improved Developer Experience:** IDEs and code editors can leverage TypeScript type information to provide better autocompletion, hints, and error messages, improving developer productivity.
*   **Precise Callback Typing:** TypeScript allows for detailed typing of callback functions, including the types of arguments they receive, providing better type safety and developer guidance. (`onClick: (person: Person) => void;`)

## 4. Don't Overthink React Re-renders Prematurely

### 4.1 Debunking the "Re-renders are Expensive" Myth

There's a common misconception that React component re-renders are inherently performance-intensive and should be avoided at all costs. This often leads to premature optimization efforts that can complicate code unnecessarily.

**Understanding React's Virtual DOM**

> **Virtual DOM (VDOM):** The Virtual DOM is a lightweight, in-memory representation of the actual DOM. React uses it to efficiently update the user interface by comparing the VDOM with the real DOM and only making necessary changes to the real DOM.

**How React Rendering Works:**

1.  **Component Function Execution:** When a component re-renders, React executes the component function again.
2.  **Virtual DOM Creation:**  The JSX returned by the component is transpiled into `React.createElement` calls, which construct a virtual DOM node.
3.  **Virtual DOM Tree Update:** React builds or updates the virtual DOM tree, which represents the desired state of the UI.
4.  **VDOM Diffing and Reconciliation:** React compares the new virtual DOM tree with the previous one to identify differences (diffing). It then efficiently updates only the necessary parts of the actual DOM to reflect these changes (reconciliation).
5.  **Real DOM Updates (Minimal):** React efficiently updates the real DOM only where changes are detected. If there are no changes between renders, no DOM updates occur.

**Performance Implications:**

*   **Initial Render Cost:** The first render, especially for complex components or large lists, can have a noticeable performance cost (e.g., 100 milliseconds in the example of rendering 500 list items).
*   **Subsequent Re-renders (Often Minimal):** Re-renders where the output is the same as the previous render are typically very fast (sub-millisecond). React's VDOM efficiently detects no changes and avoids unnecessary DOM manipulations.

**Focus on Actual Performance Bottlenecks:**

*   **Infinite Loops in `useEffect`:**  Performance issues are more likely to stem from bugs like infinite loops in `useEffect` hooks due to incorrect dependency arrays, leading to excessive and unnecessary re-renders.
*   **Legitimate Performance Problems:** If genuine performance issues arise, React provides developer tools and profiling capabilities to diagnose and address them effectively.

**Recommendation:**

*   **Don't Prematurely Optimize Re-renders:** Focus on writing correct and maintainable code first. Avoid premature optimization aimed at preventing re-renders unless you have identified a real performance bottleneck through profiling.
*   **Trust the Framework:** React's rendering optimizations are highly efficient. Let React handle re-renders naturally and address performance issues only when they demonstrably impact application performance.

## 5. Learn to Love (or at Least Understand) Dependency Arrays

### 5.1 The Purpose of Dependency Arrays in Hooks

Dependency arrays are crucial for controlling the behavior of hooks like `useEffect`, `useMemo`, and `useCallback`. They specify the dependencies that React uses to determine when to re-run an effect, re-memoize a value, or re-create a callback.

> **Dependency Array:** An array provided as the second argument to `useEffect`, `useMemo`, and `useCallback` hooks. It lists the variables that the hook depends on. React uses this array to determine when to re-run the hook's effect or recompute its value.

**`useEffect` and Dependency Arrays:**

*   **Control Effect Execution:** The dependency array in `useEffect` dictates when the effect function will be executed.
*   **Empty Dependency Array (`[]`):**  The effect runs only once after the initial render (component mount) and once on unmount (cleanup function, if provided).
*   **Dependency Array with Values (`[dep1, dep2]`):** The effect runs after the initial render and whenever any of the values in the dependency array change between renders (using shallow comparison).
*   **Missing Dependency Array (Avoid):** If no dependency array is provided, the effect runs after *every* render, which can often lead to performance issues or infinite loops.

### 5.2 Rule 1: Include All External Values Used in the Effect

The first key rule for dependency arrays is to include all external values that are used within the effect function. "External values" refer to variables that are not defined within the scope of the effect itself.

**Example: Fetching User Data Based on `userId`**

```javascript
function UserProfile({ userId }) {
  const [userData, setUserData] = useState(null);

  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(response => response.json())
      .then(data => setUserData(data));
  }, []); // Incorrect - Missing dependency on userId

  // ... component rendering ...
}
```

**Problem:** The `useEffect` has an empty dependency array `[]`, but it uses `userId` from the component's props (an external value). If `userId` changes, the effect will *not* re-run, and the component will not fetch new user data.

**Corrected `useEffect` with Dependency:**

```javascript
useEffect(() => {
  fetch(`/api/users/${userId}`)
    .then(response => response.json())
    .then(data => setUserData(data));
}, [userId]); // Correct - Dependency on userId
```

**Rule 1 Summary:** If your effect function uses a variable from outside its scope, add that variable to the dependency array.

### 5.3 Rule 2: Check for Side Effects of Adding Dependencies

Adding dependencies to the array can sometimes introduce unexpected side effects, such as infinite loops.

**Example: Potential Infinite Loop**

```javascript
useEffect(() => {
  fetch('/api/users')
    .then(response => response.json())
    .then(data => {
      if (!userData) { // Conditional check to avoid re-fetch if data exists
        setUserData(data);
      }
    });
}, [userData, setUserData]); // Adding setUserData and userData might cause issues
```

**Problem:** Adding `setUserData` to the dependency array is unnecessary and potentially problematic. `setUserData` is a stable function provided by `useState` and will generally not change between renders. However, including `userData` could still lead to issues if the effect logic isn't carefully designed.

**Explanation:** If `setUserData(data)` is called within the effect, it *will* update the `userData` state.  If `userData` is in the dependency array, this state update could potentially trigger the effect to re-run, leading to an infinite loop.

**Solution: Conditional Logic or Stable Values**

*   **Conditional Check:** Add a condition within the effect to prevent re-fetching if the data already exists, as shown in the example.
*   **Stable Values (Use `useCallback` or `useRef` if necessary):** In more complex scenarios, you might need to use `useCallback` to memoize functions or `useRef` to manage values that shouldn't trigger effect re-runs. However, for simple state updates, conditional checks are often sufficient.

**Rule 2 Summary:**  When adding dependencies, carefully consider if they are truly necessary and if they might introduce unintended side effects like infinite loops. Implement conditional logic within the effect if needed.

### 5.4 Rule 3: Embrace the React ESLint Plugin's `exhaustive-deps` Rule

The `eslint-plugin-react-hooks` plugin, included by default in React projects created with Create React App and similar tools, provides excellent linting rules for hooks, including the `exhaustive-deps` rule.

> **ESLint:** ESLint is a popular JavaScript and JSX linting tool used to identify and report on patterns found in ECMAScript/JavaScript code. It helps maintain code quality and consistency.

> **Linting Rule (exhaustive-deps):** The `exhaustive-deps` rule from `eslint-plugin-react-hooks` helps ensure that dependency arrays in hooks (`useEffect`, `useMemo`, `useCallback`) are correctly specified by warning when dependencies are missing or incorrectly included.

**Benefits of `exhaustive-deps` Rule:**

*   **Detects Missing Dependencies:** The rule warns if you've missed adding a dependency to the array that is used within the hook.
*   **Identifies Unnecessary Dependencies:** The rule can also sometimes suggest removing dependencies that are likely stable and don't need to trigger re-runs.
*   **Prevents Common Hook Errors:** By enforcing correct dependency array usage, the rule helps prevent common bugs like stale closures, infinite loops, and unexpected effect behavior.

**Recommendation:**

*   **Enable and Trust the `exhaustive-deps` Rule:** Do *not* disable this rule. It is a valuable tool for catching hook-related errors early in development.
*   **Pay Attention to Linting Warnings:**  When ESLint flags warnings related to dependency arrays, carefully review your hook logic and dependency array to ensure correctness.

### 5.5  Reference Equality vs. Value Equality in Dependency Arrays

It's crucial to understand how React compares values in dependency arrays:

*   **Primitive Values (Numbers, Strings, Booleans):** React uses *value equality* (using `===`) to compare primitive values. If the value is the same between renders, it's considered unchanged.
*   **Objects, Arrays, Functions:** React uses *referential equality* (comparing object/array/function *references*, not their contents). Two objects or arrays are considered different if they are different instances in memory, even if their contents are identical.

**Implications for Dependency Arrays:**

*   **Arrays and Objects as Dependencies:** If you include an array or object directly in a dependency array, the effect, memoized value, or callback will likely re-run on every render because a new array or object reference is created on each render, even if the contents are the same.
*   **Functions as Dependencies:** Similarly, functions defined inline within a component are re-created on each render, leading to re-runs if used as dependencies.

**Avoiding Referential Equality Issues:**

*   **Memoize Functions with `useCallback`:** Use `useCallback` to memoize functions that are used as dependencies or passed as props to child components. This ensures that the function reference remains the same across renders unless its own dependencies change.
*   **Memoize Objects/Arrays with `useMemo`:** Use `useMemo` to memoize objects or arrays that are used as dependencies to maintain referential identity.
*   **Stable References:**  Ensure that arrays, objects, or functions used in dependency arrays have stable references across renders when their underlying data or logic doesn't change. Avoid creating new instances on every render if you want to prevent unnecessary re-runs.

**Avoid Hacks for Deep Comparison:**

Avoid using hacks like `array.join()` or `JSON.stringify()` to attempt deep comparison of arrays or objects in dependency arrays. These are generally not robust and can be less performant than proper memoization techniques.

## 6. Don't Ignore `useCallback` and `useMemo`: Vital for React's Reactive Model

### 6.1 Debunking Misconceptions about `useCallback` and `useMemo` Performance

Contrary to some misleading advice, `useCallback` and `useMemo` are *not* performance bottlenecks in React applications. They are essential tools for managing referential identity and optimizing performance in specific scenarios within React's reactive state management model.

**Purpose of `useCallback` and `useMemo`:**

*   **Referential Identity:** Both hooks are primarily used to maintain the *referential identity* of values (functions for `useCallback`, any value for `useMemo`) across renders. This means ensuring that the hook returns the *same* reference to a value if its dependencies haven't changed.
*   **Performance Optimization (Secondary):** While referential identity is their primary purpose, correctly using these hooks can also lead to performance optimizations by preventing unnecessary re-renders of child components or re-computations of expensive values.

### 6.2 `useMemo`: Memoizing Values

`useMemo` is used to memoize the result of a computation. It takes a function and a dependency array as arguments. It will only re-run the function and recompute the value if any of the dependencies in the array have changed since the last render. Otherwise, it returns the previously memoized value (same reference).

**Two Primary Use Cases for `useMemo`:**

1.  **Memoizing Arrays and Objects (Referential Identity):** When you need to maintain the same reference to an array or object across renders (e.g., for dependency arrays or prop comparison in child components).
2.  **Memoizing Expensive Computations (Performance):** When you have a computationally expensive operation that you want to avoid re-running unnecessarily on every render.

**Examples of `useMemo` Usage:**

*   **Expensive Calculation (Potential Benefit):**

    ```javascript
    const totalCost = useMemo(() => {
      // Potentially expensive calculation based on costs array
      return costs.reduce((sum, cost) => sum + cost, 0);
    }, [costs]);
    ```

    *   **Rationale:**  If `costs` array is large, recalculating the `totalCost` on every render could be inefficient. `useMemo` ensures it's recalculated only when `costs` changes.

*   **Sorting an Array (Referential Identity and Performance):**

    ```javascript
    const sortedPeople = useMemo(() => {
      return [...people].sort((a, b) => a.name.localeCompare(b.name)); // Create new sorted array
    }, [people]);
    ```

    *   **Rationale:**  Sorting can be computationally expensive. `useMemo` avoids re-sorting if `people` array hasn't changed.  Also, `sortedPeople` will have the same array reference across renders if `people` is unchanged, which can be important for dependency arrays or prop comparisons.

*   **Simple String Concatenation (Not Recommended):**

    ```javascript
    const fullName = useMemo(() => {
      return `${firstName} ${lastName}`;
    }, [firstName, lastName]); // Unnecessary use of useMemo
    ```

    *   **Rationale:** String concatenation is a very cheap operation. `useMemo` introduces unnecessary overhead in this case. A simple `const fullName = `${firstName} ${lastName}`;` is sufficient and more efficient.

**`useMemo` Summary:** Use `useMemo` when you need to maintain referential identity for arrays or objects or when you have computationally expensive operations that should be memoized. Avoid overuse for trivial calculations.

### 6.3 `useCallback`: Memoizing Functions

`useCallback` is used to memoize callback functions. It takes a function and a dependency array as arguments. It will return the same function reference across renders as long as its dependencies haven't changed.

**Two Primary Use Cases for `useCallback`:**

1.  **Preventing Stale Callbacks:** In scenarios where a callback function depends on values that might change between renders, `useCallback` ensures that the callback always has access to the latest values when it's eventually executed (especially in asynchronous contexts).
2.  **Maintaining Referential Identity of Callbacks:**  When you need to pass callbacks as props to child components that use `React.memo` or `shouldComponentUpdate` for performance optimization, `useCallback` is essential to prevent unnecessary re-renders of child components.

**Example: `NameList` Component with `useCallback`**

```javascript
import React, { useMemo, useCallback } from 'react';

interface NameListProps {
  names: string[];
  sortFunction: (a: string, b: string) => number;
}

const NameList: React.FC<NameListProps> = React.memo(({ names, sortFunction }) => {
  const sortedNames = useMemo(() => {
    console.log('Sorting names...'); // For demonstration
    return [...names].sort(sortFunction);
  }, [names, sortFunction]); // Memoize based on names and sortFunction

  return (
    <ul>
      {sortedNames.map((name, index) => (
        <li key={index}>{name}</li>
      ))}
    </ul>
  );
});

function ParentComponent() {
  const names = ['Charlie', 'Alice', 'Bob'];

  // Incorrect: Inline function - new reference on each render
  // const sortByName = (a, b) => a.localeCompare(b);

  // Correct: Memoized function - same reference if dependencies don't change
  const sortByName = useCallback((a, b) => a.localeCompare(b), []); // No dependencies - stable sort function

  return (
    <div>
      <NameList names={names} sortFunction={sortByName} />
    </div>
  );
}
```

**Explanation:**

*   **`NameList` Component (Memoized with `React.memo`):** `NameList` is wrapped in `React.memo`, which performs shallow prop comparison to determine if re-rendering is needed.
*   **`useMemo` in `NameList`:** `useMemo` is used to memoize the `sortedNames` array based on `names` and `sortFunction`.
*   **`ParentComponent` - `sortByName` with `useCallback`:**
    *   **Incorrect (Inline Function):** If `sortFunction` were defined inline (`(a, b) => a.localeCompare(b)`), a *new* function reference would be created on every render of `ParentComponent`. This would invalidate the `useMemo` in `NameList` and cause `NameList` to re-render unnecessarily, even if `names` hadn't changed.
    *   **Correct (`useCallback`):** Using `useCallback` with an empty dependency array `[]` creates a *stable* `sortByName` function reference. This ensures that `NameList` only re-renders and re-sorts names when the `names` prop actually changes, not just on every render of `ParentComponent`.

**`useCallback` Summary:** Use `useCallback` to memoize callback functions, especially when passing them as props to memoized child components or when you need to ensure stable function references for dependency arrays.

## 7. Do Create and Utilize Custom Hooks for Reusability

### 7.1 Custom Hooks: Encapsulating Reusable Hook Logic

Custom hooks are a powerful feature in React that allow you to extract and reuse stateful logic across multiple components. They are essentially JavaScript functions that can call other hooks (`useState`, `useEffect`, `useMemo`, etc.) and return values that can be used in components.

> **Custom Hooks:** Custom Hooks are JavaScript functions that start with "use" and can call other Hooks. They allow you to extract component logic into reusable functions, enhancing code organization and reusability. Custom Hooks are a convention, not a built-in React feature.

**Benefits of Custom Hooks:**

*   **Code Reusability:**  Extract common hook logic into custom hooks to avoid code duplication across components.
*   **Improved Code Organization:**  Organize complex component logic into smaller, more manageable custom hooks, making components cleaner and easier to understand.
*   **Testability:** Custom hooks can be tested in isolation, separate from components, improving testability of complex logic.
*   **Abstraction:** Custom hooks can abstract away complex implementation details, providing a simpler API for components to use.

### 7.2 Example: Creating a `useUserList` Custom Hook

Let's revisit the `UserList` component example and refactor the data fetching logic into a custom hook called `useUserList`.

**Original `UserList` Component (with in-component fetching):**

```javascript
function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('/api/users')
      .then(response => response.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

**Creating the `useUserList` Custom Hook:**

```javascript
import { useState, useEffect } from 'react';

function useUserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true); // Optional: Add loading state
  const [error, setError] = useState(null);     // Optional: Add error state

  useEffect(() => {
    setLoading(true); // Optional: Set loading to true before fetch
    fetch('/api/users')
      .then(response => {
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        return response.json();
      })
      .then(data => {
        setUsers(data);
        setLoading(false); // Optional: Set loading to false on success
      })
      .catch(error => {
        setError(error);     // Optional: Set error state on failure
        setLoading(false); // Optional: Set loading to false on error
      });
  }, []);

  return { users, loading, error }; // Return relevant data and states
}
```

**Using the `useUserList` Custom Hook in `UserList` Component:**

```javascript
function UserList() {
  const { users, loading, error } = useUserList();

  if (loading) return <p>Loading users...</p>;
  if (error) return <p>Error loading users: {error.message}</p>;

  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

**Advantages of `useUserList` Custom Hook:**

*   **Reusability:** The `useUserList` hook can be reused in other components that need to fetch and display user lists.
*   **Improved Component Readability:** The `UserList` component becomes much cleaner and focused on rendering the UI, as data fetching logic is moved to the custom hook.
*   **Testability:** `useUserList` can be tested independently to verify its data fetching and state management logic.

**Recommendation:** Identify reusable logic within your components and extract it into custom hooks to improve code organization, reusability, and testability.

## 8. Don't Automatically Default to Redux for State Management

### 8.1 Context and Hooks: Powerful Built-in State Management

In the early days of React, Redux was often considered the de facto standard for state management, especially in larger applications. However, with the introduction of Context API and Hooks in React, built-in state management capabilities have become significantly more powerful and often sufficient for many applications.

> **Redux:** Redux is a popular open-source JavaScript library for managing application state. It provides a predictable state container for JavaScript apps and is often used with React, although it's framework-agnostic.

> **Context API:** React Context provides a way to share values like theme, locale, or user authentication across the component tree without explicitly passing props down through every level. It's a built-in mechanism for global state management in React.

**Evolution of React State Management:**

*   **Early React (Pre-Hooks):** Redux and similar external state management libraries were often necessary for managing complex application state, especially in larger projects.
*   **React with Context API and Hooks:** Context API provides a built-in mechanism for global state, and Hooks (especially `useState` and `useReducer`) offer robust state management within components, reducing the need for external libraries in many cases.

**Modern State Management Strategies:**

1.  **Start with Context and Hooks:** For many applications, especially smaller to medium-sized ones, Context API combined with Hooks (`useState`, `useReducer`, custom hooks) can provide sufficient state management capabilities without the added complexity of external libraries like Redux.
2.  **Consider Query Libraries for Server State:** For managing data fetched from APIs (server state), libraries like React Query or SWR are excellent choices. They provide caching, error handling, background updates, and other features specifically designed for server state management. These libraries often handle a significant portion of state management needs related to API data.
3.  **Form Libraries for Form State:** For managing form state and logic, libraries like Formik or React Hook Form are highly effective. They simplify form handling, validation, and submission, often encompassing form-related state management.
4.  **Redux (or Alternatives) - Consider if Needed:** If Context and Hooks, query libraries, and form libraries are not sufficient for the complexity of your application's state management needs (e.g., very large applications, complex state transformations, time travel debugging), then consider using Redux or other external state management libraries like Recoil, Jotai, or Zustand.

**Redux Toolkit Recommendation:** If you do choose to use Redux, strongly consider using Redux Toolkit.

> **Redux Toolkit:** Redux Toolkit is the official, opinionated, batteries-included toolset for efficient Redux development. It simplifies common Redux tasks and includes best practices to reduce boilerplate and improve developer experience.

**Benefits of Redux Toolkit:**

*   **Simplified Redux Development:** Reduces boilerplate code and simplifies common Redux patterns.
*   **Built-in Query Library (`createApi`):** Redux Toolkit includes `createApi`, a powerful query library similar to React Query, for managing server state within Redux.

**Recommendation:**

*   **Keep it Simple:** Start with the simplest state management solutions that meet your application's needs.
*   **Context and Hooks First:** Evaluate Context API and Hooks as your primary state management approach.
*   **Query Libraries and Form Libraries for Specific Needs:** Utilize query libraries (React Query, SWR, Redux Toolkit Query) for server state and form libraries (Formik, React Hook Form) for form state.
*   **Redux (or Alternatives) as a Last Resort:** Consider Redux or other external state managers only if built-in and specialized solutions are insufficient for your application's complexity.

## 9. Do Utilize Query Libraries for API Interactions

### 9.1  Beyond Basic Data Fetching: The Power of Query Libraries

For applications that interact with APIs, using a dedicated query library like React Query or SWR is highly recommended. These libraries provide a wealth of features beyond basic data fetching and greatly simplify the management of server state.

> **React Query:** React Query is a popular library for fetching, caching, synchronizing, and updating server state in React applications. It provides hooks for data fetching, mutations, and caching, simplifying API interactions.

> **SWR (Stale-While-Revalidate):** SWR is a lightweight React Hooks library for remote data fetching. It follows the "stale-while-revalidate" strategy for data updates, providing a fast and efficient way to manage server data in React applications.

> **RTK Query (Redux Toolkit Query):** RTK Query is a powerful data fetching and caching solution built into Redux Toolkit. It provides similar features to React Query and SWR but is integrated with Redux for state management.

**Limitations of Basic Data Fetching (like the `useUserList` example):**

*   **No Error Handling:**  Basic fetch implementations often lack robust error handling.
*   **No Loading States:**  Managing loading states manually can be cumbersome.
*   **No Caching:**  Data is fetched every time the component renders, even if the data hasn't changed, leading to unnecessary API requests.
*   **No Refetching or Refreshing Mechanisms:**  Implementing features like refetching data on demand or refreshing data at intervals requires manual coding.

**Benefits of Query Libraries (React Query, SWR, RTK Query):**

*   **Simplified Data Fetching:** Provide hooks that streamline data fetching with minimal code.
*   **Automatic Caching:**  Implement intelligent caching mechanisms to reduce redundant API requests and improve performance.
*   **Background Updates:**  Support background data updates to keep data fresh and synchronized.
*   **Error Handling:**  Provide robust error handling capabilities.
*   **Loading States:**  Manage loading states automatically, simplifying UI updates.
*   **Refetching and Refreshing:**  Offer built-in methods for refetching data on demand or refreshing at intervals.
*   **Mutations (Data Updates):**  Provide hooks for performing data mutations (POST, PUT, DELETE requests) and updating caches accordingly.

### 9.2 Example: Migrating `useUserList` to React Query's `useQuery`

Let's refactor the `useUserList` custom hook to use React Query's `useQuery` hook to demonstrate the simplicity and power of query libraries.

**Original `useUserList` (Custom Hook with `useState` and `useEffect`):**

```javascript
// ... (useUserList code from section 7.2) ...
```

**Refactored `useUserList` using React Query's `useQuery`:**

```javascript
import { useQuery } from 'react-query';

function useUserList() {
  const { data, isLoading, error, refetch } = useQuery(
    'users', // Query key (cache key)
    () => fetch('/api/users').then(res => res.json()) // Fetch function
  );

  return { users: data, loading: isLoading, error, refetch };
}
```

**Explanation of `useQuery` Usage:**

*   **`useQuery('users', ...)`:**  Calls the `useQuery` hook from React Query.
    *   **`'users'` (Query Key):**  A unique key for this query, used for caching and identifying the query in React Query's cache.
    *   **`() => fetch('/api/users').then(res => res.json())` (Fetch Function):**  A function that performs the API request and returns a promise that resolves to the data.
*   **Return Values from `useQuery`:**
    *   **`data`:** The fetched data (users array in this case).
    *   **`isLoading`:** A boolean indicating if the query is currently loading.
    *   **`error`:**  An error object if the query failed.
    *   **`refetch`:** A function to manually refetch the data.

**Benefits of React Query's `useQuery`:**

*   **Concise Data Fetching:**  Significantly reduces the code required for data fetching compared to manual `useState` and `useEffect` implementations.
*   **Automatic Caching and State Management:** React Query handles caching, loading states, and error states automatically.
*   **Built-in Features:** Provides access to a wide range of features like background updates, refetching, refreshing, and more.

**Recommendation:** If your React application interacts with APIs, use a query library like React Query, SWR, or RTK Query to simplify server state management and leverage their powerful features for data fetching, caching, and updates. Avoid rolling your own data fetching and caching solutions, as these libraries offer robust and well-tested implementations.

## 10. Don't Build Your Own UI Library: Leverage Existing React UI Frameworks

### 10.1 The Value of Pre-built UI Libraries in React

Building a custom UI library from scratch for a React project is generally not recommended. Numerous excellent React UI libraries exist that provide a wide range of components, styling, and features, saving development time and effort and ensuring best practices in UI development.

> **UI Library (User Interface Library):** A collection of pre-built, reusable components and styles that developers can use to create user interfaces for web applications. UI libraries provide ready-made elements like buttons, forms, navigation bars, and more, along with consistent styling and often accessibility features.

**Popular React UI Libraries:**

*   **Material UI (MUI):** A comprehensive UI library implementing Google's Material Design.
*   **Ant Design (AntD):** A popular UI library, especially in enterprise applications, with a rich set of components.
*   **React Bootstrap:**  A React implementation of the popular Bootstrap CSS framework.
*   **Chakra UI:** A simple, modular, and accessible UI library that emphasizes ease of use and customization.
*   **Mantine:** A full-featured UI library with a focus on developer experience and a wide range of components and hooks.

**Advantages of Using Pre-built UI Libraries:**

*   **Reduced Development Time:**  Significantly speeds up UI development by providing ready-to-use components, eliminating the need to build components from scratch.
*   **Consistent UI and Styling:**  Ensure a consistent look and feel across your application with pre-defined themes and styles.
*   **Accessibility (A11y):**  Reputable UI libraries are designed with accessibility best practices in mind, helping you create more inclusive applications.
*   **Internationalization (i18n):** Many UI libraries offer internationalization support, making it easier to adapt your application for different languages and regions.
*   **Theming and Customization:**  Provide theming capabilities to customize the look and feel of components to match your brand or design requirements.
*   **Community Support and Documentation:**  Benefit from active communities, extensive documentation, and examples, making it easier to learn and use the libraries.
*   **Design System Integration:**  Some libraries, like Material UI, offer Figma templates that align with their component sets. This facilitates better communication and collaboration between designers and developers by using standardized components and design specifications.

**Benefits of Figma Templates (Example: Material UI):**

*   **Designer-Developer Collaboration:** Figma templates for UI libraries allow designers to work directly with library components in their design tools.
*   **Component-Based Design:** Designers can drag and drop components from the UI library into their mockups, ensuring consistency with available UI elements.
*   **Theming in Design Tools:** Designers can apply themes within Figma that correspond to the UI library's theming system, ensuring design consistency with the final application.
*   **Precise Design Specifications:**  Designers can provide developers with mockups that use actual UI library components, along with specific prop configurations, making the handoff process more accurate and efficient.

**Recommendation:**

*   **Choose a Suitable UI Library:**  Select a React UI library that aligns with your project's design requirements, complexity, and team's familiarity. Consider factors like component set, styling approach, accessibility, and community support.
*   **Leverage Library Components:**  Utilize the components provided by the chosen UI library extensively. Avoid re-implementing components that are already available in the library.
*   **Customize and Theme:**  Take advantage of the library's theming and customization options to adapt the UI to your application's specific brand and design guidelines.
*   **Avoid Building Custom UI Libraries:**  Unless you have very specific and compelling reasons (e.g., highly unique UI requirements, performance constraints that cannot be met by existing libraries), avoid building your own UI library from scratch. It's generally more efficient and beneficial to leverage the maturity, features, and community support of existing React UI frameworks.

By following these do's and don'ts, you can significantly improve your React development practices, build more robust and maintainable applications, and leverage the power of the React ecosystem effectively.
