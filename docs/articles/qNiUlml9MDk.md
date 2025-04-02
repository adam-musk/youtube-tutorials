---
layout: "../../layouts/BlogPost.astro"
title: "Building a QR Code Generator with Vanilla JavaScript"
pubDate: "2025-03-01 14:20:25.149987"
youtubeVideoID: "qNiUlml9MDk"
index:
---

# Building a QR Code Generator with Vanilla JavaScript

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/qNiUlml9MDk" frameborder="0" allowfullscreen></iframe>

## Introduction to QR Code Generation

In today's digital age, QR codes (Quick Response codes) have become ubiquitous.  You've likely encountered them everywhere, from restaurant menus to advertisements and payment systems. These matrix barcodes offer a quick and efficient way to share information, primarily URLs, with users via a simple scan using a smartphone camera.

This chapter will guide you through the process of building your own QR code generator using **vanilla JavaScript**.

> **Vanilla JavaScript:** Refers to using plain JavaScript without relying on any external libraries or frameworks. It emphasizes writing code using the core features of the JavaScript language.

This project is inspired by the practical application of QR codes in restaurants, where they are often used to provide customers with digital menus.  Imagine visiting a restaurant and scanning a QR code to instantly access the menu on your phone – that's the kind of functionality we aim to enable with our generator.

We will create a web application that allows users to input a URL, select a desired size for the QR code, and then generate the corresponding visual code.  Users will also have the option to save the generated QR code as an image for printing or digital sharing.

## Project Overview and Potential

This project is designed to be a simple yet functional application, achievable within a few hours of development time.  The core features of our QR code generator will include:

*   **URL Input:** A user-friendly form field for entering the website address or any text-based information to be encoded in the QR code.
*   **Size Selection:** Options to choose the dimensions of the generated QR code, allowing for customization based on intended use.
*   **QR Code Generation:**  Utilizing a JavaScript library to dynamically create the QR code image based on the user's input.
*   **Download Functionality:** A feature to save the generated QR code as a downloadable image file (e.g., PNG format).

Beyond its practical utility, this project serves as an excellent example of a **side project** with several potential benefits.

> **Side Project:** A project undertaken in one's free time, often for personal enjoyment, skill development, or to explore new ideas outside of regular work or study.

Such projects, even simple ones, can be valuable for:

*   **Portfolio Building:** Demonstrating practical coding skills and problem-solving abilities to potential employers.
*   **Skill Enhancement:**  Providing hands-on experience with JavaScript, HTML, and CSS.
*   **Potential Revenue Generation:**  With further development and marketing efforts, a QR code generator could potentially generate **monthly recurring revenue** through avenues like advertising or premium features.

> **Monthly Recurring Revenue (MRR):** A predictable income stream that a business can expect to receive every month, often from subscriptions or ongoing services.

While the QR code generator market is competitive, creating your own version is a worthwhile endeavor for learning and portfolio enrichment.  It exemplifies how a relatively small project can offer significant learning opportunities and potential real-world applications.

## Technologies and Libraries

To build our QR code generator, we will leverage the following technologies and libraries:

*   **Vanilla JavaScript:** As mentioned, we will use core JavaScript for the application's logic and functionality, avoiding the complexities of larger frameworks for this relatively simple project.
*   **Tailwind CSS:** For styling the user interface (**UI**) and creating a visually appealing design without writing custom **CSS**.

    > **User Interface (UI):**  The means by which a user interacts with a computer system, application, or device. In web development, it refers to the visual elements and interactive components of a website or web application that users see and interact with.

    > **CSS (Cascading Style Sheets):** A stylesheet language used to describe the presentation of a document written in HTML or XML (including XML dialects such as SVG, MathML or XHTML). CSS describes how elements should be rendered on screen, on paper, in speech, or on other media.

    **Tailwind CSS** is a utility-first CSS framework that provides pre-defined classes for styling HTML elements directly within the HTML markup. This approach accelerates UI development and promotes consistency in design.

*   **QRCode.js:** A JavaScript library specifically designed for generating QR codes in the browser.  This library simplifies the complex process of QR code creation by providing a straightforward **API** to generate QR codes from text or URLs.

    > **API (Application Programming Interface):** A set of rules and specifications that software programs can follow to communicate with each other.  An API allows developers to use pre-built functionalities and services from other software components or systems.

