---
layout: "../../layouts/BlogPost.astro"
title: "Building a Product Filtering UI with Vanilla JavaScript and Tailwind CSS: An Educational Guide"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "Hwyyk1Ueoig"
channel: ""
index: 8
---

# Building a Product Filtering UI with Vanilla JavaScript and Tailwind CSS: An Educational Guide

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/Hwyyk1Ueoig" frameborder="0" allowfullscreen></iframe>


This chapter provides a step-by-step guide to building a dynamic product filtering user interface (UI) using vanilla JavaScript and Tailwind CSS. This project is excellent for beginner to intermediate web developers looking to enhance their JavaScript skills and explore the utility-first CSS framework, Tailwind CSS. We will cover building the layout with Tailwind CSS, implementing "Add to Cart" functionality, category filtering, and product search.

## Project Overview

This project focuses on creating an interactive product display with the following features:

*   **Product Display:**  Visually appealing product cards displaying images, names, and prices.
*   **Add/Remove from Cart:**  Functionality to add products to a virtual cart, indicated by a dynamic cart count.
*   **Category Filtering:**  Allow users to filter products based on predefined categories (e.g., cameras, smartphones, games, televisions).
*   **Product Search:**  Enable users to search for products by name.
*   **Combined Filtering and Search:**  When categories are selected, the search functionality will only apply to the products within the chosen categories.
*   **Responsive Design:**  The UI will adapt to different screen sizes, ensuring optimal viewing on desktops and mobile devices.

This project is designed to improve your understanding of:

*   **Vanilla JavaScript:**  Working with core JavaScript without relying on external libraries or frameworks for DOM manipulation and event handling.
*   **Tailwind CSS:**  Utilizing a utility-first CSS framework to rapidly style web elements with pre-defined classes.
*   **DOM Manipulation:**  Dynamically creating, modifying, and updating HTML elements using JavaScript.
*   **Event Handling:**  Responding to user interactions such as clicks and input changes.
*   **Array Methods:**  Employing higher-order array methods like `forEach`, `filter`, and `map` for data manipulation and filtering.

## Setting Up the Development Environment

To begin, you will need a basic development environment. This includes:

*   **Text Editor:** A code editor like VS Code, Sublime Text, or Atom. VS Code is recommended and will be used in this guide.
*   **Web Browser:** A modern web browser such as Chrome, Firefox, or Safari to view your project.
*   **Live Server (Optional but Recommended):** A local development server that automatically refreshes your browser when you save changes to your code.  VS Code has a Live Server extension that is easy to install and use.

### Project Structure

Create a new project folder named `product-filtering-ui`. Inside this folder, create the following files and folders:

*   `index.html`:  The main HTML file to structure the UI.
*   `script.js`:  The JavaScript file for adding interactivity.
*   `images/`: A folder to store product images. You can obtain these images from the provided resources or use your own.

## HTML Structure with Tailwind CSS

We will begin by structuring the HTML for our product filtering UI and styling it using Tailwind CSS.

### Including Tailwind CSS

Tailwind CSS is included in this project using its Play CDN (Content Delivery Network). This is a quick way to get started with Tailwind without needing a complex build process. Add the following script tag within the `<head>` section of your `index.html` file:

```html
<head>
    <title>Text Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
```

> **CDN (Content Delivery Network)**
> A CDN is a geographically distributed network of servers that caches static content like CSS, JavaScript, and images. Using a CDN allows users to load content faster as it is served from a server closer to their location.

### Basic HTML Boilerplate and Body Styling

Start with a basic HTML boilerplate in `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="script.js" defer></script>
</head>
<body class="bg-gray-800 text-white">
    <h1>Hello</h1>
</body>
</html>
```

Here, we've styled the `<body>` element using Tailwind CSS classes:

