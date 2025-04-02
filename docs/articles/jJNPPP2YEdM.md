---
layout: "../../layouts/BlogPost.astro"
title: "Building an AI-Powered Keyword Extractor with React and OpenAI: A Comprehensive Guide"
pubDate: "2025-02-28 14:26:51.677165"
youtubeVideoID: "jJNPPP2YEdM"
index: 37
---

# Building an AI-Powered Keyword Extractor with React and OpenAI: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/jJNPPP2YEdM" frameborder="0" allowfullscreen></iframe>


This chapter will guide you through the process of building and deploying an AI-powered keyword extractor application. We will utilize React, a popular JavaScript library for building user interfaces, along with Vite, a fast build tool and development server.  For styling and pre-built components, we will leverage the Chakra UI library.  The core functionality of keyword extraction will be powered by the OpenAI Completions API, a powerful tool for natural language processing.

This project serves as an excellent example of how to customize prompts for the OpenAI API to achieve specific tasks. While we focus on keyword extraction, the principles and techniques learned here can be applied to a wide range of projects by simply modifying the prompt sent to the API.

## 1. Introduction: The Need for AI-Powered Keyword Extraction

For content creators, marketers, and researchers, identifying relevant keywords from text is a crucial task. Manually selecting keywords can be time-consuming and subjective. This application automates this process, allowing users to input any text, such as blog posts or articles, and receive a list of the most relevant keywords extracted by AI.

As a practical demonstration, consider the following example: inputting the descriptive text of a JavaScript course into our keyword extractor. The application, leveraging the OpenAI API, accurately identifies key topics such as "JavaScript," "data types," "functions," "loops," and "DOM manipulations," demonstrating its effectiveness in extracting pertinent keywords.

The application not only extracts keywords but also formats them according to our specifications.  Instead of simply returning an array of words, we instruct the API to provide a comma-separated list with each word capitalized. This highlights the power of prompt engineering in controlling the output format of the OpenAI API.

Beyond keyword extraction, this project showcases additional features for a polished user experience.  It includes:

*   **Input Validation:**  A "toast" notification appears if the user attempts to extract keywords without entering any text, providing immediate feedback and guiding user interaction.

    > **Toast:** In user interface design, a toast is a small, non-disruptive notification that appears briefly to provide feedback or information to the user without interrupting their current action.

*   **Deployment Ready:**  The tutorial emphasizes deploying the application from scratch, utilizing Hostinger, a web hosting provider known for its ease of use and comprehensive services.

## 2. Setting Up the Development Environment

Before diving into the code, we need to set up our development environment. This involves installing necessary tools and creating the project structure.

### 2.1 Prerequisites

Ensure you have the following installed on your system:

*   **Node.js:**  A JavaScript runtime environment that allows you to run JavaScript code outside of a web browser. Node.js includes npm, the Node Package Manager.
    > **Node.js:** An open-source, cross-platform JavaScript runtime environment that executes JavaScript code server-side. It allows developers to use JavaScript for backend development and build scalable network applications.

*   **npm (Node Package Manager):** A package manager for JavaScript, included with Node.js. npm is used to install and manage project dependencies.
    > **npm (Node Package Manager):** A package manager for JavaScript. It is the default package manager for Node.js and is used to install, share, and manage dependencies for JavaScript projects.

### 2.2 Creating a React Project with Vite

We will use Vite to create a new React project. Vite offers a faster and more streamlined development experience compared to traditional tools like Create React App.

1.  **Open your terminal** and navigate to the directory where you want to create your project.

2.  **Run the following command:**

    ```bash
    npm create vite@latest ai-keyword-extractor
    ```

    This command uses `npm create vite@latest` to scaffold a new Vite project named `ai-keyword-extractor`.

    > **Vite:** A build tool and development server for modern web projects. It's known for its speed and efficiency, especially in development, due to its use of native ES modules.

3.  **Select the framework:** You will be prompted to select a framework. Choose **React**.

4.  **Select the variant:** Choose **JavaScript**. (You can also choose TypeScript if you prefer type-safe JavaScript).

5.  **Navigate into the project directory:**

    ```bash
    cd ai-keyword-extractor
    ```