We will include both Tailwind CSS and QRCode.js in our project using **CDNs** (Content Delivery Networks) for simplicity and ease of setup.

> **CDN (Content Delivery Network):** A geographically distributed network of servers that cache static content (like CSS, JavaScript files, and images) and deliver it to users based on their location. Using a CDN improves website loading speed and performance.

## Setting Up the Project Environment

Let's begin by setting up our development environment.  We will need the following:

1.  **Text Editor:** A code editor to write our HTML, CSS (via Tailwind classes), and JavaScript code. VS Code (Visual Studio Code) is a popular and highly recommended free option.
2.  **Web Browser:** A modern web browser (like Chrome, Firefox, or Safari) to view and test our QR code generator.
3.  **Live Server (Optional but Recommended):**  A development server that automatically reloads your web page in the browser whenever you save changes to your code. VS Code extensions like "Live Server" can provide this functionality.

**Project Structure:**

Create a new project folder for your QR code generator. Inside this folder, create the following files and folders:

*   `index.html`:  The main HTML file to structure the webpage.
*   `js/script.js`: A folder named `js` containing a `script.js` file for our JavaScript code.
*   `img/`: A folder named `img` to store any images (optional for this project, but good practice).

**index.html - Basic Structure:**

Open `index.html` in your text editor and start with an HTML5 **boilerplate**.

> **Boilerplate:** A basic template of code that can be reused as a starting point for projects. In HTML, a boilerplate typically includes the basic HTML structure (`<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>` tags) and essential meta tags.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QR Code Generator</title>
    <script src="js/script.js" defer></script>
</head>
<body>
    <h1>QR Code Generator</h1>
</body>
</html>
```

*   `<!DOCTYPE html>`: Declares the document type as HTML5.
*   `<html lang="en">`:  The root element of the HTML document, specifying the language as English.
*   `<head>`: Contains meta-information about the HTML document, such as character set, viewport settings, and title.
    *   `<meta charset="UTF-8">`: Sets the character encoding to UTF-8, supporting a wide range of characters.
    *   `<meta name="viewport" content="width=device-width, initial-scale=1.0">`: Configures the **viewport** for responsive design, ensuring proper scaling on different devices.

        > **Viewport:** The visible area of a web page to the user. It varies with the device screen size. The viewport meta tag controls how the page is scaled and sized on different devices.

    *   `<title>QR Code Generator</title>`: Sets the title that appears in the browser tab or window title bar.
    *   `<script src="js/script.js" defer></script>`: Links our external JavaScript file `script.js`. The `defer` attribute ensures that the script is executed after the HTML document has been fully parsed, but before the browser finishes rendering the page.

*   `<body>`: Contains the visible content of the HTML document.

**Including Tailwind CSS and QRCode.js:**

To include Tailwind CSS and QRCode.js, we will use their respective CDN links. Add the following `<script>` tags within the `<head>` section of your `index.html` file, above the link to your `script.js`:

```html
<head>
    </head>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Tailwind Configuration for Poppins Font -->
    <script>
        tailwind.config = {
          theme: {
            fontFamily: {
              sans: ['Poppins', 'sans-serif'],
            },
          }
        }
      </script>
    <!-- QRCode.js CDN -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
    <script src="js/script.js" defer></script>
