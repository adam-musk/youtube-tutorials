---
layout: "../../layouts/BlogPost.astro"
title: "PyScript: Running Python in the Browser"
pubDate: "2025-03-02 13:59:58.136575"
youtubeVideoID: "vxqBm6_0vyk"
index:
---

# PyScript: Running Python in the Browser

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/vxqBm6_0vyk" frameborder="0" allowfullscreen></iframe>

## Introduction to PyScript

This chapter explores PyScript, a novel framework that empowers developers to execute Python code and utilize Python packages directly within web browsers using HTML. This capability opens exciting new possibilities, particularly in fields like data science, by bringing the power of Python's extensive ecosystem to the front-end.

It is crucial to understand that PyScript is not intended to replace JavaScript for traditional front-end development tasks such as DOM manipulation or fetching data for display. Instead, PyScript shines when integrating powerful Python libraries, like Pandas and NumPy, into browser-based applications.

> **Framework:** In software development, a framework is a foundational structure that simplifies the development of applications by providing reusable components, libraries, and tools. It sets a standard way to build and deploy applications.

Currently in its alpha stage, PyScript is a very new technology with limited readily available learning resources. This chapter serves as an introductory exploration, demonstrating its core functionalities and potential.

## Setting Up PyScript

### Minimal Installation

One of PyScript's key advantages is its ease of setup. Unlike traditional software installations, PyScript requires no local installation. To integrate PyScript into your HTML project, you simply need to include two files via CDN links in the `<head>` section of your HTML document: `pi-script.js` and `pi-script.css`.

> **CDN (Content Delivery Network):** A geographically distributed network of servers that caches static content (like JavaScript and CSS files) to deliver it to users from the server closest to them, resulting in faster loading times.

The `pi-script.js` file is the core JavaScript library that enables Python execution, while `pi-script.css` provides default styling, based on Tailwind CSS, for PyScript components.  You can also choose to download these files and host them locally if preferred.

### Core Components: WebAssembly and Pyodide

PyScript's functionality is built upon two key technologies: WebAssembly (WASM) and Pyodide.

> **WebAssembly (WASM):** A binary instruction format for a stack-based virtual machine. It is designed as a portable compilation target for programming languages, enabling high-performance applications on the web.

> **Pyodide:** A Python distribution for the browser and Node.js that is based on WebAssembly. It allows running Python and installing Python packages within these environments.

Pyodide, leveraging WebAssembly, compiles Python and its standard libraries to run efficiently in the browser environment. This makes it possible to execute Python code and install Python packages directly within the browser, without server-side Python installations.  Pyodide also incorporates Micropip, a Python package installer designed for use within the browser environment.

> **Micropip:** A Python package installer specifically designed for Pyodide and browser-based Python environments. It allows installing Python packages directly in the browser without needing a traditional Python installation.

### Key Features of PyScript

PyScript boasts several compelling features that make it a valuable tool for specific web development scenarios:

*   **Python in the Browser:** Enables the execution of Python code directly within the browser environment.
*   **Python Ecosystem Access:** Grants access to the vast Python ecosystem and allows the use of various Python packages.
*   **Python-JavaScript Interoperability:** Facilitates bi-directional communication between Python and JavaScript, allowing for seamless integration of both languages within a single project. This includes accessing browser Web APIs from Python code.

    > **Web APIs (Web Application Programming Interfaces):**  A set of programming interfaces provided by web browsers that allow web developers to interact with browser functionalities and the surrounding computing environment, such as the DOM, geolocation, and more.

*   **Environment Management:** Allows developers to define project dependencies, including Python packages and external files, directly within the HTML.
*   **Visual Application Development:** Provides UI components like buttons, lists, and containers for building interactive user interfaces.

    > **UI Components (User Interface Components):** Reusable building blocks for constructing user interfaces. They include elements like buttons, input fields, dropdown menus, and containers, providing pre-built functionality and structure.

## Exploring PyScript in Practice

To understand PyScript in action, examining practical examples is beneficial. The official PyScript GitHub repository provides a wealth of examples demonstrating various functionalities. Cloning this repository and exploring the examples, particularly those utilizing libraries like Bokeh, D3, and NumPy, is a valuable learning exercise.

The `to-do.html` example within the repository is particularly instructive. It demonstrates how to interact with the Document Object Model (DOM) using Python within PyScript.

> **DOM (Document Object Model):** A programming interface for HTML and XML documents. It represents the page structure as a tree of objects, allowing programs to dynamically access and update the content, structure, and style of a website.

This example showcases event handling using the `pys-on-click` attribute, which links HTML elements to Python functions. It also illustrates how to select elements from the DOM and manipulate them using Python code, taking user inputs and dynamically updating the webpage content.

