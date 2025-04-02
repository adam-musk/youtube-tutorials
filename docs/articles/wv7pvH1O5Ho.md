---
layout: "../../layouts/BlogPost.astro"
title: "Building a Sortable List with Drag and Drop using Vanilla JavaScript: An Educational Guide"
pubDate: "2025-03-08 16:00:39.848220"
youtubeVideoID: "wv7pvH1O5Ho"
---

# Building a Sortable List with Drag and Drop using Vanilla JavaScript: An Educational Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/wv7pvH1O5Ho" frameborder="0" allowfullscreen></iframe>

This chapter will guide you through the process of creating a dynamic, sortable list using vanilla JavaScript, enhanced with drag and drop functionality.  This project, originally from a web development course, serves as an excellent practical exercise for understanding core JavaScript concepts, DOM manipulation, and the browser's Drag and Drop API.  We will break down each step, from setting up the HTML structure to implementing the JavaScript logic and styling with CSS.

## 1. Introduction to Sortable Lists and Drag and Drop

Interactive web applications often require users to manipulate data visually. Sortable lists are a common UI pattern that allows users to reorder items within a list intuitively.  Combined with drag and drop functionality, this becomes a powerful tool for creating engaging and user-friendly interfaces.

This chapter focuses on building a sortable list of the "Top 10 Richest People" as a practical example. However, the principles and code structure can be easily adapted to any list of items you wish to make sortable. The primary focus will be on leveraging the browser's built-in **Drag and Drop API** to enable this interactivity.

> The **Drag and Drop API** is a set of interfaces that allows web applications to enable drag-and-drop features using native browser events. It provides a standardized way to handle drag-and-drop interactions within web pages.

We will also explore various JavaScript methods and concepts including:

*   **DOM Manipulation:**  Dynamically creating and modifying HTML elements using JavaScript.
*   **Array Methods:**  `forEach`, `map`, `sort`, and the **spread operator** for efficient data handling.
*   **Event Handling:**  Listening for and responding to user interactions like drag and drop events.
*   **CSS Styling:**  Applying styles to enhance the visual presentation of the list.

Let's begin by setting up the basic HTML structure.

## 2. Setting Up the HTML Structure

For this project, we will start with a minimal HTML file.  The list items themselves will be generated dynamically using JavaScript. This approach highlights the power of JavaScript in manipulating the **Document Object Model (DOM)**.

> The **Document Object Model (DOM)** is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as nodes and objects; that way, programming languages can interact with the page.

Here's the basic HTML structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Top 10 Richest People</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://kit.fontawesome.com/[YOUR_FONT_AWESOME_KIT].js" crossorigin="anonymous"></script>
</head>
<body>
    <h1>10 Richest People</h1>
    <p>Drag and drop the items into their corresponding spots</p>
    <ul class="draggable-list" id="draggable-list">
        <!-- List items will be inserted here by JavaScript -->
    </ul>
    <button class="check-btn" id="check">
        Check Order <i class="fas fa-paper-plane"></i>
    </button>
    <script src="script.js"></script>
</body>
</html>
```

**Key elements in the HTML:**

*   **Font Awesome:**  We are including Font Awesome for icons, specifically the "grip lines" icon for drag handles and the "paper plane" icon for the "Check Order" button. You will need to replace `[YOUR_FONT_AWESOME_KIT].js` with your own Font Awesome kit script.
*   **`<h1>`:**  The main title of the page.
*   **`<p>`:**  A descriptive paragraph instructing the user.
*   **`<ul>`:**  An unordered list with the class `draggable-list` and ID `draggable-list`. This `ul` element will serve as the container for our sortable list items.  Crucially, it is initially empty; list items will be dynamically added via JavaScript.
*   **`<button>`:** A button with the class `check-btn` and ID `check`. This button will be used to trigger the order checking functionality.
*   **`style.css` and `script.js`:** Links to external CSS and JavaScript files, respectively.

## 3. JavaScript: Setting up DOM Elements and Data

Now, let's move to the `script.js` file and start implementing the JavaScript logic. First, we need to select the relevant DOM elements and define our data.

```javascript
const draggableList = document.getElementById('draggable-list');
const checkBtn = document.getElementById('check');