</head>
```

*   **Tailwind CSS CDN:**  `<script src="https://cdn.tailwindcss.com"></script>` includes the Tailwind CSS library in our project.
*   **Tailwind Configuration:** The `<script>` block configures Tailwind CSS to use the "Poppins" font as the default sans-serif font. This customizes the default font family of Tailwind CSS.
*   **QRCode.js CDN:** `<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>` includes the QRCode.js library, enabling us to generate QR codes.

With these steps completed, we have set up the basic project structure and included the necessary libraries to start building our QR code generator.

## Building the User Interface with HTML and Tailwind CSS

Now, let's construct the user interface for our QR code generator using HTML and Tailwind CSS classes.  We will structure the UI into the following sections:

1.  **Header:**  A prominent header section displaying the title of the application.
2.  **Main Content Area:** This area will be a **flexbox** container, divided into two main sections:
    *   **Text and Form Section:**  Contains introductory text and the input form for URL and size selection.
    *   **Image Section:**  Displays a placeholder image initially and will later house the generated QR code.
3.  **Generated QR Code Output Area:**  A section below the main content to display the generated QR code and a download button.

    > **Flexbox:** A CSS layout module that provides an efficient way to arrange, align, and distribute space among items in a container, even when their size is unknown or dynamic. It's particularly useful for creating responsive layouts.

**HTML Structure within `<body>`:**

Replace the `<h1>QR Code Generator</h1>` in your `index.html` `<body>` with the following structure:

```html
<body>
    <header class="bg-red-500 p-4 mb-10">
        <div class="max-w-5xl mx-auto text-xl font-bold text-white">
            QR Code Generator
        </div>
    </header>

    <main class="max-w-5xl mx-auto flex flex-col-reverse md:flex-row md:max-w-4xl items-center justify-center mt-20 p-10">
        <div class="w-full md:w-2/3 md:mr-24 self-center">
            <h1 class="text-3xl font-bold mb-5 md:text-4xl">QR Code Generator</h1>
            <p class="mb-4">This is a simple QR code generator built with Vanilla JavaScript and Tailwind CSS.</p>
            <p class="mb-4">Enter a URL below to generate a QR code.</p>

            <form id="generate-form" class="mt-4">
                <input type="url" id="url" class="w-full border-2 border-gray-200 rounded p-3 text-gray-700 mr-2 focus:outline-none mb-5" placeholder="Enter a URL" required>

                <select id="size" class="w-full border-2 border-gray-200 rounded p-3 text-gray-700 mr-2 focus:outline-none mb-5">
                    <option value="100">100x100</option>
                    <option value="200">200x200</option>
                    <option value="300" selected>300x300</option>
                    <option value="400">400x400</option>
                    <option value="500">500x500</option>
                    <option value="600">600x600</option>
                    <option value="700">700x700</option>
                </select>

                <button type="submit" class="bg-gray-600 rounded w-full text-white py-3 px-4 mt-5 hover:bg-black">Generate QR Code</button>
            </form>
        </div>

        <div class="w-full md:w-1/3 self-center mb-10 md:mb-0">
            <img src="img/qr-code.png" class="w-1/2 mx-auto md:w-full mb-10 md:mb-0" alt="QR Code Example">
        </div>
    </main>

    <div id="generated" class="max-w-5xl mx-auto flex flex-col items-center justify-center text-center mt-20">
        <div id="spinner" class="hidden">
            <svg class="animate-spin -ml-1 mr-3 h-10 w-10 text-gray-700" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            <span class="sr-only">Loading...</span>
        </div>
        <div id="qrcode" class="mx-auto"></div>
    </div>

    <style>
        #spinner { display: none; }
    </style>