## Hands-on Demonstration: Building a Simple Array Shuffler

Let's delve into a practical example to solidify our understanding of PyScript. We will build a simple application that displays a NumPy array and allows users to shuffle its elements using a button.

### Setting up the HTML Structure

1.  **Create `index.html`:**  Start by creating an `index.html` file in your project directory.
2.  **Basic HTML Boilerplate:** Add the basic HTML structure, including the PyScript CSS and JS links in the `<head>` section as discussed earlier. Set the title to "PyScript Demo".
3.  **Disable Prettier Formatting (Optional):** If using VS Code with Prettier and "Format on Save" enabled, create a `.vscode` folder and a `settings.json` file within it. Add the following JSON to disable formatting for HTML files to prevent conflicts with Python indentation within `<pi-script>` tags:

    ```json
    {
        "editor.formatOnSave": false
    }
    ```

4.  **Add PyScript Tag:** In the `<body>` section, add a `<pi-script>` tag. This is where you will embed your Python code directly within the HTML.
5.  **Basic Python Code:** Inside the `<pi-script>` tag, write a simple Python script to print a variable to the webpage:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>PyScript Demo</title>
        <link rel="stylesheet" href="https://pyscript.net/latest/pyscript.css" />
        <script defer src="https://pyscript.net/latest/pyscript.js"></script>
    </head>
    <body>
        <pi-script>
            name = "Brad"
            print(name)
        </pi-script>
    </body>
    </html>
    ```

    > **Prettier:** A popular code formatter that automatically formats code to maintain consistent style. While helpful for languages like JavaScript and HTML, its default formatting rules can conflict with Python's indentation requirements when used within `<pi-script>` tags.

    Open `index.html` with a live server (or your preferred method to view HTML files in a browser). You should see "Brad" displayed on the webpage.

### Defining Python Functions and Variables

You can define Python functions and variables directly within the `<pi-script>` tag. For instance, to create a function that adds two numbers and displays the sum:

```html
    <pi-script>
        def get_sum(x, y):
            return x + y

        sum_result = get_sum(5, 5)
        print(sum_result)
    </pi-script>
```

This will output "10" on the webpage.

### Interacting with the DOM

To dynamically update elements on the page, you can use `pi.write()`. First, create a `<div>` element with an `id` where you want to display output:

```html
    <div id="output" class="text-3xl"></div>
    <pi-script>
        # ... Python code ...
        pi.write("output", sum_result)
    </pi-script>
```

This will place the value of `sum_result` (which is 10) inside the `<div>` with the `id` "output".  The `class="text-3xl"` is a Tailwind CSS class applied due to the inclusion of `pi-script.css`, making the text larger.

### Exploring the Python REPL

PyScript provides a `<pi-repl>` tag that embeds a Python Read-Eval-Print Loop (REPL) directly in your webpage.

> **REPL (Read-Eval-Print Loop):** An interactive programming environment that takes user input (Read), evaluates it (Eval), prints the result (Print), and loops back to read more input. It provides an immediate way to test code snippets and explore language features.

```html
    <pi-repl></pi-repl>
```

Adding this tag will display an interactive Python interpreter on your webpage, allowing you to execute Python code directly in the browser and see immediate results.  This is useful for experimentation and debugging.

### Utilizing Python Modules: Math and NumPy

PyScript allows you to import and use Python modules. For example, to use the `math` module:

```html
    <pi-script>
        import math
        pi.write("output", math.sqrt(10))
    </pi-script>
```

This will calculate and display the square root of 10 in the "output" div.

To use external packages like NumPy, you need to declare them in the `<pi-env>` tag within the `<head>` section of your HTML.

```html
    <head>
        <title>PyScript Demo</title>
        <link rel="stylesheet" href="https://pyscript.net/latest/pyscript.css" />
        <script defer src="https://pyscript.net/latest/pyscript.js"></script>
        <pi-env>
            - numpy
        </pi-env>
    </head>
```

Now you can import and use NumPy:

```html
    <pi-script>
        import numpy as np
        array = np.array([1, 5, 2, 8, 3])
        pi.write("output", array)
    </pi-script>
