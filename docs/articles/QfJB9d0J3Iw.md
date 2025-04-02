---
layout: "../../layouts/BlogPost.astro"
title: "Building AI-Powered Applications with Claude: An Educational Guide"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "QfJB9d0J3Iw"
channel: ""
index: 29
---

# Building AI-Powered Applications with Claude: An Educational Guide

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/QfJB9d0J3Iw" frameborder="0" allowfullscreen></iframe>


This chapter will guide you through building practical AI applications using Claude, Anthropic's powerful large language model. Through a series of coding challenges, you will develop hands-on skills to effectively harness Claude's capabilities in diverse projects. This material is based on a comprehensive course designed to empower developers with AI skills.

## Introduction to Claude: Anthropic's AI Model

Welcome to the world of Claude! This course, led by Sean Dasan from Scrimba, will equip you with the skills to build cutting-edge AI-powered applications. We will explore how to leverage Claude to create intelligent tools like text summarizers and image describers.

### What is Claude?

Claude is not just a single AI model, but a family of AI models developed by Anthropic.

> **AI (Artificial Intelligence)**:  A broad field of computer science focused on creating intelligent agents, which are systems that can reason, learn, and act autonomously.
> **Large Language Model (LLM)**: A type of AI model trained on massive amounts of text data to understand and generate human-like text.

Claude offers a range of models categorized by cost and intelligence, allowing you to select the most appropriate model for your specific task. These models are:

*   **Haiku:**  Offers speed and efficiency at a lower cost.
*   **Sonnet:**  Provides a balance of intelligence and cost-effectiveness.
*   **Opus:**  The most powerful and intelligent model, suited for complex tasks.

Anthropic's latest advancement is **Claude 3.5 Sonnet**, their most powerful model to date. Benchmarking data released by Anthropic indicates that Claude 3.5 Sonnet outperforms other market-leading models across various intelligence metrics.

> **Benchmarks**: Standardized tests or metrics used to evaluate and compare the performance and capabilities of different AI models.

### Claude's Capabilities

Claude excels in a wide array of applications, including:

*   **Advanced Reasoning:**  Solving complex problems and making logical inferences.
*   **Vision Analysis:**  Understanding and interpreting information from images.
*   **Code Generation:**  Writing and assisting with programming code.
*   **Multilingual Processing:**  Understanding and generating text in multiple languages.

> **Vision Analysis**: The ability of an AI model to process and interpret visual information from images or videos, understanding objects, scenes, and contexts.
> **Code Generation**:  The capability of an AI model to automatically write or assist in writing programming code based on natural language instructions or specifications.
> **Multilingual Processing**: The capacity of an AI model to understand, process, and generate text in multiple human languages.

Claude is versatile, capable of processing both text and images, functionalities we will explore in this course.

### Anthropic: The Company Behind Claude

Anthropic, the AI startup responsible for Claude, was founded in 2021 by seven former OpenAI employees, including Dario Amodei and Daniela Amodei. Anthropic distinguishes itself by its dual commitment to both AI power and **AI safety**.

> **AI Safety**: A field dedicated to researching and implementing methods to ensure that AI systems are beneficial, reliable, and aligned with human values, minimizing potential risks and unintended consequences.

They employ a unique AI model training technique called **Constitutional AI** to develop Claude as a helpful, honest, and harmless AI system. This approach prioritizes ethical AI development and aims to build trustworthy AI solutions.

> **Constitutional AI**: A specific approach to AI safety training where the AI model is trained to align with a set of principles or a "constitution," guiding its behavior to be more helpful, honest, and harmless.

Anthropic's focus on AI safety, combined with Claude's powerful capabilities, enables enterprise customers to build secure and scalable AI-powered applications.

> **Enterprise Customers**: Businesses or organizations that utilize AI technologies for large-scale operations and applications, often requiring robust security, scalability, and reliability.

### Course Overview: What You Will Learn and Build

This course will guide you through building two exciting AI-powered applications:

1.  **Text Summarizer with Claude:**  We will create an application that can summarize lengthy texts into concise summaries.
2.  **Image Describer with Claude:**  We will develop an application that can generate descriptions of images.

Through these projects, you will learn essential skills:

*   **Using Claude's Messages API:**  Interacting with Claude programmatically to send requests and receive responses.
*   **Controlling Claude's Output:**  Learning techniques to guide and refine Claude's responses to meet specific requirements.
*   **Error Handling:**  Implementing robust error handling to ensure application stability.
*   **Handling Different Media Types:**  Working with both text and image data within AI applications.
*   **Deployment of AI Applications:**  Deploying your AI-powered applications to production using Cloudflare.

> **Messages API**:  A programming interface provided by Claude that allows developers to interact with the AI model by sending and receiving messages, enabling them to build applications that leverage Claude's capabilities.
> **API Key**:  A unique security code that authenticates your access to an API (Application Programming Interface), allowing your application to interact with a service like Claude.

We will also explore Scrimba's templates, powerful tools for efficient development.

### Meet Your Instructor