</body>
```

**Explanation of HTML Structure and Tailwind CSS Classes:**

*   **`<header>`:**
    *   `bg-red-500`: Sets the background color to red-500 from Tailwind's color palette.
    *   `p-4`: Adds padding of size 4 on all sides.
    *   `mb-10`: Adds margin-bottom of size 10.
    *   `<div class="max-w-5xl mx-auto text-xl font-bold text-white">`:  A container to limit the header's width and center its content.
        *   `max-w-5xl`: Sets the maximum width to Tailwind's 5xl breakpoint.
        *   `mx-auto`: Centers the container horizontally using auto margins.
        *   `text-xl`: Sets the text size to extra-large.
        *   `font-bold`: Makes the text bold.
        *   `text-white`: Sets the text color to white.

*   **`<main>`:**
    *   `max-w-5xl mx-auto`:  Container for the main content, similar to the header container.
    *   `flex flex-col-reverse md:flex-row md:max-w-4xl items-center justify-center mt-20 p-10`:  Configures the main content as a flex container.
        *   `flex`: Enables flexbox layout.
        *   `flex-col-reverse`:  Stacks flex items vertically in reverse order (image on top on small screens).
        *   `md:flex-row`:  On medium screens and above (**responsive layout**), switches to a horizontal row layout.

            > **Responsive Layout:** A web design approach that aims to make web pages render well on a variety of devices and screen sizes by using flexible grids and layouts, images, and CSS media queries.

        *   `md:max-w-4xl`:  On medium screens and above, sets the maximum width to 4xl.
        *   `items-center`: Aligns items vertically to the center within the flex container.
        *   `justify-center`: Centers items horizontally within the flex container.
        *   `mt-20`: Adds margin-top of size 20.
        *   `p-10`: Adds padding of size 10 on all sides.

    *   **Text and Form Section (`<div>` with `w-full md:w-2/3 md:mr-24 self-center`):**
        *   `w-full`:  Takes full width on small screens.
        *   `md:w-2/3`:  On medium screens and above, takes two-thirds width.
        *   `md:mr-24`:  On medium screens and above, adds margin-right of size 24.
        *   `self-center`: Aligns this flex item to the center vertically within the flex container.
        *   `<h1 class="text-3xl font-bold mb-5 md:text-4xl">`:  Heading for the section.
            *   `text-3xl`: Text size 3xl.
            *   `font-bold`: Bold text.
            *   `mb-5`: Margin-bottom of size 5.
            *   `md:text-4xl`: On medium screens and above, text size 4xl.
        *   `<p class="mb-4">`: Paragraph elements with `mb-4` for margin-bottom.
        *   `<form id="generate-form" class="mt-4">`: The form element.
            *   `id="generate-form"`:  Sets the **ID** of the form to `generate-form` for JavaScript access.

                > **ID:** A unique identifier assigned to an HTML element within a document. IDs are used to target and manipulate specific elements using CSS and JavaScript.

            *   `class="mt-4"`: Adds margin-top of size 4.
            *   `<input type="url" id="url" ...>`: URL input field.
                *   `type="url"`: Specifies the input type as URL, providing browser-side validation for URLs.
                *   `id="url"`: Sets the ID to `url` for JavaScript access.
                *   `class="w-full border-2 border-gray-200 rounded p-3 text-gray-700 mr-2 focus:outline-none mb-5"`: Styles the input field using Tailwind classes for width, border, rounded corners, padding, text color, and focus outline removal.
            *   `<select id="size" ...>`: Size selection dropdown.
                *   `id="size"`: Sets the ID to `size` for JavaScript access.
                *   `class="..."`:  Styles the select dropdown similar to the input field.
                *   `<option value="...">`: Options within the dropdown, each with a `value` and displayed text.
            *   `<button type="submit" ...>`: Generate QR Code button.
                *   `type="submit"`:  Specifies the button as a form submission button.
                *   `class="..."`: Styles the button with Tailwind classes for background color, rounded corners, text color, padding, and hover effect.

    *   **Image Section (`<div>` with `w-full md:w-1/3 self-center mb-10 md:mb-0`):**
        *   `w-full`: Takes full width on small screens.
        *   `md:w-1/3`: On medium screens and above, takes one-third width.
        *   `self-center`: Aligns this flex item to the center vertically.
        *   `mb-10 md:mb-0`: Adds margin-bottom of size 10 on small screens, removes it on medium screens and above.
        *   `<img src="img/qr-code.png" class="w-1/2 mx-auto md:w-full mb-10 md:mb-0" alt="QR Code Example">`:  Displays a placeholder image.
            *   `src="img/qr-code.png"`: Sets the image source. (You'll need to place a `qr-code.png` image in the `img` folder).
            *   `class="w-1/2 mx-auto md:w-full mb-10 md:mb-0"`: Styles the image for width and centering on different screen sizes.
            *   `alt="QR Code Example"`: Provides alternative text for accessibility.

*   **Generated QR Code Output Area (`<div id="generated" ...>`):**
    *   `id="generated"`: Sets the ID to `generated` for JavaScript access.
    *   `max-w-5xl mx-auto flex flex-col items-center justify-center text-center mt-20`: Container for the generated QR code and spinner.
        *   `flex flex-col items-center justify-center text-center`: Configures as a flex column, centering items horizontally and vertically, and text alignment.
        *   `mt-20`: Adds margin-top of size 20.
    *   **Spinner (`<div id="spinner" class="hidden">`):**
        *   `id="spinner"`: Sets the ID to `spinner` for JavaScript access.
        *   `class="hidden"`: Initially hides the spinner using Tailwind's `hidden` utility. We will show it using JavaScript when generating the QR code.
        *   `<svg class="animate-spin -ml-1 mr-3 h-10 w-10 text-gray-700" ...>`: SVG code for a spinning animation. Tailwind's `animate-spin` class applies a spinning animation.
        *   `<span class="sr-only">Loading...</span>`:  Provides screen reader-only text for accessibility, indicating "Loading...".
    *   **QR Code Container (`<div id="qrcode" class="mx-auto"></div>`):**
        *   `id="qrcode"`: Sets the ID to `qrcode` for JavaScript access. This empty `<div>` will be used to insert the generated QR code using JavaScript.
        *   `class="mx-auto"`: Centers the QR code horizontally.

*   **`<style>` block:**
    *   `#spinner { display: none; }`:  CSS rule to initially hide the spinner. This provides a fallback in case the Tailwind `hidden` class is not immediately applied.