6.  **Open the project in your code editor:**  Visual Studio Code (VS Code) is recommended, but you can use any code editor you prefer.

    ```bash
    code .
    ```

### 2.3 Configuring the Development Server Port (Optional)

By default, Vite runs the development server on port 5173.  To change this to port 3000 (as in the tutorial), modify the `vite.config.js` file in the project root:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
})
```

### 2.4 Installing Dependencies

Before running the development server, install the project dependencies, including React itself and other necessary packages.

1.  **Open your terminal within the project directory.**

2.  **Run the command:**

    ```bash
    npm install
    ```

    This command reads the `package.json` file and installs all listed dependencies into the `node_modules` folder.

### 2.5 Running the Development Server

Start the development server to preview your application in the browser.

1.  **Run the command:**

    ```bash
    npm run dev
    ```

2.  **Open your browser** and navigate to `http://localhost:3000` (or `http://localhost:5173` if you did not change the port). You should see the default Vite + React landing page.

### 2.6 Cleaning Up Boilerplate Code

Vite projects come with minimal boilerplate code compared to Create React App, making cleanup straightforward.

1.  **Delete `src/App.css`:**  We will be using Chakra UI for styling, so this CSS file is not needed.

2.  **Clear `src/index.css`:** Remove all default styles from this file, but keep the file itself as a potential place for global styles if needed.

3.  **Optionally delete `src/assets/react.svg`:** This is the React logo, which is not used in this project.

### 2.7 Adding Assets

For visual enhancements, you can add images to the `src/assets` folder. In this project, a light bulb icon (`light-bulb.svg`) and the OpenAI logo (`openai.png`) are used.  You can download these from the project's GitHub repository or use your own images.

## 3. Integrating Chakra UI for Styling and Components

Chakra UI is a React UI library that provides a set of accessible, reusable, and composable UI components, making it easy to build visually appealing and functional user interfaces with minimal code.

> **UI Library (User Interface Library):** A collection of pre-built user interface components (like buttons, modals, forms, etc.) and styling utilities that developers can use to quickly build the front-end of web applications, ensuring consistency and saving development time.

> **Material UI:** Another popular React UI library, similar to Chakra UI, offering a wide range of components based on Google's Material Design principles.

> **Tailwind CSS:** A utility-first CSS framework that provides a large set of pre-defined CSS classes that can be composed to style HTML elements directly in the markup, offering a different approach to UI development compared to component libraries like Chakra UI or Material UI.

### 3.1 Installing Chakra UI and Dependencies

Install Chakra UI and its required dependencies:

1.  **Stop the development server** (if it's running) by pressing `Ctrl + C` in the terminal.

2.  **Run the following command:**

    ```bash
    npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
    ```

    This command installs:
    *   `@chakra-ui/react`: The core Chakra UI library.
    *   `@emotion/react` and `@emotion/styled`:  Libraries for CSS-in-JS styling, used by Chakra UI.
    *   `framer-motion`: An animation library, also used by Chakra UI for component animations.

### 3.2 Setting up ChakraProvider

To use Chakra UI components throughout your application, you need to wrap your root component (`App`) with the `ChakraProvider`.

1.  **Open `src/main.jsx`.**

2.  **Import `ChakraProvider`:**

    ```javascript
    import { ChakraProvider } from '@chakra-ui/react'
    ```

3.  **Wrap the `App` component with `ChakraProvider`:**

    ```jsx
    import React from 'react'
    import ReactDOM from 'react-dom/client'
    import App from './App'
    import './index.css'
    import { ChakraProvider } from '@chakra-ui/react' // Import ChakraProvider

    ReactDOM.createRoot(document.getElementById('root')).render(
      <React.StrictMode>
        <ChakraProvider> {/* Wrap App with ChakraProvider */}
          <App />
        </ChakraProvider> {/* End ChakraProvider */}
      </React.StrictMode>
    )
    ```

### 3.3 Creating Basic Layout Components in `App.jsx`

Modify `src/App.jsx` to set up the basic layout using Chakra UI components: `Box` and `Container`.

1.  **Open `src/App.jsx`.**

2.  **Import necessary Chakra UI components:**

    ```javascript
    import { Box, Container } from '@chakra-ui/react';
    ```

3.  **Modify the `App` component:**

    ```jsx
    import { Box, Container } from '@chakra-ui/react'; // Import Box and Container

    function App() {
      return (
        <Box bg="blue.600" color="white" height="100vh" pt={30}> {/* Box for background and styling */}
          <Container maxW="3xl" centerContent> {/* Container for centering content */}
            <h1>My App</h1> {/* Placeholder H1 */}
          </Container>
        </Box>
      );
    }

    export default App;
    ```

    > **Props (in React):** Short for "properties," props are inputs to React components. They are read-only values passed from parent components to child components to customize their behavior and appearance. In Chakra UI, props are used extensively to style and configure components.

    > **Fragment (in React):**  Represented as `<>` and `</>`, or `<React.Fragment>` and `</React.Fragment>`, a fragment is a way to group multiple React elements without adding an extra node to the DOM. It is used when you need to return multiple elements from a component's render method but don't want to introduce unnecessary divs or other wrapper elements.

## 4. Building UI Components: Header, Footer, and Text Input

To structure the application, we will create separate React components for the header, footer, and text input area. These components will be placed in a `components` folder within the `src` directory.

### 4.1 Creating the Header Component (`Header.jsx`)

1.  **Create a folder named `components` in `src`:** `src/components`.

2.  **Create a file named `Header.jsx` inside `src/components`.**

3.  **Add the following code to `Header.jsx`:**

    ```jsx
    import React from 'react';
    import { Heading, Image, Text, Box } from '@chakra-ui/react'; // Import Chakra UI components
    import logo from '../assets/light-bulb.svg'; // Import logo image

    function Header() {
      return (
        <> {/* React Fragment */}
          <Image src={logo} alt="logo" width="100px" mb="1rem" /> {/* Image component for logo */}
          <Heading color="white" mb="1rem" textAlign="center">AI Keyword Extractor</Heading> {/* Heading component */}
          <Text fontSize="25px" textAlign="center">Paste in your text below and we'll extract the keywords for you</Text> {/* Text component */}
        </>
      );
    }

    export default Header;
    ```

### 4.2 Creating the Footer Component (`Footer.jsx`)

1.  **Create a file named `Footer.jsx` inside `src/components`.**

2.  **Add the following code to `Footer.jsx`:**

    ```jsx
    import React from 'react';
    import { Box, Image, Text, Flex } from '@chakra-ui/react'; // Import Chakra UI components
    import logo from '../assets/openai.png'; // Import OpenAI logo

    function Footer() {
      return (
        <Box mt={50}> {/* Box component for footer container */}
          <Flex justifyContent="center" alignItems="center"> {/* Flex component for layout */}
            <Image src={logo} alt="OpenAI Logo" mr={1} width="30px" /> {/* Image component for OpenAI logo */}
            <Text>Powered by OpenAI</Text> {/* Text component */}
          </Flex>
        </Box>
      );
    }

    export default Footer;
    ```

    > **Flexbox:** A CSS layout module that provides an efficient way to arrange, align, and distribute space among items in a container, even when their size is unknown or dynamic. Chakra UI's `Flex` component is a convenient way to use flexbox layouts.

### 4.3 Creating the Text Input Component (`TextInput.jsx`)

1.  **Create a file named `TextInput.jsx` inside `src/components`.**

2.  **Add the following code to `TextInput.jsx`:**

    ```jsx
    import React, { useState } from 'react'; // Import useState hook
    import { Textarea, Button, useToast } from '@chakra-ui/react'; // Import Chakra UI components

    function TextInput({ extractKeywords }) { // Receive extractKeywords function as prop
      const [text, setText] = useState(''); // State for text input
      const toast = useToast(); // Initialize toast hook

      const submitText = () => {
        if (text === '') {
          toast({ // Show toast notification if text is empty
            title: 'Text field is empty',
            description: 'Please enter some text to extract keywords.',
            status: 'error',
            duration: 5000,
            isClosable: false,
          });
          return;
        }
        extractKeywords(text); // Call extractKeywords function with input text
      };

      return (
        <> {/* React Fragment */}
          <Textarea
            bg="blue.400"
            color="white"
            padding={4}
            marginTop={6}
            height="200px"
            value={text}
            onChange={(e) => setText(e.target.value)} // Update text state on input change
            placeholder="Paste your text here..."
          /> {/* Textarea component for text input */}
          <Button
            bg="blue.500"
            color="white"
            marginTop={4}
            width="100%"
            _hover={{ bg: 'blue.700' }} // Hover style
            onClick={submitText} // Call submitText function on button click
          >
            Extract Keywords
          </Button> {/* Button component */}
        </>
      );
    }

    export default TextInput;
    ```

    > **State (in React):** A JavaScript object that represents the dynamic data that controls the behavior and rendering of a React component. State is mutable, and changes to state trigger re-renders of the component and its children. The `useState` hook is the primary way to manage state in functional React components.

    > **Hook (in React):** Functions in React that let you "hook into" React state and lifecycle features from within functional components. Hooks were introduced in React 16.8 and allow functional components to have state and other features previously only available in class components. `useState` and `useToast` are examples of React Hooks.

    > **useToast (Chakra UI Hook):** A hook provided by Chakra UI to create and manage toast notifications within your application. It simplifies the process of displaying temporary messages to the user.

    > **useState (React Hook):** A React Hook that allows functional components to have state. It returns an array with two elements: the current state value and a function to update it.

## 5. Integrating OpenAI API for Keyword Extraction

Now we will connect our application to the OpenAI Completions API to perform keyword extraction. This involves setting up API keys, environment variables, and making API requests from our React application.

### 5.1 Obtaining an OpenAI API Key

1.  **Go to the OpenAI Platform website:** [https://platform.openai.com/](https://platform.openai.com/) and sign up or log in to your account.

2.  **Navigate to "View API keys"** under your profile menu.

3.  **Click "Create new secret key"** to generate a new API key.

4.  **Copy the API key** and store it securely.  **Important:** Treat your API key like a password and do not expose it in your client-side code or commit it to version control.

### 5.2 Setting up Environment Variables

To securely store your API key and API URL, we will use environment variables.

1.  **Create a file named `.env` in the root of your project** (not inside the `src` folder).

2.  **Add the following lines to `.env`, replacing `YOUR_OPENAI_API_KEY` with your actual API key:**

    ```
    VITE_OPENAI_API_KEY=YOUR_OPENAI_API_KEY
    VITE_OPENAI_API_URL=https://api.openai.com/v1/completions
    ```

    > **API Key:** A unique identifier used to authenticate and authorize access to an Application Programming Interface (API). It acts like a password for your application to interact with the API service.

    > **Environment Variables:**  Variables set outside the application code, typically in the operating system or a `.env` file, to configure application behavior without modifying the code directly. They are often used to store sensitive information like API keys or database credentials, and to differentiate settings between development and production environments.

    > **.env file:** A file used to store environment variables for an application, especially in development environments. It is commonly used to keep configuration settings separate from the codebase and avoid hardcoding sensitive information.

3.  **Restart your development server** after creating or modifying the `.env` file to ensure the environment variables are loaded.

4.  **Add `.env` to `.gitignore`:** To prevent accidentally committing your API key to version control, add `.env` to your `.gitignore` file. If you don't have a `.gitignore` file, create one in the root of your project and add `.env` to it.

    > **.gitignore:** A file in Git repositories that specifies intentionally untracked files that Git should ignore. It's commonly used to exclude temporary files, build artifacts, and sensitive information like `.env` files from being committed to the repository.

    **Security Note:** While `.env` files are helpful in development, storing API keys directly in front-end applications is generally not recommended for production applications with many users. For production, consider using a back-end server to handle API requests and keep your API key secure on the server-side.

    > **Front-end/Back-end (in Web Development):** The front-end is the client-side part of a web application that users interact with directly (e.g., the user interface in a browser). The back-end is the server-side part that handles data storage, processing, and API logic, often hidden from direct user interaction. In a more secure setup, the front-end would send requests to a back-end server, which would then securely interact with the OpenAI API, keeping the API key server-side.

### 5.3 Implementing the `extractKeywords` Function in `App.jsx`

Modify `App.jsx` to include the `extractKeywords` function that will make the API request to OpenAI.

1.  **Open `src/App.jsx`.**

2.  **Import `useState` Hook:** Ensure `useState` is imported from React.

3.  **Add State Variables:** Inside the `App` component, add state variables for keywords, modal open state, and loading state:

    ```javascript
    import React, { useState } from 'react'; // Ensure useState is imported
    import { Box, Container } from '@chakra-ui/react';
    import Header from './components/Header';
    import TextInput from './components/TextInput';
    import Footer from './components/Footer';
    import KeywordsModal from './components/KeywordsModal'; // Import KeywordsModal

    function App() {
      const [keywords, setKeywords] = useState(''); // State for extracted keywords
      const [isOpen, setIsOpen] = useState(false); // State for modal visibility
      const [loading, setLoading] = useState(false); // State for loading indicator

      // ... rest of your component code
    }
    ```

4.  **Implement the `extractKeywords` function:** Add the `extractKeywords` function within the `App` component:

    ```javascript
    function App() {
      // ... state variables

      const extractKeywords = async (text) => { // Async function for API request
        setLoading(true); // Set loading state to true
        setIsOpen(true); // Open the modal
        const options = {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${import.meta.env.VITE_OPENAI_API_KEY}`, // API key from environment variable
          },
          body: JSON.stringify({ // Request body as JSON
            model: 'text-davinci-003',
            prompt: `Extract keywords from this text:\n\n${text}\n\nMake the first letter of each word uppercase and separate with commas.`, // Prompt for keyword extraction
            temperature: 0.5,
            max_tokens: 60,
            frequency_penalty: 0.8,
          }),
        };

        try {
          const response = await fetch(import.meta.env.VITE_OPENAI_API_URL, options); // Fetch API request
          const json = await response.json(); // Parse JSON response
          const data = json.choices[0].text.trim(); // Extract keywords from response
          setKeywords(data); // Update keywords state
          setLoading(false); // Set loading state to false
        } catch (error) {
          console.error("Error fetching keywords:", error);
          setLoading(false); // Ensure loading is set to false even on error
          // Handle error appropriately, e.g., display an error toast
        }
      };

      const closeModal = () => {
        setIsOpen(false); // Function to close the modal
      };

      return (
        // ... JSX structure (Header, TextInput, Footer, KeywordsModal)
      );
    }
    ```

    > **Context API/Redux:** State management solutions for React applications, especially useful for complex applications with shared state across many components. Context API is built into React and suitable for simpler state management needs, while Redux is a more robust library often used for larger, more complex applications. In this project, `useState` within `App.jsx` serves as a simple form of "global state" for demonstration purposes.

    > **Global State (in React):**  State that is accessible and modifiable by multiple components throughout the application. In simpler applications, state can be lifted up to a common ancestor component (like `App` in this case) and passed down as props. For more complex applications, dedicated state management solutions like Context API or Redux are often used to manage global state more effectively.

    > **JSON (JavaScript Object Notation):** A lightweight data-interchange format that is easy for humans to read and write and easy for machines to parse and generate. It is commonly used for transmitting data in web applications, especially between a server and a client, and is often used as the format for API requests and responses.

    > **Asynchronous Function/Async-Await:** Asynchronous functions in JavaScript allow you to write promise-based code as if it were synchronous, making asynchronous operations more readable and manageable. The `async` keyword marks a function as asynchronous, and the `await` keyword pauses the execution of the function until a promise resolves (e.g., an API request completes).

    > **Fetch API:** A modern JavaScript interface for making network requests, such as fetching resources from a server or sending data to an API. It provides a more powerful and flexible alternative to older methods like `XMLHttpRequest`.

### 5.4 Passing `extractKeywords` as a Prop to `TextInput`

Pass the `extractKeywords` function down to the `TextInput` component as a prop so that the text input can trigger the keyword extraction process when the button is clicked.

1.  **In `App.jsx`, within the `TextInput` component instantiation, pass `extractKeywords` as a prop:**

    ```jsx
    <TextInput extractKeywords={extractKeywords} /> {/* Pass extractKeywords function as prop */}
    ```

### 5.5 Embedding Components in `App.jsx`

Embed the `Header`, `TextInput`, `Footer`, and `KeywordsModal` components into the `App` component's JSX structure.

1.  **In `App.jsx`, within the `return` statement, structure the components:**

    ```jsx
    return (
      <Box bg="blue.600" color="white" height="100vh" pt={30}>
        <Container maxW="3xl" centerContent>
          <Header /> {/* Header component */}
          <TextInput extractKeywords={extractKeywords} /> {/* TextInput component */}
          <Footer /> {/* Footer component */}
          <KeywordsModal // KeywordsModal component
            isOpen={isOpen}
            keywords={keywords}
            loading={loading}
            closeModal={closeModal}
          />
        </Container>
      </Box>
    );
    ```

## 6. Creating the Keywords Modal Component (`KeywordsModal.jsx`)

The `KeywordsModal` component will display the extracted keywords in a modal window. It will also show a loading spinner while the API request is in progress.

1.  **Create a file named `KeywordsModal.jsx` inside `src/components`.**

2.  **Add the following code to `KeywordsModal.jsx`:**

    ```jsx
    import React from 'react';
    import {
      Modal,
      ModalOverlay,
      ModalContent,
      ModalHeader,
      ModalFooter,
      ModalBody,
      ModalCloseButton,
      Button,
      Text,
      CircularProgress,
    } from '@chakra-ui/react'; // Import Chakra UI modal components

    function KeywordsModal({ isOpen, keywords, loading, closeModal }) { // Receive props
      return (
        <Modal isOpen={isOpen} onClose={closeModal}> {/* Modal component */}
          <ModalOverlay /> {/* Modal overlay */}
          <ModalContent> {/* Modal content container */}
            <ModalHeader>Keywords</ModalHeader> {/* Modal header */}
            <ModalCloseButton /> {/* Close button in modal header */}
            <ModalBody display="flex" alignItems="center" justifyContent="center"> {/* Modal body */}
              {loading ? ( // Conditional rendering based on loading state
                <CircularProgress isIndeterminate color="blue.300" /> // Circular progress indicator
              ) : (
                <Text>{keywords}</Text> // Display keywords if not loading
              )}
            </ModalBody>

            <ModalFooter> {/* Modal footer */}
              <Button colorScheme="blue" mr={3} onClick={closeModal}> {/* Close button in modal footer */}
                Close
              </Button>
            </ModalFooter>
          </ModalContent>
        </Modal>
      );
    }

    export default KeywordsModal;
    ```

    > **Modal:** A UI element that appears on top of the application's main content, temporarily blocking user interaction with the main content until the modal is closed. Modals are often used for dialogs, alerts, or to display focused content.

    > **Modal Overlay:** A semi-transparent layer that covers the background content when a modal is open, visually separating the modal from the rest of the application.

    > **Modal Content:** The main container within a modal that holds the header, body, and footer of the modal.

    > **Circular Progress (Chakra UI Component):** A component that displays a circular loading indicator, often used to indicate that a process is ongoing or data is being fetched. The `isIndeterminate` prop makes the progress indicator spin continuously, useful when the exact progress is unknown.

    > **Ternary Operator:** A concise conditional operator in JavaScript (and many other languages) written as `condition ? expressionIfTrue : expressionIfFalse`. It provides a shorthand for writing simple if-else statements.

## 7. Deployment with Hostinger

Hostinger is a web hosting provider that offers easy deployment options. We will use Hostinger's hPanel to deploy our React application.

### 7.1 Building the Production Application

Before deploying, you need to build a production-ready version of your React application.

1.  **Stop the development server** (if it's running).

2.  **Run the build command:**

    ```bash
    npm run build
    ```

    This command uses Vite to build your application, creating optimized production files in the `dist` folder in your project root.

    > **Production Files:** Optimized and minified files that are ready to be deployed to a production server. These files typically include bundled JavaScript, CSS, and assets, optimized for performance and reduced file size.

### 7.2 Deploying to Hostinger via File Manager

Hostinger's hPanel provides a file manager that allows you to upload files directly to your web hosting account.

1.  **Log in to your Hostinger account** and access your hosting panel (hPanel).

2.  **Navigate to "Files"** and then **"File Manager."**

3.  **Access the file directory for your domain.** This is typically the `public_html` folder.

    > **Public HTML Folder:** The root directory on a web server where website files are stored. Files placed in this directory are publicly accessible via the website's domain.

4.  **Open the `dist` folder** in your local project directory.

5.  **Drag and drop the *contents* of the `dist` folder** (not the folder itself) into the `public_html` folder in Hostinger's file manager. This includes `index.html` and the `assets` folder.

    > **Finder (macOS):** The file manager application in macOS, used to browse and manage files and folders. Windows has "File Explorer," and Linux distributions have various file managers.

### 7.3 Accessing Your Deployed Application

Once the files are uploaded, your application should be live on your domain.

1.  **Open your web browser** and go to your domain name (e.g., `yourdomain.com`).

2.  **Test your keyword extractor** to ensure it is working correctly in the deployed environment.

    If you encounter a "403 Forbidden" error when accessing your domain, it might indicate that there is no `index.html` file in the `public_html` directory, or there might be file permission issues. Ensure that the `index.html` file from your `dist` folder is correctly placed in `public_html`.

    > **403 Error (HTTP 403 Forbidden):** An HTTP status code indicating that the server understood the request, but is refusing to authorize it. In web hosting contexts, it often occurs when there is no `index.html` file in the website's root directory, or when file permissions are incorrectly configured, preventing access to the website.

### 7.4 Alternative Deployment Methods (Git)

Hostinger also supports deployment via Git. This method is more suitable for ongoing development and continuous deployment.

1.  **In Hostinger's hPanel, navigate to "Advanced"** and then **"Git."**

2.  **Initialize a Git repository** in your hosting account.

3.  **Connect your local Git repository** to the remote repository on Hostinger.

4.  **Push your code** to the remote repository. Hostinger can be configured to automatically deploy your application whenever you push changes to the repository.

    For Git-based deployment, you may need to set up an SSH key for secure authentication between your local machine and the Hostinger server.

    > **Repository (Git Repository):** A storage location for a software project, tracking all changes made to the code over time. Git repositories contain the project's files, history of changes (commits), branches, and other metadata.

    > **SSH Key (Secure Shell Key):** A cryptographic key pair used for secure authentication, often used to access remote servers or Git repositories without needing to enter passwords repeatedly. SSH keys provide a more secure and convenient way to authenticate compared to password-based authentication.

## 8. Conclusion and Further Exploration

Congratulations! You have successfully built and deployed an AI-powered keyword extractor using React, Chakra UI, and the OpenAI Completions API. This project demonstrates the power of combining front-end technologies with AI APIs to create practical and intelligent applications.

**Key Takeaways:**

*   **Prompt Engineering is Crucial:** The effectiveness of the OpenAI API heavily relies on well-crafted prompts. Experiment with different prompts to customize the output and explore various functionalities beyond keyword extraction.
*   **Component-Based UI with Chakra UI:** Chakra UI simplifies UI development by providing reusable and accessible components, allowing you to focus on application logic rather than writing extensive CSS.
*   **API Integration:**  Integrating front-end applications with powerful APIs like OpenAI opens up endless possibilities for creating intelligent and automated solutions.
*   **Deployment is Streamlined:** Platforms like Hostinger make deploying web applications straightforward, even for complex projects.

**Further Exploration:**

*   **Expand Functionality:**  Enhance the keyword extractor by adding features like:
    *   Keyword frequency analysis.
    *   Keyword suggestion based on context.
    *   Integration with SEO tools.
*   **Explore Different OpenAI API Models:** Experiment with other OpenAI models beyond `text-davinci-003` to see how they affect keyword extraction results.
*   **Build Different Applications:**  Apply the learned principles to build other AI-powered applications using the OpenAI API, such as:
    *   Virtual assistants.
    *   Content summarizers.
    *   Code generators.
    *   Creative writing tools.

By continuing to explore and experiment with these technologies, you can unlock even more potential and build innovative applications that leverage the power of AI.