Your instructor, Sean Dasan, is a seasoned software professional with experience since 2019. Currently a mentor and trainer at Scrimba, Sean specializes in teaching web development and AI engineering to aspiring developers. You can connect with Sean on X (formerly Twitter) [@ShanDasan](https://twitter.com/ShanDasan) and LinkedIn.

Let's embark on this exciting journey of building AI-powered applications with Claude!

## Building a Text Summarizer with Claude

Our first project is to build a text summarizer application. Meet Sam, an AI-generated 3D dog character who loves summarizing texts. Inspired by Sam, we will create an AI-powered text summarizer.

### Functionality of the Text Summarizer

The text summarizer will work as follows:

1.  **User Input:** A user will paste a long text into a designated text area.
2.  **Summary Length Adjustment:** The user can optionally adjust the desired summary length in words using a slider. The default length is 10 words.
3.  **Summarization Process:** Upon clicking a "Summarize" button, the text will be sent to Claude for processing.
4.  **Summary Display:**  The generated summary will be displayed in another text area.
5.  **Copy and Clear:** Users can copy the summary and clear the text areas to start a new summarization.

### System Design

The system architecture involves three main components:

*   **Front End:** The user interface (UI) where users interact with the application. This includes text areas for input and output, a slider for summary length, and buttons for actions.
*   **Back End:**  A server-side component that handles communication between the front end and Claude. It securely manages the **API key** and processes requests.
*   **Claude:** Anthropic's AI model that performs the text summarization.

The data flow is as follows:

1.  The user interacts with the **front end**, providing text and summary length preferences.
2.  The **front end** sends the text and preferences to the **back end**.
3.  The **back end** forwards the text to **Claude** for summarization.
4.  **Claude** processes the text and generates a summary, sending it back to the **back end**.
5.  The **back end** relays the summary back to the **front end**.
6.  The **front end** displays the summary to the user.

### Front-End Code Review

For this course, the basic front-end user interface (UI) has already been pre-built to focus on the AI-specific aspects. Let's review the existing code structure:

*   **`index.html`:**  Contains the HTML structure for the UI, including:
    *   Header
    *   Text area for input text
    *   Range input (slider) for summary length
    *   "Summarize" button
    *   Text area for summary output
    *   "Copy" and "Clear" buttons
*   **`index.css`:**  Contains the CSS styles to visually design the UI.
*   **`index.js`:**  The JavaScript file where we will add the AI-specific logic. It currently includes:
    *   Constants and element selectors to interact with HTML elements.
    *   Event listeners for button clicks and other UI interactions.
    *   Placeholder `summarize` function and other event handlers.
    *   Helper functions for UI management.
*   **`images/`:**  Folder containing image assets for the UI.

### Adding Loading Functionality: First Challenge

**Challenge:** Implement a loading spinner to visually indicate processing when the user clicks "Summarize."

**Solution:** Call the `startLoading()` function at the beginning of the `summarize` function in `index.js`. This function is already defined in the provided code to display a loading spinner in the UI.

```javascript
function summarize() {
    startLoading(); // Start loading spinner
    // ... rest of the summarize logic will be added later ...
}
```

This simple step enhances user experience by providing visual feedback during the summarization process.

## Obtaining and Setting Up the Anthropic API Key

To enable our application to communicate with Claude, we need an Anthropic **API key**. Let's go through the process of obtaining and setting up this key.

### Getting Your Anthropic API Key

1.  **Navigate to the Anthropic Website:** Click on the provided image link in the course material, which directs you to the Anthropic website.
2.  **Sign Up/Log In:** On the Anthropic website, under "Build with Claude," click "Get Started." Sign up for an account using your Google account or email address, providing the required information.
3.  **Create Account and Claim Free Credits:** After signing up, you will be directed to your Anthropic dashboard. New users are typically offered free credits (e.g., $5) to try out Claude. Click "Claim" to initiate this process.
4.  **Phone Number Verification:** Enter your phone number and click "Send Code." Input the received verification code and click "Confirm."
5.  **Access API Keys:** In your dashboard, click on "Get API Keys."
6.  **Create a New API Key:** Click on "Create Key," provide a descriptive name for your key, and click "Create Key."
7.  **Copy and Securely Store Your API Key:** Anthropic will display your newly generated API key. Click "Copy Key" to copy it. **Crucially, store this API key in a secure location.** You will need it throughout the course.

### Setting Up the API Key in Scrimba as an Environment Variable

For development within the Scrimba environment, we need to store the API key as an **environment variable**.

> **Environment Variable**: A dynamic-named value that can affect the way running processes will behave on a computer. They are often used to store configuration settings and sensitive information like API keys, keeping them separate from the codebase.

1.  **Access Scrimba Environment Settings:** In your Scrimba lesson, click on the "wheel" icon located at the bottom right corner.
2.  **Edit Environment Variables:** From the menu, select "Edit environment."
3.  **Create a New Key-Value Pair:** Click on "New key."
4.  **Enter Key Name:** In the first field (Key), enter `ANTHROPIC_API_KEY` (all caps).
5.  **Paste API Key Value:** In the second field (Value), paste the Anthropic API key you copied earlier.
6.  **Save Changes:** Click "Save" and then click outside the settings panel to close it.

Now, your Anthropic API key is securely stored as an environment variable within Scrimba. Your code can access it using `process.env.ANTHROPIC_API_KEY`.

## Integrating Claude with the Text Summarizer: AI-Specific Code

With the API key set up, we can now add the AI-specific code to our text summarizer to communicate with Claude.

### Adding the Anthropic SDK Dependency: Challenge

**Challenge:** Add the Anthropic AI SDK (Software Development Kit) as a dependency to your Scrimba project. Use version `0.243` of `@anthropic-ai/sdk`.

> **SDK (Software Development Kit)**: A collection of software development tools in one installable package.  For AI, an SDK often includes libraries and tools to easily interact with an AI model's API.
> **Dependency**:  An external library or package that your project relies on to function. In JavaScript projects, dependencies are managed using package managers like npm or yarn.

**Solution:**

1.  In Scrimba, click the "+" icon next to "Dependencies."
2.  Enter `@anthropic-ai/sdk` in the search bar.
3.  Select version `0.243` from the dropdown list.
4.  Click to add the dependency.

### Importing and Instantiating the Anthropic SDK

After adding the dependency, import the Anthropic SDK into your `index.js` file:

```javascript
import Anthropic from '@anthropic-ai/sdk';
```

Next, create an instance of the Anthropic client. This instance will be our entry point to interact with Claude's **Messages API**.

```javascript
const anthropic = new Anthropic({
    apiKey: process.env.ANTHROPIC_API_KEY,
    baseURL: 'https://api.proxy. Acrimba.com/v1' // Required for Scrimba environment
});
```

> **Instance**: In object-oriented programming, an instance is a specific realization of an object or class. Here, `anthropic` is an instance of the `Anthropic` class, configured with your API key and base URL.

**Note on `baseURL`:** The `baseURL` is set to `'https://api.proxy.scrimba.com/v1'` specifically for the Scrimba environment. Scrimba provides a proxy to handle API requests during development. This `baseURL` is not needed when deploying to a production environment outside of Scrimba.

### Retrieving Text Input: Challenge

**Challenge:** Inside the `summarize` function, retrieve the text from the text input area and store it in a variable named `text`.

**Solution:**

```javascript
function summarize() {
    startLoading();

    const text = textInputArea.value; // Get text from input area
    // ... rest of the Claude API call will be added next ...
}
```

### Calling the Claude Messages API

Now we will write the core code to interact with Claude using the **Messages API**. This code will be placed within the `summarize` function, after retrieving the input text.

```javascript
async function summarize() { // Mark function as async
    startLoading();

    const text = textInputArea.value;

    const response = await anthropic.messages.create({ // Use await for asynchronous call
        model: 'claude-3.5-sonnet', // Specify the model
        max_tokens: 300, // Set maximum tokens for the response
        system_prompt: 'You are a text summarizer. When asked to summarize a text, send back the summary.', // System prompt for Claude
        messages: [ // Array of messages
            {
                role: 'user', // User role for the message
                content: [ // Content of the message (array of content blocks)
                    {
                        type: 'text', // Content type is text
                        text: `Summarize this text: ${text}` // User prompt to Claude, using template literal
                    }
                ]
            }
        ]
    });

    endLoading(); // Stop loading spinner
    console.log(response); // Log the API response
    // ... display summary in UI will be added next ...
}
```

> **Promise**:  In JavaScript, a Promise is an object representing the eventual outcome of an asynchronous operation. It can be in one of three states: pending, fulfilled, or rejected.
> **Async/Await**: Keywords in JavaScript used to handle asynchronous operations in a more synchronous-looking way. `async` marks a function as asynchronous, and `await` pauses the execution of an `async` function until a Promise is resolved.
> **Template Literal**:  A feature in JavaScript (using backticks `` ` ``) that allows for string interpolation, embedding variables directly within strings using `${variableName}`.
> **String Interpolation**:  The process of embedding variables or expressions within a string.

**Explanation of the Claude API call:**

*   **`async function summarize() { ... }`**:  The `summarize` function is declared as `async` because we are making an asynchronous API call using `await`.
*   **`await anthropic.messages.create({ ... })`**:  This is the core API call.
    *   `anthropic.messages.create`:  Calls the `create` function of the `messages` API from the `anthropic` instance.
    *   `await`:  Pauses the function execution until the `create` promise resolves (i.e., we receive a response from Claude).
    *   **`model: 'claude-3.5-sonnet'`**: Specifies the Claude model to use.
    *   **`max_tokens: 300`**:  Sets the maximum number of tokens (roughly words or parts of words) Claude can use in its response. 300 is chosen to be sufficient for summaries of 1-100 words.
    *   **`system_prompt: '...'`**:  Provides instructions to Claude on its role and behavior. Here, we instruct it to act as a text summarizer.
    *   **`messages: [...]`**:  An array of messages representing the conversation history. In this case, we are sending a single user message.
        *   **`role: 'user'`**:  Indicates the role of the message sender (user).
        *   **`content: [...]`**:  An array of content blocks within the message.
            *   **`type: 'text'`**: Specifies the content type as text.
            *   **`text: \`Summarize this text: ${text}\``**:  The actual user prompt, asking Claude to summarize the input `text`. A template literal is used to embed the `text` variable into the prompt.

*   **`endLoading();`**:  Hides the loading spinner after receiving the response.
*   **`console.log(response);`**:  Logs the full API response to the console for inspection.

### Displaying the Summary in the UI: Challenge

**Challenge:**  Extract the summary text from the `response` object and display it in the `summaryOutputArea` text area.

**Solution:**

After examining the `console.log(response)` output, we observe that the summary text is located within:

`response.content[0].text`

Modify the `summarize` function to display the summary:

```javascript
async function summarize() {
    // ... (previous code) ...

    summaryOutputArea.value = response.content[0].text; // Display summary in UI

    endLoading();
    // console.log(response); // Comment out console log after verifying response structure
}
```

Now, when you paste text into the input area and click "Summarize," the application should send the text to Claude, receive a summary, and display it in the output text area!

### Rewriting the Claude API Call: Challenge

**Challenge:**  Rewrite the Claude API call code from scratch, based on your understanding of the `messages API` and the required fields. Try to replicate the functionality of the provided code without copying and pasting. This exercise reinforces your understanding of the AI-specific code.

This challenge encourages active learning and solidifies your grasp of how to interact with Claude's API programmatically.

## Improving the Text Summarizer with Prompt Engineering

Our text summarizer now works, but the initial summaries might not be perfect. We can refine Claude's output using **prompt engineering**.

> **Prompt Engineering**: The process of designing and refining prompts (instructions or questions given to an AI model) to elicit desired and high-quality responses. It involves understanding how the model interprets prompts and crafting them effectively to achieve specific outcomes.

### Refining the Summary Format with System Prompt Engineering: Challenge

**Issue:** The current summary format from Claude might include prefixes like "Summary:" or indicate the source of the text, which is not ideal. We want just the summary text itself, presented as if written by the original author.

**Challenge:** Rewrite the `system_prompt` to improve the summary format.

**Solution:**  Create a more specific and directive `system_prompt`.

```javascript
const response = await anthropic.messages.create({
    model: 'claude-3.5-sonnet',
    max_tokens: 300,
    system_prompt: `You are a text summarizer. When asked to summarize a text, send back the summary of it.
    Please only send back the summary without prefixing it with things like "Summary:" or telling where the text is from.
    Also, give me the summary as if the original author wrote it, and without using a third-person voice.`, // Improved system prompt
    messages: [
        {
            role: 'user',
            content: [
                {
                    type: 'text',
                    text: `Summarize this text: ${text}`
                }
            ]
        }
    ]
});
```

**Explanation of the improved system prompt:**

*   **Specificity:** The prompt is more specific about the desired output format, explicitly stating what to avoid (prefixes, source indication) and what to include (author's voice, no third-person perspective).
*   **Examples (Implicit):**  While not explicit examples in the prompt, the instructions implicitly provide examples of what *not* to do, guiding Claude towards the desired format.

By rewriting the `system_prompt` with these specific instructions, we can guide Claude to generate summaries that are cleaner, more concise, and better aligned with the desired output.

### Controlling Summary Length with User Prompt Engineering: Challenge

**Issue:** The summary length is currently fixed. We want to allow users to control the desired summary length using the slider input.

**Challenge:** Modify the **user prompt** to incorporate the desired summary length from the `summaryLengthInput` slider.

**Solution:**

1.  **Retrieve Summary Length Value:**  In the `summarize` function, get the value from the `summaryLengthInput` element.

    ```javascript
    const summaryLength = summaryLengthInput.value;
    ```

2.  **Modify User Prompt:**  Update the `text` content within the `messages` array to include the desired summary length using string interpolation.

    ```javascript
    messages: [
        {
            role: 'user',
            content: [
                {
                    type: 'text',
                    text: `Summarize this text. Limit the length to ${summaryLength} words.` // User prompt with dynamic length
                }
            ]
        }
    ]
    ```

Now, the user prompt dynamically includes the desired summary length, enabling users to control the conciseness of the generated summaries. This demonstrates how **user prompt engineering** can be used to make the application more interactive and user-centric.

## Error Handling in the Text Summarizer

Robust applications must handle errors gracefully. Let's implement error handling in our text summarizer.

### Implementing Try-Catch Error Handling: Challenge

**Challenge:**  Implement error handling using a `try...catch` block within the `summarize` function to catch potential errors during the API call to Claude. Pass any caught error to the `handleError` function (already provided in the code).

> **Error Handling**: The process of anticipating, detecting, and resolving errors that may occur during program execution.  Robust error handling prevents application crashes and provides informative feedback to the user.
> **Try-Catch Statement**: A fundamental error handling construct in JavaScript (and many other languages). Code that might throw an error is placed within the `try` block, and code to handle the error is placed within the `catch` block.

**Solution:**

Wrap the entire content of the `summarize` function (from `startLoading()` to setting `summaryOutputArea.value`) within a `try...catch` block.

```javascript
async function summarize() {
    try { // Try block starts here
        startLoading();

        const text = textInputArea.value;
        const summaryLength = summaryLengthInput.value;

        const response = await anthropic.messages.create({
            model: 'claude-3.5-sonnet',
            max_tokens: 300,
            system_prompt: `You are a text summarizer. ... (rest of system prompt)`,
            messages: [
                {
                    role: 'user',
                    content: [
                        {
                            type: 'text',
                            text: `Summarize this text. Limit the length to ${summaryLength} words.`
                        }
                    ]
                }
            ]
        });

        summaryOutputArea.value = response.content[0].text;

        endLoading();

        summaryOutputArea.disabled = false; // Enable summary output area
        copyButton.disabled = false; // Enable copy button
        copyButton.focus(); // Focus on copy button

    } catch (error) { // Catch block starts here
        handleError(error); // Pass error to handleError function
    }
}
```

**Testing Error Handling:**

To test error handling, intentionally introduce an error, such as commenting out the `max_tokens` field in the API call (as `max_tokens` is a required field). Run the application and click "Summarize." You should now see the error handling in action, displaying an error message in the UI via the `handleError` function instead of the application crashing.

After testing, remember to uncomment the `max_tokens` field to restore the correct functionality.

### Finalizing Text Summarizer Functionality

To complete the text summarizer, add the following lines within the `try` block, after setting `summaryOutputArea.value` and before `endLoading()`:

```javascript
summaryOutputArea.disabled = false; // Enable summary output area for editing
copyButton.disabled = false; // Enable the copy button
copyButton.focus(); // Set focus to the copy button
```

These lines enhance the user experience by:

*   Enabling the summary output area for users to edit the summary if desired.
*   Enabling the "Copy" button to allow users to copy the generated summary to their clipboard.
*   Setting focus to the "Copy" button, making it immediately accessible after summarization.

With these enhancements, the text summarizer application is now fully functional, robust (due to error handling), and user-friendly.

## Deploying the Text Summarizer to Production with Cloudflare

Congratulations on building your first AI-powered application! Now, let's make it accessible to users worldwide by deploying it to production using Cloudflare.

> **Deployment**: The process of making an application or software system available for use in a live, production environment. It typically involves configuring servers, setting up infrastructure, and transferring the application code to the production environment.
> **Cloudflare**: A web infrastructure and security company that provides services like CDN (Content Delivery Network), DDoS protection, DNS management, and serverless computing.

**Note:** Deployment to Cloudflare is considered an advanced topic. If you are a beginner, you may choose to skip this section and return to it later. Scrimba offers a dedicated course on deploying AI-powered applications to Cloudflare for more in-depth learning.

### Overview of Deployment Steps

Deploying our text summarizer to Cloudflare involves these key steps:

1.  **Cloudflare Account Setup:** Create a free Cloudflare account and log in.
2.  **Understanding the System Design Shift:** We need to transition from Scrimba's proxy back end to a real back end hosted on Cloudflare.
3.  **Creating a Cloudflare Worker:**  Set up a Cloudflare Worker to act as our back end. Cloudflare Workers are serverless functions that run on Cloudflare's edge network.
4.  **Migrating Back-End Code to the Worker:** Move the Claude API interaction code from our front-end JavaScript to the Cloudflare Worker.
5.  **Deploying the Worker:** Deploy the Cloudflare Worker to Cloudflare's infrastructure.
6.  **Updating Front-End to Communicate with Worker:** Modify the front-end JavaScript to send requests to the deployed Cloudflare Worker URL instead of relying on Scrimba's proxy.
7.  **Deploying the Front End with Cloudflare Pages:** Deploy the front-end HTML, CSS, and JavaScript files using Cloudflare Pages, a service for hosting static websites.

> **Cloudflare Workers**: A serverless execution environment that allows you to run JavaScript, WebAssembly, and other code directly on Cloudflare's global network. Workers are ideal for building fast, scalable, and globally distributed applications.
> **Proxy**: A server that acts as an intermediary for requests from clients seeking resources from other servers. In our case, Scrimba's proxy was acting as a back end for development.
> **CORS (Cross-Origin Resource Sharing)**: A browser security mechanism that restricts web pages from making requests to a different domain than the one that served the web page. CORS needs to be properly configured when front end and back end are hosted on different domains.

### Creating a Cloudflare Worker

1.  **Open Terminal and Navigate to Project Directory:** Open your terminal and navigate to the directory where you want to create your back-end project.
2.  **Run Cloudflare Worker Creation Command:** Execute the following command:

    ```bash
    npm create cloudflare@latest worker-summarizer-backend
    ```

    Replace `worker-summarizer-backend` with your desired project name.
3.  **Follow Prompts:**  The command will prompt you for configuration options. Choose JavaScript as the programming language and accept the default options for the rest. This will create a "Hello World" worker project and deploy it to Cloudflare.
4.  **Copy Worker URL:** After successful deployment, a browser tab will open, displaying your deployed worker with a new URL. **Copy and securely store this URL.** You will need it later to connect your front end to this back end.
5.  **Navigate into Worker Project Directory:**  In your terminal, navigate into the newly created worker project directory:

    ```bash
    cd worker-summarizer-backend
    ```

### Migrating Back-End Code to the Cloudflare Worker

1.  **Replace `src/index.js` Content:**  Open the `src/index.js` file in your worker project. Replace its existing content with the following code:

    ```javascript
    import Anthropic from "@anthropic-ai/sdk";

    const corsHeaders = {
        'Access-Control-Allow-Origin': '*', // Allow requests from any origin (for simplicity in this tutorial, consider restricting in production)
        'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
        'Access-Control-Allow-Headers': 'Content-Type',
    };

    export default {
        async fetch(request, env, ctx) {
            if (request.method === 'OPTIONS') { // Handle CORS preflight requests
                return new Response('OK', { headers: corsHeaders });
            }

            try {
                const anthropic = new Anthropic({
                    apiKey: env.ANTHROPIC_API_KEY, // API key from environment variable
                });

                const { messages, max_tokens, model, system_prompt } = await request.json(); // Extract data from request body

                const response = await anthropic.messages.create({
                    model: model || 'claude-3.5-sonnet', // Use provided model or default
                    max_tokens: max_tokens || 300, // Use provided max_tokens or default
                    system_prompt: system_prompt,
                    messages: messages,
                });

                return new Response(JSON.stringify(response), { // Respond with summary
                    headers: { ...corsHeaders, 'Content-Type': 'application/json' },
                    status: 200,
                });

            } catch (error) {
                console.error("Error processing request:", error);
                return new Response(JSON.stringify({ error: error.message }), { // Respond with error
                    headers: { ...corsHeaders, 'Content-Type': 'application/json' },
                    status: 400, // Or appropriate error status code
                });
            }
        },
    };
    ```

    **Explanation of Worker Code:**

    *   **`import Anthropic from "@anthropic-ai/sdk";`**: Imports the Anthropic SDK.
    *   **`corsHeaders`**: Defines headers to handle **CORS**.  For this tutorial, it allows requests from any origin (`'*'`). In production, restrict this to your front-end domain for security.
    *   **`export default { fetch: async (request, env, ctx) => { ... } }`**:  Defines the worker's `fetch` handler function, which is executed for every incoming request.
        *   **`request`**: The incoming HTTP request object.
        *   **`env`**:  Environment variables available to the worker.
        *   **`ctx`**:  Context object for worker execution.
        *   **`if (request.method === 'OPTIONS') { ... }`**: Handles CORS preflight requests (OPTIONS method).
        *   **`const anthropic = new Anthropic({ apiKey: env.ANTHROPIC_API_KEY });`**:  Creates an Anthropic client instance, retrieving the API key from the `env` (environment variables).
        *   **`const { messages, max_tokens, model, system_prompt } = await request.json();`**: Parses the request body (assumed to be JSON) to extract parameters for the Claude API call.
        *   **`const response = await anthropic.messages.create({ ... });`**:  Makes the Claude API call, using parameters from the request.
        *   **`return new Response(JSON.stringify(response), { ... });`**: Sends the Claude API response back to the client as JSON, including CORS headers.
        *   **`catch (error) { ... }`**:  Error handling block to catch and respond to errors.

2.  **Install Anthropic SDK Dependency in Worker Project:**  In your terminal, within the worker project directory, run:

    ```bash
    npm install @anthropic-ai/sdk@0.243
    ```

3.  **Set Anthropic API Key as Worker Secret:**  Run the following command to securely store your Anthropic API key as a secret environment variable in your Cloudflare Worker:

    ```bash
    npx wrangler secret put ANTHROPIC_API_KEY
    ```

    When prompted, paste your Anthropic API key value.

### Deploying the Cloudflare Worker

In your terminal, within the worker project directory, run the deployment command:

```bash
npm run deploy
```

This command will deploy your Cloudflare Worker to Cloudflare's network.

### Updating Front-End Code to Use the Cloudflare Worker

1.  **Remove Anthropic SDK Dependency from Front-End:** In your Scrimba project's `index.js`, remove the line:

    ```javascript
    import Anthropic from '@anthropic-ai/sdk';
    ```

    Also, remove the Anthropic SDK dependency from your Scrimba project's dependencies list.

2.  **Remove Anthropic Instance Creation:**  Remove the code that creates the Anthropic client instance:

    ```javascript
    const anthropic = new Anthropic({
        apiKey: process.env.ANTHROPIC_API_KEY,
        baseURL: 'https://api.proxy.scrimba.com/v1'
    });
    ```

3.  **Define Worker URL in Front-End:**  In your Scrimba `index.js`, at the top, define a constant `workerURL` and set it to the URL of your deployed Cloudflare Worker (the URL you copied earlier):

    ```javascript
    const workerURL = 'YOUR_CLOUDFLARE_WORKER_URL'; // Replace with your worker URL
    ```

4.  **Modify `summarize` Function to Fetch from Worker:** Update the `summarize` function to use the `fetch` API to send a POST request to your Cloudflare Worker URL, instead of directly calling the Anthropic SDK.

    ```javascript
    async function summarize() {
        try {
            startLoading();

            const text = textInputArea.value;
            const summaryLength = summaryLengthInput.value;

            const messages = [{ // Prepare messages payload for worker
                role: 'user',
                content: [{ type: 'text', text: `Summarize this text. Limit the length to ${summaryLength} words.` }]
            }];

            const options = { // Fetch options for POST request to worker
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ // Send data to worker in request body
                    messages: messages,
                    max_tokens: 300,
                    model: 'claude-3.5-sonnet',
                    system_prompt: `You are a text summarizer. ... (rest of system prompt)` // System prompt remains in front end for simplicity, could be moved to worker as well
                })
            };

            const response = await fetch(workerURL, options); // Fetch from Cloudflare Worker
            if (!response.ok) {
                const message = `Error: ${response.status}`;
                throw new Error(message);
            }
            const responseData = await response.json(); // Parse JSON response from worker

            summaryOutputArea.value = responseData.content[0].text; // Extract summary from response

            endLoading();
            summaryOutputArea.disabled = false;
            copyButton.disabled = false;
            copyButton.focus();

        } catch (error) {
            handleError(error);
        }
    }
    ```

    **Explanation of Front-End Fetch Changes:**

    *   **`const workerURL = 'YOUR_CLOUDFLARE_WORKER_URL';`**:  Uses the worker URL you defined.
    *   **`const options = { ... };`**:  Sets up `fetch` options for a POST request:
        *   `method: 'POST'`:  Specifies the POST method.
        *   `headers: { 'Content-Type': 'application/json' }`: Sets the content type to JSON.
        *   `body: JSON.stringify({ ... })`:  Stringifies the data to be sent in the request body, including `messages`, `max_tokens`, `model`, and `system_prompt`.
    *   **`const response = await fetch(workerURL, options);`**:  Makes the `fetch` call to your Cloudflare Worker URL, sending the options.
    *   **Error Handling in `fetch`:** Checks if the `response.ok` is true (status code 200-299). If not, throws an error.
    *   **`const responseData = await response.json();`**: Parses the JSON response from the worker.
    *   **`summaryOutputArea.value = responseData.content[0].text;`**: Extracts the summary from the parsed JSON response.

Now, your front-end code communicates with your deployed Cloudflare Worker back end to perform text summarization using Claude.

### Deploying the Front End with Cloudflare Pages

For the final step, deploy your front-end files (HTML, CSS, JavaScript, images) using Cloudflare Pages. Follow Scrimba's provided resources or Cloudflare Pages documentation to learn how to deploy a static website to Cloudflare Pages.

> **Cloudflare Pages**: A platform for deploying static websites and frontend applications directly from your Git repository to Cloudflare's global network.

Once both the Cloudflare Worker (back end) and Cloudflare Pages (front end) are deployed, your text summarizer application will be live and accessible on the internet!

## Building an Image Describer with Claude

Let's move on to our second project: building an image describer application. Meet Daisy, an AI-generated cat character who loves describing images. Inspired by Daisy, we will create an AI-powered image describer as a fun application.

### Functionality of the Image Describer

The image describer will function as follows:

1.  **Image Input:** Users can input an image in two ways:
    *   **Drag and Drop:** Drag an image file and drop it into a designated area.
    *   **Upload File:** Click an icon to upload an image file from their computer.
2.  **Description Length Adjustment:** Users can adjust the desired description length using a slider (default 10 words).
3.  **Description Generation:** Upon clicking a "Describe" button, the image data is sent to Claude for processing.
4.  **Description Display:** The generated image description is displayed in a text area.
5.  **Copy and Clear:** Users can copy the description and clear the interface to start over.

### System Design (Similar to Text Summarizer)

The system design for the image describer is very similar to the text summarizer:

*   **Front End:**  UI for image input, description length adjustment, and displaying the description.
*   **Back End:**  Handles communication between the front end and Claude (we will reuse the Cloudflare Worker we created for the text summarizer or adapt it).
*   **Claude:** Anthropic's AI model processes the image data and generates a description.

The data flow is analogous to the text summarizer, but now involves image data instead of text data.

### User Interface (UI) Review

The UI for the image describer is also pre-built, similar to the text summarizer. Key elements include:

*   **Drag and Drop Area/Upload Icon:** For image input.
*   **Slider:** For description length adjustment.
*   **"Describe" Button.**
*   **Text Area:** To display the generated image description.
*   **"Copy" and "Clear" Buttons.**

The code structure is similar to the text summarizer project, with `index.html`, `index.css`, and `index.js` files.

### `fetchImageAndReturnBase64ImageData` Utility Function

A utility function, `fetchImageAndReturnBase64ImageData`, is provided in a `utilities/utilities.js` file and imported into `index.js`.

```javascript
// utilities/utilities.js
export async function fetchImageAndReturnBase64ImageData(imageURL) {
    const response = await fetch(imageURL);
    const blob = await response.blob();
    return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onloadend = () => resolve(reader.result.split(',')[1]); // Extract base64 data part
        reader.onerror = reject;
        reader.readAsDataURL(blob);
    });
}
```

> **Base64 Image Data**: A way to represent binary image data as a string of ASCII characters. It is commonly used to embed images directly within HTML or other text-based formats.
> **Blob (Binary Large Object)**: A data type that can store binary data, such as images or audio files.
> **File Reader**: A JavaScript object that allows web applications to asynchronously read the contents of files (or raw data buffers) stored on the user's computer.
> **Utility Function**: A reusable function designed to perform a specific, often common, task.

**Functionality of `fetchImageAndReturnBase64ImageData`:**

1.  **Fetches Image:** Takes an `imageURL` as input and fetches the image file using the `fetch` API.
2.  **Converts to Blob:** Converts the fetched image response to a Blob (binary data).
3.  **Reads as Data URL (Base64):** Uses `FileReader` to read the Blob as a data URL, which is a string containing the base64 encoded image data.
4.  **Extracts Base64 Data:** Extracts only the base64 data part from the data URL string (removes the `data:image/png;base64,` prefix).
5.  **Returns Base64 Data:** Returns the extracted base64 encoded image data as a string.

This utility function will be used to convert image files into base64 data format, which can be sent to Claude for image analysis.

### Initial `describe` Function Placeholder

The `describe` function in `index.js` currently has placeholder code:

```javascript
async function describe() {
    startLoading();
    const base64ImageData = await fetchImageAndReturnBase64ImageData(imageURL);
    // ... rest of the describe logic will be added in the next lesson ...
}
```

It starts the loading spinner and calls `fetchImageAndReturnBase64ImageData` to get base64 image data for a default `imageURL`. We will expand this function in the next section to integrate Claude's image description capabilities.

## Integrating Claude for Image Description: AI-Specific Code

Now we will add the AI-specific code to the image describer to communicate with Claude and generate image descriptions.

### Implementing Claude Image Description: Super Challenge

**Super Challenge:** Add all necessary code to the `describe` function in `index.js` to:

1.  Talk to Claude's **Messages API** to request an image description.
2.  Determine appropriate **system and user prompts** for image description.
3.  Send the **base64 image data** to Claude as part of the API request.
4.  Display the generated **image description** in the UI.

This is a comprehensive challenge that tests your understanding of how to interact with Claude's API for image processing.

**Solution:**

```javascript
async function describe() {
    try {
        startLoading();

        const descriptionLength = descriptionLengthInput.value;

        const response = await anthropic.messages.create({
            model: 'claude-3.5-sonnet',
            max_tokens: 300,
            system_prompt: 'You are an image describer. When asked to describe an image, provide a concise and informative description.',
            messages: [
                {
                    role: 'user',
                    content: [
                        {
                            type: 'text',
                            text: `Describe this image. Limit the description to ${descriptionLength} words.`
                        },
                        {
                            type: 'image',
                            source: {
                                type: 'base64',
                                media_type: imageType, // e.g., 'image/png'
                                data: base64ImageData // Base64 image data obtained from fetchImageAndReturnBase64ImageData
                            }
                        }
                    ]
                }
            ]
        });

        descriptionOutputArea.value = response.content[0].text;

        endLoading();
        descriptionOutputArea.disabled = false;
        copyButton.disabled = false;
        copyButton.focus();

    } catch (error) {
        handleError(error);
    }
}
```

**Explanation of the Image Description Code:**

*   **`system_prompt: 'You are an image describer. ...'`**: Sets Claude's role as an image describer in the system prompt.
*   **`messages: [...]`**:  The `messages` array now contains two content blocks within the user message:
    *   **Text Content:**
        ```javascript
        {
            type: 'text',
            text: `Describe this image. Limit the description to ${descriptionLength} words.`
        }
        ```
        This is the user prompt asking Claude to describe the image and setting the desired description length.
    *   **Image Content:**
        ```javascript
        {
            type: 'image',
            source: {
                type: 'base64',
                media_type: imageType, // e.g., 'image/png'
                data: base64ImageData
            }
        }
        ```
        This is the crucial part for image processing. It sends the base64 encoded image data to Claude.
        *   **`type: 'image'`**: Specifies the content type as image.
        *   **`source: { ... }`**:  Defines the image source.
            *   **`type: 'base64'`**: Indicates that the image data is in base64 format.
            *   **`media_type: imageType`**:  Specifies the image file type (e.g., 'image/png', 'image/jpeg'). The `imageType` variable should be set correctly when handling image uploads or drag-and-drop events in your code.
            *   **`data: base64ImageData`**:  The actual base64 encoded image data string.

*   **`descriptionOutputArea.value = response.content[0].text;`**:  Displays the generated image description in the `descriptionOutputArea`.

### Error Handling: Challenge

**Challenge:** Implement error handling using a `try...catch` block in the `describe` function, similar to the text summarizer, to gracefully handle any errors during the Claude API call.

**Solution:**  The `try...catch` block is already included in the provided `describe` function solution above. Ensure you have wrapped the Claude API call and related code within the `try` block and are calling `handleError(error)` in the `catch` block.

### Debugging and Fixing Errors: Challenge

**Challenge:** If you encounter an error when running the image describer (e.g., a 400 error message indicating "Max tokens field required"), debug the code to identify and fix the error.

> **Debugging**: The process of identifying and removing errors (bugs) from software code.

**Solution:** Carefully examine the error message and your code. In the example error message "Max tokens field required," the issue might be a typo in the `max_tokens` field name in your API call (e.g., writing `max_token` instead of `max_tokens`). Correcting such typos is a common debugging task.

> **Typo**: A typographical error, a mistake made in typing.

### Prompt Engineering for Description Length: Challenge

**Challenge:** Practice prompt engineering to adjust the length of the image description. Modify the **user prompt** to dynamically control the description length using the `descriptionLengthInput` slider value.

**Solution:** The user prompt in the provided `describe` function solution already includes dynamic description length control:

```javascript
text: `Describe this image. Limit the description to ${descriptionLength} words.`
```

Ensure that you have correctly implemented this dynamic length in your user prompt and are retrieving the `descriptionLength` value from the `descriptionLengthInput` element in your `describe` function.

### Finalizing Image Describer Functionality

To complete the image describer functionality, add the following lines within the `try` block, after setting `descriptionOutputArea.value` and before `endLoading()`:

```javascript
descriptionOutputArea.disabled = false; // Enable description output area for editing
copyButton.disabled = false; // Enable copy button
copyButton.focus(); // Focus on copy button
```

These lines make the description output area editable, enable the "Copy" button, and set focus to the "Copy" button, enhancing the user experience, just as we did for the text summarizer.

With all these components in place, you have now built a fully functional AI-powered image describer application using Claude!

## Conclusion: Becoming a More Powerful Developer with AI

Congratulations! You have successfully completed this journey of building AI-powered applications with Claude. By building both a text summarizer and an image describer, you have gained practical skills and a solid understanding of how to harness the power of large language models for real-world applications.

### Course Recap: Key Learnings and Achievements

Throughout this course, you have:

*   **Built a Text Summarizer with Claude:**  Learned to process text data using Claude's **Messages API** and create a useful application.
*   **Mastered Prompt Engineering:**  Developed skills in crafting effective **system and user prompts** to control and refine Claude's output.
*   **Implemented Error Handling:**  Learned to use `try...catch` blocks to create robust and user-friendly applications.
*   **Explored AI Application Deployment:**  Gained an introduction to deploying AI-powered applications to production using **Cloudflare**.
*   **Built an Image Describer with Claude:** Extended your skills to process **image data** using Claude's **Messages API**, creating a new type of AI application.
*   **Utilized Scrimba Templates:**  Discovered the efficiency of using Scrimba templates for rapid development.

By completing these projects and challenges, you have significantly enhanced your capabilities as a developer and taken a crucial step towards becoming an AI-empowered developer.

Keep coding, keep learning, and continue to explore the exciting world of AI! Sam and Daisy wish you the best in your future endeavors.