This HTML structure, combined with Tailwind CSS classes, creates a responsive and visually appealing user interface for our QR code generator.

## Implementing JavaScript Functionality

Now, let's add the JavaScript code in `js/script.js` to make our QR code generator interactive. We will implement the following functionalities:

1.  **Get DOM Elements:**  Select the necessary HTML elements (form, QR code container) using their IDs.
2.  **Form Submission Event Listener:**  Attach an **event listener** to the form to handle the `submit` event.

    > **Event Listener:** A procedure or function in JavaScript that waits for a specific event to occur (like a user clicking a button, submitting a form, or a page loading) and then executes code in response to that event.

3.  **Prevent Default Form Submission:**  Prevent the default form submission behavior, which would cause the page to reload.
4.  **Get Input Values:** Retrieve the URL and size values entered by the user from the form.
5.  **Input Validation:**  Check if the URL input field is empty. If so, display an alert message.
6.  **Show and Hide Spinner:**  Implement functions to display a loading spinner while the QR code is being generated and hide it afterwards.
7.  **Generate QR Code:** Use the QRCode.js library to generate the QR code image based on the user's input URL and size, and embed it in the designated `<div>`.
8.  **Clear UI:** Create a function to clear any previously generated QR code and save button from the UI before generating a new one.
9.  **Create Save Button:** Dynamically create a download button that allows users to save the generated QR code as an image.

**JavaScript Code in `js/script.js`:**

```javascript
// Get DOM elements
const form = document.getElementById('generate-form');
const qrCodeDiv = document.getElementById('qrcode');
const qr = document.getElementById('qrcode'); // Another reference for clearing
const spinner = document.getElementById('spinner');
const generatedDiv = document.getElementById('generated');

// Function to show the spinner
const showSpinner = () => {
    spinner.classList.remove('hidden');
};

// Function to hide the spinner
const hideSpinner = () => {
    spinner.classList.add('hidden');
};

// Function to clear the QR code and save button from UI
const clearUI = () => {
    qrCodeDiv.innerHTML = '';
    const saveButton = document.getElementById('save-link');
    if (saveButton) {
        saveButton.remove();
    }
};

// Function to generate QR code using QRCode.js
const generateQRCode = (url, size) => {
    clearUI();
    new QRCode(qrCodeDiv, {
        text: url,
        width: size,
        height: size,
    });
    // Create save button after a short delay to ensure QR code is rendered in DOM
    setTimeout(() => {
        const qrCodeImage = qrCodeDiv.querySelector('img');
        if (qrCodeImage) {
            createSaveButton(qrCodeImage.src);
        }
    }, 50); // Short delay to allow QR code to be rendered
};

// Function to create and append the save button
const createSaveButton = (saveUrl) => {
    const link = document.createElement('a');
    link.id = 'save-link';
    link.classList.add('bg-red-500', 'hover:bg-red-700', 'text-white', 'font-bold', 'py-2', 'rounded', 'w-1/3', 'text-center', 'mx-auto', 'my-5', 'block');
    link.href = saveUrl;
    link.download = 'qrcode'; // Default filename for download
    link.innerHTML = 'Save Image';
    generatedDiv.appendChild(link);
};

// Event listener for form submission
form.addEventListener('submit', (e) => {
    e.preventDefault(); // Prevent default form submission

    clearUI(); // Clear previous QR code and button

    const url = document.getElementById('url').value;
    const size = document.getElementById('size').value;

    if (url === '') {
        alert('Please enter a URL'); // Basic validation
    } else {
        showSpinner(); // Show spinner
        setTimeout(() => {
            hideSpinner(); // Hide spinner after a short delay
            generateQRCode(url, size); // Generate QR code
        }, 1000); // Simulate processing time (1 second)
    }
});

// Initially hide spinner (in case CSS is not loaded immediately)
hideSpinner();
```

**Explanation of JavaScript Code:**