*   `bg-gray-800`: Sets the background color to a dark gray (Tailwind's gray-800 shade).
*   `text-white`: Sets the default text color to white.

### Navigation Bar (Nav)

The navigation bar will contain a search input and a cart icon.

```html
<nav class="bg-gray-900 p-4 mb-6">
    <div class="container max-w-6xl mx-auto flex flex-col gap-8 items-center sm:flex-row">
        <div class="relative w-full">
            <input type="text" id="search" class="bg-gray-700 rounded-full p-2 pl-10 focus:w-full" placeholder="Search products">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5 absolute left-2 top-1/2 transform -translate-y-1/2 text-gray-400">
                <!-- SVG Path for Search Icon -->
                <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
            </svg>
        </div>
        <div class="relative text-center">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <!-- SVG Path for Cart Icon -->
                <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3 3 3 0 106 0 3 3 0 00-3-3zM15.75 14.25a3 3 0 00-3 3 3 3 0 106 0 3 3 0 00-3-3zM2.25 3l.5-2c.087-.35-.291-.8-.675-.8H2.25zm6.5 4.25l7.75-3.333.262.975-7.75 3.333-.262-.975z" />
            </svg>
            <small id="cart-count" class="bg-red-500 rounded-full text-xs text-white absolute -top-2 -right-2 w-4 h-4 flex items-center justify-center">0</small>
        </div>
    </div>
</nav>
```

**Tailwind CSS Classes Explained:**

*   `bg-gray-900`: Navigation bar background color (darker gray).
*   `p-4`: Padding on all sides (Tailwind's padding scale, 4 units).
*   `mb-6`: Margin bottom (Tailwind's margin scale, 6 units).
*   `container`: Centers content and sets maximum width.
*   `max-w-6xl`: Maximum width of the container (Tailwind's maximum width scale, 6xl).
*   `mx-auto`: Centers the container horizontally by setting left and right margins to auto.
*   `flex`: Enables flexbox layout for the container.
*   `flex-col`: Sets flex direction to column (for mobile view).
*   `gap-8`: Spacing between flex items (Tailwind's gap scale, 8 units).
*   `items-center`: Aligns flex items vertically to the center.
*   `sm:flex-row`:  Applies `flex-row` (flex direction to row) for small screens and above (responsive breakpoint).
*   `relative`: Positions the div relatively, enabling absolute positioning of child elements.
*   `w-full`: Sets width to 100% of the parent container.
*   `bg-gray-700`: Input background color (slightly lighter gray).
*   `rounded-full`:  Rounds the input's corners to create a pill shape.
*   `p-2`: Padding for the input.
*   `pl-10`: Left padding for the input to accommodate the search icon.
*   `focus:w-full`: When the input is focused, set width to 100%.
*   `absolute`: Positions the search icon absolutely within the relative parent.
*   `left-2`: Positions the icon 2 units from the left.
*   `top-1/2`: Positions the icon at 50% from the top.
*   `transform -translate-y-1/2`: Vertically centers the icon precisely.
*   `text-gray-400`: Sets the color of the search icon to a light gray.
*   `text-center`: Centers text within the div.
*   `bg-red-500`: Background color for the cart count circle (red).
*   `rounded-full`: Makes the cart count circle round.
*   `text-xs`: Text size extra small.
*   `text-white`: Text color white.
*   `absolute -top-2 -right-2`: Positions the cart count circle at the top-right corner, slightly outside.
*   `w-4 h-4`: Sets width and height to 4 units for the cart count circle.
*   `flex items-center justify-center`: Centers the number within the cart count circle.

> **Flexbox**
> Flexbox is a CSS layout module that provides an efficient way to arrange, align, and distribute space among items in a container, even when their size is unknown or dynamic. It is particularly useful for designing one-dimensional layouts.

> **Responsive Design**
> Responsive design is an approach to web design that aims to make web pages render well on a variety of devices and screen sizes, from desktop monitors to mobile phones. Tailwind CSS uses breakpoints to apply different styles at different screen sizes.

### Main Content Area

The main content area will house the category filters sidebar and the product display grid.

```html
<main class="flex flex-col mx-auto container max-w-6xl md:flex-row">
    <div class="space-y-4 p-2 w-full max-w-[10rem]">
        <h2>Filters</h2>
        <h3>Category</h3>
        <div id="filters-container" class="text-xl space-y-2">
            <div>
                <input type="checkbox" class="check" id="cameras">
                <label for="cameras">Cameras</label>
            </div>
            <div>
                <input type="checkbox" class="check" id="smartphones">
                <label for="smartphones">Smartphones</label>
            </div>
            <div>
                <input type="checkbox" class="check" id="games">
                <label for="games">Games</label>
            </div>
            <div>
                <input type="checkbox" class="check" id="televisions">
                <label for="televisions">Televisions</label>
            </div>
        </div>
    </div>

    <div id="products-wrapper" class="w-full max-w-4xl mx-auto grid grid-cols-2 gap-6 place-content-center p-4 sm:grid-cols-3 xl:grid-cols-4">
        <!-- Products will be dynamically inserted here by JavaScript -->
    </div>
</main>
```

**Tailwind CSS Classes Explained (Main Content Area):**

*   `flex flex-col`: Enables flexbox and sets direction to column (stacking sidebar and product area).
*   `mx-auto container max-w-6xl`: Centers and sets maximum width for the main container, similar to the nav.
*   `md:flex-row`: Changes flex direction to row for medium screens and above, creating a sidebar layout.
*   `space-y-4`: Adds vertical spacing between elements within the filters div.
*   `p-2`: Padding for the filters div.
*   `w-full`: Filters div takes full width initially.
*   `max-w-[10rem]`: Sets a maximum width for the filters sidebar (using arbitrary value syntax in Tailwind CSS).
*   `text-xl`: Sets text size for category labels to extra-large.
*   `space-y-2`: Adds vertical spacing between category checkboxes.
*   `w-full max-w-4xl mx-auto`:  Sets width, maximum width, and centers the products wrapper.
*   `grid`: Enables CSS Grid layout for the products.
*   `grid-cols-2`: Sets initial grid columns to 2.
*   `gap-6`: Spacing between grid items (products).
*   `place-content-center`: Centers grid content if there's extra space.
*   `p-4`: Padding for the products wrapper.
*   `sm:grid-cols-3`: Changes grid columns to 3 for small screens and above.
*   `xl:grid-cols-4`: Changes grid columns to 4 for extra-large screens and above.

> **CSS Grid**
> CSS Grid Layout is a powerful CSS layout module that allows for two-dimensional layouts, meaning it can handle both columns and rows. It provides a grid-based system for arranging elements on a page, offering more control and flexibility than flexbox for complex layouts.

At this point, you have the basic HTML structure styled with Tailwind CSS. The product display area is currently empty, and we will populate it dynamically using JavaScript in the next section.

## JavaScript Functionality

Now, we will add JavaScript code to `script.js` to bring our UI to life. This includes:

1.  **Product Data:**  Defining an array of product objects.
2.  **DOM Element Selection:**  Selecting HTML elements that we need to interact with.
3.  **Dynamic Product Rendering:**  Creating and appending product elements to the product wrapper.
4.  **Add/Remove from Cart Functionality:**  Implementing the "Add to Cart" and "Remove from Cart" button behavior and updating the cart count.
5.  **Category Filtering:**  Implementing filtering based on selected categories.
6.  **Product Search:**  Implementing product search functionality.
7.  **Combining Filtering and Search:**  Ensuring search operates within selected categories.

### Product Data

First, define an array of product objects in `script.js`. This data will represent our products and their details. You can copy this data from the provided resources:

```javascript
const products = [
    {
        "name": "PlayStation 5",
        "category": "games",
        "price": 499,
        "url": "images/playstation.webp"
    },
    {
        "name": "Samsung Galaxy S23",
        "category": "smartphones",
        "price": 799,
        "url": "images/samsung-galaxy.webp"
    },
    {
        "name": "Sony A7 IV",
        "category": "cameras",
        "price": 2499,
        "url": "images/sony-a7.webp"
    },
    // ... (rest of the product data)
];
```

This `products` array contains objects, each representing a product with properties like `name`, `category`, `price`, and `url` (image URL).

### DOM Element Selection

Select the necessary DOM elements using JavaScript selectors:

```javascript
const productsWrapper = document.getElementById('products-wrapper');
const checkboxes = document.querySelectorAll('.check');
const filtersContainer = document.getElementById('filters-container');
const searchInput = document.getElementById('search');
const cartCountElement = document.getElementById('cart-count');
```

*   `document.getElementById()`: Selects a single element by its `id`.
*   `document.querySelectorAll()`: Selects all elements that match a CSS selector (in this case, elements with the class `check`).

> **DOM (Document Object Model)**
> The DOM is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as a tree of objects, where each object represents a part of the document. JavaScript uses the DOM to interact with HTML elements.

### Dynamic Product Rendering

Create a function `createProductElement` to generate the HTML for each product dynamically:

```javascript
let cartItemCount = 0;
let productElements = [];

function createProductElement(product) {
    const productElement = document.createElement('div');
    productElement.className = 'item space-y-2';
    productElement.innerHTML = `
        <div class="bg-gray-100 flex justify-center relative overflow-hidden border rounded-xl group cursor-pointer">
            <img src="images/${product.url}" alt="${product.name}" class="w-full h-full object-cover">
            <button class="status bg-black text-white absolute bottom-0 left-0 right-0 text-center py-2 translate-y-full transition-transform group-hover:translate-y-0">Add to cart</button>
        </div>
        <p class="text-xl">${product.name}</p>
        <p><strong>$${product.price.toLocaleString()}</strong></p>
    `;

    const statusButton = productElement.querySelector('.status');
    statusButton.addEventListener('click', updateCart);

    productElements.push(productElement);
    return productElement;
}
```

**Explanation:**

*   `createProductElement(product)`: This function takes a product object as input.
*   `document.createElement('div')`: Creates a new `div` element.
*   `productElement.className = 'item space-y-2'`: Sets the CSS classes for the product container.
*   `productElement.innerHTML = \``...\``: Sets the inner HTML of the product element using a template literal, dynamically inserting product data (`product.url`, `product.name`, `product.price`).
*   ``${product.url}``, ``${product.name}``, ``${product.price.toLocaleString()}``:  These are template literals used to embed JavaScript expressions within the HTML string. `toLocaleString()` formats the price with commas for thousands separators.
*   `productElement.querySelector('.status')`: Selects the "Add to cart" button within the product element.
*   `statusButton.addEventListener('click', updateCart)`: Attaches a click event listener to the button, calling the `updateCart` function when clicked.
*   `productElements.push(productElement)`: Adds the created product element to the `productElements` array.
*   `return productElement`: Returns the created product element.

> **Template Literals**
> Template literals (backtick-quoted strings) are string literals allowing embedded expressions. You can embed expressions using `${expression}`. They can also span multiple lines and allow string interpolation and tagged templates.

> **Event Listener**
> An event listener is a procedure or function in JavaScript that waits for an event to occur. In web development, events can be user actions like clicks, key presses, or page loading. When a specified event occurs on a particular HTML element, the event listener executes a predefined function.

Loop through the `products` array and append each product element to the `productsWrapper`:

```javascript
products.forEach(product => {
    const productElement = createProductElement(product);
    productsWrapper.appendChild(productElement);
});
```

*   `products.forEach(...)`: Iterates over each product in the `products` array.
*   `createProductElement(product)`: Calls the function to create a product element for each product.
*   `productsWrapper.appendChild(productElement)`: Appends the created product element as a child to the `productsWrapper` element, displaying it on the page.

> **Array Methods (forEach)**
> `forEach` is a higher-order array method that executes a provided function once for each element in an array. It's used to iterate over array elements and perform operations on them.

### Add/Remove from Cart Functionality

Implement the `updateCart` function to handle adding and removing items from the cart:

```javascript
function updateCart(event) {
    const statusElement = event.target;

    if (statusElement.classList.contains('added')) {
        // Remove from cart
        statusElement.classList.remove('added');
        statusElement.innerText = 'Add to cart';
        statusElement.classList.remove('bg-red-600');
        statusElement.classList.add('bg-black');
        cartItemCount--;
    } else {
        // Add to cart
        statusElement.classList.add('added');
        statusElement.innerText = 'Remove from cart';
        statusElement.classList.remove('bg-black');
        statusElement.classList.add('bg-red-600');
        cartItemCount++;
    }
    updateCartItemCountDisplay();
}

function updateCartItemCountDisplay() {
    cartCountElement.innerText = cartItemCount.toString();
}

updateCartItemCountDisplay(); // Initialize cart count display
```

**Explanation:**

*   `updateCart(event)`: This function is called when the "Add to cart" or "Remove from cart" button is clicked. It receives the `event` object.
*   `const statusElement = event.target`: Gets the button element that was clicked (`event.target`).
*   `statusElement.classList.contains('added')`: Checks if the button already has the class `added` (which we'll add when an item is in the cart).
*   **Remove from cart (if `added` class exists):**
    *   `statusElement.classList.remove('added')`: Removes the `added` class.
    *   `statusElement.innerText = 'Add to cart'`: Changes the button text back to "Add to cart".
    *   `statusElement.classList.remove('bg-red-600')`: Removes the red background color.
    *   `statusElement.classList.add('bg-black')`: Adds the black background color back.
    *   `cartItemCount--`: Decrements the `cartItemCount`.
*   **Add to cart (if `added` class does not exist):**
    *   `statusElement.classList.add('added')`: Adds the `added` class.
    *   `statusElement.innerText = 'Remove from cart'`: Changes the button text to "Remove from cart".
    *   `statusElement.classList.remove('bg-black')`: Removes the black background color.
    *   `statusElement.classList.add('bg-red-600')`: Adds the red background color.
    *   `cartItemCount++`: Increments the `cartItemCount`.
*   `updateCartItemCountDisplay()`: Calls the function to update the cart count display in the navigation bar.
*   `updateCartItemCountDisplay()`: This function updates the `cartCountElement`'s text content with the current `cartItemCount`.
*   `updateCartItemCountDisplay()` (initial call): Initializes the cart count display to "0" when the page loads.

> **classList Property**
> The `classList` property in JavaScript is a read-only property that returns a live `DOMTokenList` collection of the class attributes of the element. It provides methods like `add()`, `remove()`, `contains()`, and `toggle()` to manipulate the CSS classes of an element dynamically.

### Category Filtering

Implement the `filterProducts` function to filter products based on selected categories and the search term. Also, add event listeners for the category checkboxes and the search input:

```javascript
filtersContainer.addEventListener('change', filterProducts);
searchInput.addEventListener('input', filterProducts);

function filterProducts() {
    const searchTerm = searchInput.value.trim().toLowerCase();
    const checkedCategories = Array.from(checkboxes)
        .filter(checkbox => checkbox.checked)
        .map(checkbox => checkbox.id);

    productElements.forEach((productElement, index) => {
        const product = products[index];
        const matchesSearchTerm = product.name.toLowerCase().includes(searchTerm);
        const isInCheckedCategory = checkedCategories.length === 0 || checkedCategories.includes(product.category);

        if (matchesSearchTerm && isInCheckedCategory) {
            productElement.classList.remove('hidden');
        } else {
            productElement.classList.add('hidden');
        }
    });
}
```

**Explanation:**

*   `filtersContainer.addEventListener('change', filterProducts)`: Adds a `change` event listener to the `filtersContainer`. When any checkbox within the container changes its state (checked or unchecked), `filterProducts` is called.
*   `searchInput.addEventListener('input', filterProducts)`: Adds an `input` event listener to the `searchInput`.  As the user types in the search input, `filterProducts` is called.
*   `function filterProducts()`: This function performs the product filtering logic.
*   `const searchTerm = searchInput.value.trim().toLowerCase()`: Gets the search term from the input, removes leading/trailing whitespace (`trim()`), and converts it to lowercase.
*   `const checkedCategories = ...`:  Gets an array of IDs (category names) of the checked checkboxes:
    *   `Array.from(checkboxes)`: Converts the `NodeList` of checkboxes to an array.
    *   `.filter(checkbox => checkbox.checked)`: Filters the array to keep only checked checkboxes.
    *   `.map(checkbox => checkbox.id)`: Maps the filtered array to an array of checkbox IDs (which are category names).

> **Array Methods (filter, map)**
> `filter` is a higher-order array method that creates a new array with all elements that pass the test implemented by the provided function.
> `map` is a higher-order array method that creates a new array by calling a provided function on every element in the calling array.

*   `productElements.forEach((productElement, index) => { ... })`: Iterates through each product element and its corresponding product data.
*   `const product = products[index]`: Gets the product object from the `products` array using the index.
*   `const matchesSearchTerm = product.name.toLowerCase().includes(searchTerm)`: Checks if the product name (converted to lowercase) includes the `searchTerm`.
*   `const isInCheckedCategory = checkedCategories.length === 0 || checkedCategories.includes(product.category)`: Checks if the product's category is in the `checkedCategories` array, or if no categories are checked (in which case `checkedCategories.length === 0` is true, and all categories are considered).
*   **Conditional Display (`if (matchesSearchTerm && isInCheckedCategory)`)**:
    *   If both `matchesSearchTerm` and `isInCheckedCategory` are true (product matches search term AND is in a checked category OR no categories are checked), then:
        *   `productElement.classList.remove('hidden')`: Removes the `hidden` class from the product element, making it visible.
    *   `else`: Otherwise (product does not match search term OR is not in a checked category):
        *   `productElement.classList.add('hidden')`: Adds the `hidden` class to the product element, hiding it (using Tailwind CSS's `hidden` utility class which sets `display: none;`).

> **Higher-Order Array Methods**
> Higher-order array methods are functions that operate on arrays and can take other functions as arguments or return functions.  Examples include `forEach`, `map`, `filter`, `reduce`, and `sort`. They are powerful tools for functional programming in JavaScript and make array manipulation more concise and readable.

## Conclusion

Congratulations! You have successfully built a product filtering UI using vanilla JavaScript and Tailwind CSS. This project demonstrates fundamental web development concepts such as DOM manipulation, event handling, and responsive design using a utility-first CSS framework.

This educational guide has covered:

*   Setting up the development environment.
*   Structuring the HTML with Tailwind CSS for styling and responsiveness.
*   Writing JavaScript to dynamically render products, implement "Add to Cart" functionality, category filtering, and product search.
*   Utilizing higher-order array methods for efficient data manipulation.

This project serves as a solid foundation for further exploration into more complex front-end development topics and frameworks. You can extend this project by adding features like persistent cart storage (using localStorage), more advanced filtering options (price range, ratings), or integrating with a backend API to fetch product data dynamically.