```

If you encounter an error like "No module named numpy" before adding `<pi-env>`, it indicates that you need to declare the package in the environment.

Using f-strings in Python allows for formatted string output:

> **f-string (Formatted String Literal):** A way to embed expressions inside string literals in Python, making string formatting more readable and concise. They are denoted by an `f` prefix before the opening quote.

```python
pi.write("output", f"My array is: {array}")
```

### Separating Python Code into External Files

For larger applications, it's best practice to separate Python code into external `.py` files, similar to how JavaScript code is often placed in `.js` files.

1.  **Create `main.py`:** Create a new file named `main.py` in the same directory as your `index.html`.
2.  **Move Python Code:** Move the Python code from within the `<pi-script>` tag in `index.html` into `main.py`.
3.  **Link `main.py` in HTML:** In your `index.html` file, replace the `<pi-script>` tag with a `<pi-script src="./main.py"></pi-script>` tag, specifying the path to your `main.py` file using the `src` attribute.

You should see the same output as before, but now your Python code is organized in a separate file.

### Building the Array Shuffler: Adding Interactivity

Let's enhance our example by adding a button to shuffle the NumPy array.

1.  **HTML Structure for Shuffling:** Modify the `index.html` body to include a `main` container for styling and center the output and a button below it:

    ```html
    <body class="bg-gray-100">
        <main class="container h-screen flex flex-col items-center justify-center">
            <div id="output" class="text-3xl"></div>
            <button id="shuffle" pys-on-click="shuffle_array()" class="mt-4 px-2 py-1 text-white bg-blue-600 rounded">Shuffle</button>
        </main>
        <pi-script src="./main.py"></pi-script>
        <pi-env>
            - numpy
        </pi-env>
    </body>
    ```

    The `pys-on-click="shuffle_array()"` attribute on the button links the button's click event to a Python function named `shuffle_array`.

2.  **Implement `shuffle_array()` in `main.py`:** In your `main.py` file, define the `shuffle_array()` function. This function will shuffle the NumPy array and update the "output" div with the shuffled array.  We will use the `random` module from Python's standard library for shuffling.

    ```python
    import numpy as np
    import random

    array = np.array([1, 5, 2, 8, 3])

    def shuffle_array(*args): # *args to accept potential event arguments
        shuffled_array = sorted(array, key=lambda k: random.random())
        pi.write("output", shuffled_array)

    pi.write("output", array) # Initial display of the array
    ```

    The `sorted(array, key=lambda k: random.random())` line uses Python's `sorted()` function along with a `lambda` function and `random.random()` to effectively shuffle the array elements randomly.

    > **Lambda function:** A small anonymous function defined using the `lambda` keyword in Python. They are often used for short, simple operations and can be used wherever function objects are required.

    Clicking the "Shuffle" button now should update the displayed array with a shuffled version.

### Accessing DOM Elements Directly

Instead of `pi.write()`, you can access DOM elements more directly using `Element()`.

```python
output_element = Element("output")
# ... later ...
output_element.element.innerHTML = f"{shuffled_array}"
```

`Element("output")` creates a proxy object representing the DOM element with the ID "output". To access the actual DOM element, you use `.element`. Then, you can use standard JavaScript DOM properties like `innerHTML` to modify the element's content.

> **Proxy Object:** In programming, a proxy object acts as an intermediary or surrogate for another object. It provides a way to control access to the original object and can add additional functionality or behavior. In PyScript, `Element()` returns a proxy that allows interaction with the DOM from Python.

### Importing Utility Functions from Separate Files

To further organize your code, you can create utility functions in separate `.py` files and import them into your main Python file.

1.  **Create `utils.py`:** Create a new file named `utils.py`.
2.  **Define Utility Function:** In `utils.py`, define a function, for example, `add_class()`, to add a CSS class to a DOM element:

    ```python
    def add_class(element, class_name):
        element.element.classList.add(class_name)
    ```

3.  **Declare `utils.py` in `<pi-env>`:** In `index.html`, add `utils.py` to the `<pi-env>` section under `paths`:

    ```html
    <pi-env>
        - numpy
        paths:
            - utils.py
    </pi-env>
    ```

4.  **Import in `main.py`:** In `main.py`, import the `add_class` function from `utils.py`:

    ```python
    from utils import add_class
    ```

5.  **Use the Utility Function:** You can now use the `add_class` function in your `shuffle_array()` function to, for example, change the color of the shuffled array:

    ```python
    def shuffle_array(*args):
        shuffled_array = sorted(array, key=lambda k: random.random())
        output_element.element.innerHTML = f"{shuffled_array}"
        add_class(output_element, "text-blue-500") # Add Tailwind CSS class for blue text
    ```

This demonstrates how to structure larger PyScript applications by separating code into modules and utility files, improving organization and maintainability.

## Conclusion

PyScript offers a compelling approach to integrating Python's power into web applications. While not intended to replace JavaScript for all front-end tasks, its ability to run Python and leverage its extensive package ecosystem within the browser opens significant possibilities, especially in data science and related fields. By understanding its setup, key features, and practical usage, as demonstrated through the array shuffler example, developers can begin to explore and harness the potential of PyScript for their web projects. Further exploration of the official examples and continued experimentation are encouraged to fully grasp the capabilities and nuances of this emerging framework.