*   **DOM Element Selection:**
    *   `const form = document.getElementById('generate-form');`
    *   `const qrCodeDiv = document.getElementById('qrcode');`
    *   `const qr = document.getElementById('qrcode');` (Another reference to the same element)
    *   `const spinner = document.getElementById('spinner');`
    *   `const generatedDiv = document.getElementById('generated');`
    These lines use `document.getElementById()` to select HTML elements based on their **IDs** and store them in JavaScript **variables**.

        > **DOM (Document Object Model):** A programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as a tree of objects.

        > **Variable:** A named storage location in a computer's memory that can hold a value. In JavaScript, variables are declared using `const`, `let`, or `var`.

*   **`showSpinner()` and `hideSpinner()` functions:**
    *   `spinner.classList.remove('hidden');` and `spinner.classList.add('hidden');` use the **classList API** to toggle the `hidden` class on the spinner element, effectively showing and hiding it.

        > **classList API:** A property of DOM elements that returns a live `DOMTokenList` representing the set of CSS class attributes of the element. It provides methods like `add()`, `remove()`, `toggle()`, and `contains()` to manipulate the element's classes.

*   **`clearUI()` function:**
    *   `qrCodeDiv.innerHTML = '';` clears the content of the QR code container, removing any previously generated QR code.
    *   `const saveButton = document.getElementById('save-link');` and the `if (saveButton) { saveButton.remove(); }` block checks if a save button exists (by checking its ID) and removes it from the **DOM** if it does.

        > **DOM (Document Object Model):**  (Refer to previous definition)

*   **`generateQRCode(url, size)` function:**
    *   `clearUI();` calls the `clearUI()` function to ensure a clean slate.
    *   `new QRCode(qrCodeDiv, { ... });` creates a new QR code object using the `QRCode` constructor from the QRCode.js library. It takes the `qrCodeDiv` element as the container and an **object** as the second argument to configure the QR code.

        > **Object:** In JavaScript, an object is a collection of key-value pairs. It's a fundamental data type used to represent structured data.

        *   `text: url`:  Sets the text to be encoded in the QR code to the provided `url`.
        *   `width: size`, `height: size`: Sets the dimensions of the QR code.
    *   `setTimeout(() => { ... }, 50);` uses `setTimeout()` to introduce a short delay. This is a workaround to ensure that the QR code image is fully rendered in the **DOM** before we try to access its `src` attribute to create the save button.

        > **setTimeout():** A JavaScript function that allows you to execute a function or code snippet after a specified delay in milliseconds. It's commonly used for asynchronous operations or to delay actions.

        *   `const qrCodeImage = qrCodeDiv.querySelector('img');`:  Uses `querySelector()` to find the `<img>` element that QRCode.js inserts within the `qrCodeDiv`.
        *   `if (qrCodeImage) { createSaveButton(qrCodeImage.src); }`: Checks if an image element was found (QR code generated successfully) and calls `createSaveButton()` passing the image's source (`src`) as the **argument**.

            > **Argument:** A value passed to a function when it is called. Arguments provide input to the function, allowing it to operate on different data.

*   **`createSaveButton(saveUrl)` function:**
    *   `const link = document.createElement('a');`: Creates a new `<a>` (anchor) element using `document.createElement()`. This element will act as our download button.
    *   `link.id = 'save-link';`: Sets the **ID** of the link to `save-link`.
    *   `link.classList.add(...);`: Adds multiple Tailwind CSS classes to style the button.
    *   `link.href = saveUrl;`: Sets the `href` **attribute** of the link to the `saveUrl`, which is the data URL of the QR code image.

        > **Attribute:** A characteristic or property of an HTML element that provides additional information or instructions to the element. Attributes are defined within the opening tag of an HTML element (e.g., `<a href="...">`).

    *   `link.download = 'qrcode';`: Sets the `download` **attribute**, which instructs the browser to download the linked resource (the QR code image) when the link is clicked, with a default filename "qrcode".
    *   `link.innerHTML = 'Save Image';`: Sets the text content of the link to "Save Image".
    *   `generatedDiv.appendChild(link);`: Appends the newly created link element as a child to the `generatedDiv` element, making it visible in the UI.