const richestPeople = [
    'Jeff Bezos',
    'Bill Gates',
    'Warren Buffett',
    'Bernard Arnault',
    'Carlos Slim Helu',
    'Amancio Ortega',
    'Larry Ellison',
    'Mark Zuckerberg',
    'Michael Bloomberg',
    'Larry Page'
];

const listItems = [];

let dragStartIndex;

createList();

// ... (rest of JavaScript code will be added in subsequent sections)
```

**Explanation:**

*   **`draggableList` and `checkBtn`:** We use `document.getElementById` to select the `ul` element (`draggable-list`) and the button element (`check`) from the HTML. These variables will allow us to manipulate these elements in our JavaScript code.
*   **`richestPeople` Array:**  This array holds the names of the top 10 richest people in the correct order. This array serves as our source data and the basis for comparison when checking the order.
*   **`listItems` Array:**  This array is initialized as empty. It will store the dynamically created list items as they are generated and potentially reordered.
*   **`dragStartIndex` Variable:**  This variable will be used to keep track of the index of the list item that is being dragged. It is initialized with `let` because its value will change during the drag and drop process.
*   **`createList()` Function Call:**  This line calls the `createList` function, which we will define next, to generate and insert the list items into the DOM.

## 4. JavaScript: Creating and Inserting List Items into the DOM

The `createList` function is responsible for dynamically generating the list items based on the `richestPeople` array and inserting them into the `draggableList` (the `ul` element in our HTML).

```javascript
function createList() {
    [...richestPeople] // Using spread operator to create a copy
        .map(a => ({ value: a, sort: Math.random() })) // Map to objects with value and random sort value
        .sort((a, b) => a.sort - b.sort) // Sort based on random value
        .map(a => a.value) // Map back to array of names
        .forEach((person, index) => {
            const listItem = document.createElement('li');
            listItem.setAttribute('data-index', index);

            listItem.innerHTML = `
                <span class="number">${index + 1}</span>
                <div class="draggable" draggable="true">
                    <p class="person-name">${person}</p>
                    <i class="fas fa-grip-lines"></i>
                </div>
            `;

            listItems.push(listItem);
            draggableList.appendChild(listItem);
        });

    addEventListeners(); // Call function to attach event listeners
}
```

**Detailed Explanation of `createList` Function:**

1.  **Scrambling the List Order:**
    *   **`[...richestPeople]` (Spread Operator):**
        > The **spread operator** (`...`) allows an iterable such as an array or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected.  Here, it creates a shallow copy of the `richestPeople` array, preventing modification of the original ordered array.
    *   **.`map(a => ({ value: a, sort: Math.random() }))`:** The `map` method iterates over the copied array and transforms each element (person's name) into an object. Each object has two properties:
        *   `value`:  The person's name.
        *   `sort`: A random decimal number generated using `Math.random()`.
        > The **`map()` method** is a higher-order array method that creates a new array by calling a provided function on every element in the calling array.
    *   **.`sort((a, b) => a.sort - b.sort)`:** The `sort` method shuffles the array of objects based on the `sort` property (the random numbers). This effectively randomizes the order of the names.
        > The **`sort()` method** is a higher-order array method that sorts the elements of an array *in place* and returns the sorted array. It can take a compare function to customize the sort order.
    *   **.`map(a => a.value)`:**  Another `map` method is used to transform the array of objects back into an array of just the person names, but now in a scrambled order.

2.  **Generating List Item Elements:**
    *   **.`forEach((person, index) => { ... })`:** The `forEach` method iterates over the scrambled array of person names.
        > The **`forEach()` method** is a higher-order array method that executes a provided function once for each array element.
    *   **`const listItem = document.createElement('li');`:**  For each person, a new `li` (list item) element is created using `document.createElement('li')`. This is a core **DOM manipulation** technique.
        > **`document.createElement()`** is a DOM method that creates an HTML element specified by `tagName`.
    *   **`listItem.setAttribute('data-index', index);`:** A custom `data-index` attribute is added to each `li` element. This attribute stores the original index of the item in the `richestPeople` array (before scrambling). This is crucial for tracking the correct order and for drag and drop functionality. **Data attributes** are used to store custom data private to the page or application.
    *   **`listItem.innerHTML = \`...\`;` (Template Literals):**  The `innerHTML` property is used to set the HTML content within each `li` element.
        > **`innerHTML`** is a property that gets or sets the HTML markup contained within an element.
        **Template literals** (backticks `` ` ``) are used to create multi-line strings and embed expressions (`\${expression}`) within strings, making string construction more readable and powerful.
        The HTML structure within each `li` includes:
        *   `<span class="number">`: Displays the item number (index + 1).
        *   `<div class="draggable" draggable="true">`:  The draggable area. The `draggable="true"` attribute is essential for enabling drag and drop functionality on this element using the Drag and Drop API.
        *   `<p class="person-name">`:  Displays the person's name.
        *   `<i class="fas fa-grip-lines">`: The Font Awesome icon to visually indicate draggable handle.

3.  **Adding List Items to the DOM and `listItems` Array:**
    *   **`listItems.push(listItem);`:** The newly created `listItem` element is added to the `listItems` array. This array now holds references to all the `li` elements in the order they are currently displayed (scrambled initially).
    *   **`draggableList.appendChild(listItem);`:** The `listItem` element is appended as a child to the `draggableList` (`ul` element) in the DOM. This makes the list item visible on the webpage.
        > **`appendChild()`** is a DOM method that adds a node to the end of the list of children of a specified parent node.

4.  **`addEventListeners();`:**  Finally, the `createList` function calls the `addEventListeners` function (which we will define in the next section) to attach event listeners for drag and drop interactions to the generated list items.

## 5. JavaScript: Implementing Drag and Drop Event Listeners

To enable drag and drop functionality, we need to attach event listeners to the draggable elements and list items.  The `addEventListeners` function handles this.

```javascript
function addEventListeners() {
    const draggables = document.querySelectorAll('.draggable');
    const dragListItems = document.querySelectorAll('.draggable-list li');

    draggables.forEach(draggable => {
        draggable.addEventListener('dragstart', dragStart);
    });

    dragListItems.forEach(item => {
        item.addEventListener('dragover', dragOver);
        item.addEventListener('drop', dragDrop);
        item.addEventListener('dragenter', dragEnter);
        item.addEventListener('dragleave', dragLeave);
    });
}
```

**Explanation of `addEventListeners` Function:**

*   **`const draggables = document.querySelectorAll('.draggable');`:**  Selects all elements with the class `draggable` (the `div` elements within each list item).  `querySelectorAll` returns a **NodeList** (similar to an array) of all matching elements.
    > **`document.querySelectorAll()`** is a DOM method that returns a static (not live) NodeList representing a list of the document's elements that match the specified group of selectors.
*   **`const dragListItems = document.querySelectorAll('.draggable-list li');`:** Selects all `li` elements that are descendants of the element with the class `draggable-list` (our `ul` element).
*   **Event Listeners for Draggable Elements (`draggables`):**
    *   **`draggables.forEach(draggable => { ... });`:** Iterates over each `draggable` element.
    *   **`draggable.addEventListener('dragstart', dragStart);`:**  Attaches a `dragstart` event listener to each `draggable` element. When a drag operation begins on a `draggable` element, the `dragStart` function will be executed.
        > **`addEventListener()`** is a DOM method that attaches an event handler to the specified element.
        > The **`dragstart` event** is fired when the user starts to drag an element.
*   **Event Listeners for List Item Elements (`dragListItems`):**
    *   **`dragListItems.forEach(item => { ... });`:** Iterates over each list item (`li` element).
    *   **`item.addEventListener('dragover', dragOver);`:** Attaches a `dragover` event listener. This event is fired continuously as the mouse pointer is over an element during a drag operation.  We will use `e.preventDefault()` in the `dragOver` function to allow dropping on the list items.
        > The **`dragover` event** is fired when an element or text selection is being dragged over a valid drop target (every few hundred milliseconds).
    *   **`item.addEventListener('drop', dragDrop);`:** Attaches a `drop` event listener. This event is fired when a dragged element or text selection is dropped on a valid drop target.
        > The **`drop` event** is fired when the user releases the mouse button or touch screen at a drop target.
    *   **`item.addEventListener('dragenter', dragEnter);`:** Attaches a `dragenter` event listener. This event is fired when the mouse pointer enters an element during a drag operation. We will use this to visually highlight the target list item.
        > The **`dragenter` event** is fired when a dragged element or text selection enters a valid drop target.
    *   **`item.addEventListener('dragleave', dragLeave);`:** Attaches a `dragleave` event listener. This event is fired when the mouse pointer leaves an element during a drag operation. We will use this to remove the visual highlight from the target list item.
        > The **`dragleave` event** is fired when a dragged element or text selection leaves a valid drop target.

## 6. JavaScript: Implementing Drag Event Handlers

Now, we need to define the functions that will be executed when the drag and drop events are triggered. These functions will handle the logic for visual feedback and reordering the list items.

```javascript
let dragStartIndex;

function dragStart(e) {
    dragStartIndex = +this.closest('li').getAttribute('data-index');
}

function dragOver(e) {
    e.preventDefault(); // Necessary to allow dropping
}

function dragDrop(e) {
    const dragEndIndex = +this.getAttribute('data-index');
    swapItems(dragStartIndex, dragEndIndex);
    this.classList.remove('over'); // Remove highlight after drop
}

function dragEnter(e) {
    this.classList.add('over'); // Add highlight when entering
}

function dragLeave(e) {
    this.classList.remove('over'); // Remove highlight when leaving
}

function swapItems(fromIndex, toIndex) {
    const itemOne = listItems[fromIndex].querySelector('.draggable');
    const itemTwo = listItems[toIndex].querySelector('.draggable');

    listItems[fromIndex].appendChild(itemTwo);
    listItems[toIndex].appendChild(itemOne);
}
```

**Explanation of Drag Event Handler Functions:**

*   **`dragStart(e)`:**
    *   **`dragStartIndex = +this.closest('li').getAttribute('data-index');`:**  When a drag operation starts, this function determines the index of the dragged list item.
        *   **`this`:** Inside the event handler, `this` refers to the `draggable` element that triggered the `dragstart` event.
        *   **`.closest('li')`:**  The `closest('li')` method traverses up the DOM tree from the `draggable` element until it finds the closest ancestor `li` element (the list item).
            > **`closest()`** is a DOM method that traverses the Element and its parents (heading toward the document root) until it finds a node that matches the specified CSS selector.
        *   **`.getAttribute('data-index')`:**  Retrieves the value of the `data-index` attribute from the found `li` element.
            > **`getAttribute()`** is a DOM method that returns the string value of a named attribute on the current element.
        *   **`+` (Unary Plus Operator):**  Converts the attribute value (which is a string) to a number. This numerical index is then stored in the `dragStartIndex` variable.

*   **`dragOver(e)`:**
    *   **`e.preventDefault();`:**  This line is crucial. By default, data/elements cannot be dropped onto other elements. Calling `e.preventDefault()` in the `dragover` handler prevents the default behavior and allows the `drop` event to be fired when an element is dropped onto a valid drop target.
        > **`e.preventDefault()`** is a method on the **event object** (`e`). It prevents the default action of the event from happening. In the context of drag and drop, it's necessary to prevent the browser's default drag-and-drop behavior and allow JavaScript to handle the drop.

*   **`dragDrop(e)`:**
    *   **`const dragEndIndex = +this.getAttribute('data-index');`:**  When an element is dropped onto a list item, this function gets the `data-index` of the list item where the element was dropped.
    *   **`swapItems(dragStartIndex, dragEndIndex);`:** Calls the `swapItems` function (defined below) to reorder the list items in the DOM based on the `dragStartIndex` and `dragEndIndex`.
    *   **`this.classList.remove('over');`:** Removes the `over` class from the list item where the element was dropped, removing the visual highlight.

*   **`dragEnter(e)`:**
    *   **`this.classList.add('over');`:** When a dragged element enters a list item, this function adds the `over` class to the list item, triggering a visual highlight (defined in CSS) to indicate that this is a potential drop target.
        > **`classList.add()`** is a DOM method that adds one or more classes to the element's class list.
*   **`dragLeave(e)`:**
    *   **`this.classList.remove('over');`:** When a dragged element leaves a list item, this function removes the `over` class, removing the visual highlight.
        > **`classList.remove()`** is a DOM method that removes one or more classes from the element's class list.

*   **`swapItems(fromIndex, toIndex)`:**
    *   **`const itemOne = listItems[fromIndex].querySelector('.draggable');`:** Selects the `draggable` element within the list item at the `fromIndex` (the item being dragged).
        > **`querySelector()`** is a DOM method that returns the first element within the element that matches a specified CSS selector.
    *   **`const itemTwo = listItems[toIndex].querySelector('.draggable');`:** Selects the `draggable` element within the list item at the `toIndex` (the drop target).
    *   **`listItems[fromIndex].appendChild(itemTwo);`:** Appends `itemTwo` (the draggable element of the target list item) to `listItems[fromIndex]` (the original list item's container). This effectively moves `itemTwo` to the position of `itemOne`.
    *   **`listItems[toIndex].appendChild(itemOne);`:** Appends `itemOne` (the draggable element of the dragged list item) to `listItems[toIndex]` (the target list item's container). This completes the swap, moving `itemOne` to the position of `itemTwo`.

## 7. JavaScript: Checking the Order

Finally, we implement the `checkOrder` function, which is triggered when the "Check Order" button is clicked. This function compares the current order of the list items with the original correct order (`richestPeople` array) and visually indicates correct and incorrect positions.

```javascript
checkBtn.addEventListener('click', checkOrder);

function checkOrder() {
    listItems.forEach((listItem, index) => {
        const personName = listItem.querySelector('.draggable').innerText.trim();
        const correctName = richestPeople[index];

        if (personName !== correctName) {
            listItem.classList.add('wrong');
            listItem.classList.remove('right');
        } else {
            listItem.classList.remove('wrong');
            listItem.classList.add('right');
        }
    });
}
```

**Explanation of `checkOrder` Function:**

*   **`checkBtn.addEventListener('click', checkOrder);`:**  Attaches a `click` event listener to the `checkBtn` (the "Check Order" button). When the button is clicked, the `checkOrder` function is executed.
*   **`listItems.forEach((listItem, index) => { ... });`:** Iterates over the `listItems` array (which reflects the current order of list items in the DOM).
*   **`const personName = listItem.querySelector('.draggable').innerText.trim();`:**  For each list item, it gets the text content of the `.draggable` element (which contains the person's name) using `innerText` and removes any leading/trailing whitespace using `trim()`.
        > **`innerText`** is a property that gets or sets the text content of an element and its descendants.
        > **`trim()`** is a string method that removes whitespace from both ends of a string.
*   **`const correctName = richestPeople[index];`:** Gets the correct person's name from the `richestPeople` array at the corresponding `index`.
*   **`if (personName !== correctName) { ... } else { ... }`:**  Compares the `personName` from the current list item with the `correctName` from the `richestPeople` array.
    *   **`if (personName !== correctName)`:** If the names do not match (incorrect position):
        *   `listItem.classList.add('wrong');`: Adds the `wrong` class to the list item (to style it red, indicating an incorrect position).
        *   `listItem.classList.remove('right');`: Removes the `right` class if it was previously added.
    *   **`else { ... }`:** If the names match (correct position):
        *   `listItem.classList.remove('wrong');`: Removes the `wrong` class if it was previously added.
        *   `listItem.classList.add('right');`: Adds the `right` class to the list item (to style it green, indicating a correct position).

## 8. CSS Styling (`style.css`)

To visually enhance the sortable list and provide feedback to the user, we use CSS.  Here's a basic CSS stylesheet (`style.css`) to complement the JavaScript functionality:

```css
@import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');

:root {
    --border-color: #e3e5e4;
    --background-color: #c3c7ca;
    --text-color: #34444f;
}

* {
    box-sizing: border-box;
}

body {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    font-family: 'Lato', sans-serif;
    margin: 0;
    height: 100vh;
}

.draggable-list {
    border: 1px solid var(--border-color);
    padding: 0;
    list-style-type: none;
}

.draggable-list li {
    background-color: #fff;
    display: flex;
    flex: 1;
}

.draggable-list li:not(:last-of-type) {
    border-bottom: 1px solid var(--border-color);
}

.draggable-list .number {
    background-color: var(--background-color);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 28px;
    height: 60px;
    width: 60px;
}

.draggable {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 15px;
    flex: 1;
}

.draggable p {
    margin: 0;
}

.draggable i {
    margin-left: 10px;
    cursor: grab;
}

.draggable.over {
    background-color: #eaeaea;
}

.draggable-list li.right .person-name {
    color: #3ae374; /* Green */
}

.draggable-list li.wrong .person-name {
    color: #ff3838; /* Red */
}

.check-btn {
    background-color: var(--background-color);
    border: none;
    color: var(--text-color);
    font-size: 16px;
    padding: 10px 20px;
    cursor: pointer;
}

.check-btn:active {
    transform: scale(0.98);
}

.check-btn:focus {
    outline: none;
}
```

**CSS Highlights:**

*   **CSS Variables (`:root`):**  Custom CSS properties (variables) are defined in the `:root` pseudo-class for reusable colors.
    > **CSS Variables (Custom Properties)** are entities defined by CSS authors that contain specific values to be reused throughout a stylesheet. They are defined using `--` followed by the variable name.
*   **Basic Styling:**  Sets up basic body styling, centers content, and applies the Lato font from Google Fonts.
*   **`draggable-list` Styles:** Styles the `ul` container with a border and removes default list styling.
*   **`draggable-list li` Styles:** Styles the list items for layout and borders.
*   **`.number` Styles:** Styles the number span to appear as a square box on the left.
*   **`.draggable` Styles:** Styles the draggable area, sets the cursor to pointer, and uses `space-between` for content distribution.
*   **`.draggable i` Styles:** Styles the drag handle icon.
*   **`.draggable.over` Styles:**  Provides visual feedback by changing the background color when a draggable element is dragged over a list item.
*   **`.draggable-list li.right .person-name` and `.draggable-list li.wrong .person-name` Styles:** Styles the person's name to green for correct positions and red for incorrect positions, based on the `right` and `wrong` classes added by JavaScript.
*   **`.check-btn` Styles:** Styles the "Check Order" button.

## 9. Conclusion

This chapter has provided a comprehensive guide to building a sortable list with drag and drop functionality using vanilla JavaScript. By following these steps, you can create interactive lists that allow users to reorder items intuitively.  This project demonstrates the power of JavaScript for DOM manipulation, event handling, and leveraging browser APIs like the Drag and Drop API.

**Key Takeaways:**

*   **Vanilla JavaScript Implementation:**  You learned how to implement drag and drop without relying on external libraries, using only core JavaScript features.
*   **Drag and Drop API:** You gained practical experience using the Drag and Drop API and its key events (`dragstart`, `dragover`, `drop`, `dragenter`, `dragleave`).
*   **DOM Manipulation:** You practiced dynamic DOM manipulation techniques, including creating elements, setting attributes, and modifying element content.
*   **Array Methods:** You utilized various JavaScript array methods (`map`, `sort`, `forEach`, spread operator) for efficient data processing and manipulation.
*   **Event Handling:** You learned how to attach and handle events to make web pages interactive.
*   **CSS Styling for Interactivity:** You applied CSS to enhance the visual appearance and provide user feedback during drag and drop operations.

This project serves as a solid foundation for building more complex interactive web applications. You can adapt and extend this code to create sortable lists for various purposes, enhancing user experience and application functionality. Remember to experiment with different data, styling, and functionalities to deepen your understanding and explore the full potential of vanilla JavaScript and the Drag and Drop API.