*   **Form Submission Event Listener:**
    *   `form.addEventListener('submit', (e) => { ... });`: Attaches an event listener to the `form` element that listens for the `submit` **event**. When the form is submitted (when the "Generate QR Code" button is clicked), the provided **function** (the arrow function `(e) => { ... }`) is executed.

        > **Function:** A block of organized, reusable code that performs a specific task. Functions are fundamental building blocks in programming, allowing you to modularize code and make it more readable and maintainable.

        *   `e.preventDefault();`: Prevents the default form submission behavior (page reload). `e` is the **event object** passed to the event listener function, representing the `submit` event.
        *   `clearUI();`: Calls `clearUI()` to clear any previous QR code and button.
        *   `const url = document.getElementById('url').value;` and `const size = document.getElementById('size').value;`: Get the URL and size values from the input fields using `document.getElementById()` and accessing the `.value` **property** of the input elements.

            > **Property:** A characteristic or attribute of an object. In JavaScript, objects have properties that can be accessed and modified using dot notation (e.g., `object.property`) or bracket notation (e.g., `object['property']`).

        *   `if (url === '') { alert('Please enter a URL'); }`: **Validation** check to ensure the URL input is not empty. If it's empty, an alert message is displayed.

            > **Validation:** The process of checking if user input or data meets certain criteria or rules before processing it. Input validation helps ensure data integrity and prevent errors or security vulnerabilities.

        *   `else { showSpinner(); setTimeout(() => { hideSpinner(); generateQRCode(url, size); }, 1000); }`: If the URL is not empty:
            *   `showSpinner();`: Shows the loading spinner.
            *   `setTimeout(() => { ... }, 1000);`: Uses `setTimeout()` to introduce a 1-second delay (1000 milliseconds) to simulate processing time.
                *   `hideSpinner();`: Hides the spinner after the delay.
                *   `generateQRCode(url, size);`: Calls `generateQRCode()` to generate the QR code, passing the retrieved `url` and `size` as **arguments**.

*   **`hideSpinner();` (initial call):**  This line is placed at the end of the script to ensure that the spinner is initially hidden when the page loads. This handles cases where the CSS rule to hide the spinner might not be applied immediately.

With this JavaScript code in place, our QR code generator is now fully functional. Users can input a URL, select a size, generate a QR code, and download it as an image.

## Testing and Further Development

To test your QR code generator:

1.  Open `index.html` in your web browser (ideally using Live Server for automatic reloading during development).
2.  Enter a valid URL in the input field.
3.  Select a desired size from the dropdown.
4.  Click the "Generate QR Code" button.
5.  Observe the spinner appear briefly, followed by the generated QR code appearing below.
6.  Click the "Save Image" button to download the QR code as a PNG image.
7.  Scan the generated QR code with a QR code scanner app on your smartphone to verify that it correctly redirects to the entered URL.

**Further Development Ideas:**

*   **Customizable Colors:** Allow users to customize the colors of the QR code (foreground and background).
*   **Error Correction Level:** Implement options to adjust the error correction level of the QR code, which affects its robustness against damage.
*   **Input Type Selection:**  Allow users to choose different input types besides URLs, such as plain text, contact information (vCard), or Wi-Fi credentials.
*   **More Advanced Validation:** Implement more robust input validation and error handling.
*   **Improved UI/UX:** Enhance the user interface and user experience with better styling, feedback messages, and potentially using a JavaScript framework for more complex UI interactions if further features are added.
*   **Deployment:** Deploy your QR code generator to a web hosting platform to make it accessible online, as demonstrated by the example mentioned in the transcript (qrcodes.tech).

## Conclusion: Side Projects and Continuous Learning

This chapter demonstrated how to build a functional QR code generator using vanilla JavaScript, Tailwind CSS, and the QRCode.js library. This project serves as a practical example of how relatively simple side projects can be valuable for learning, portfolio building, and even potential revenue generation.

Remember that side projects, regardless of their scale, offer excellent opportunities to:

*   **Apply Learned Skills:**  Put theoretical knowledge into practice and solidify your understanding.
*   **Experiment and Innovate:** Explore new technologies, libraries, and approaches in a low-pressure environment.
*   **Build a Portfolio:** Showcase your abilities and projects to potential employers or clients.
*   **Learn by Doing:**  Gain hands-on experience and develop problem-solving skills through real-world application.

Even if your primary goal is to work for a large tech company, having a portfolio of side projects demonstrates initiative, passion for technology, and practical coding skills, which are highly valued.

Continue to explore, experiment, and build small projects like this to enhance your skills and expand your knowledge in web development. Every project, no matter how small, contributes to your growth and opens up new possibilities.
