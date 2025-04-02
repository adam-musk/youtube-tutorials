---
layout: "../../layouts/BlogPost.astro"
title: "Building a RAG Chatbot with Your Data: A Practical Guide for JavaScript Developers"
description: ""
pubDate: "2025-02-27"
youtubeVideoID: "d-VKYF4Zow0"
channel: ""
index: 28
---

# Building a RAG Chatbot with Your Data: A Practical Guide for JavaScript Developers

> 



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/d-VKYF4Zow0" frameborder="0" allowfullscreen></iframe>


## Introduction to Generative AI and RAG Chatbots

Welcome to the exciting world of Generative AI for JavaScript developers! This chapter will guide you through the process of building and deploying your very own Retrieval-Augmented Generation (RAG) chatbot.  You will learn how to create a chatbot that is not limited by the knowledge cut-off dates of standard models like ChatGPT, but instead, is powered by data you provide, ensuring up-to-date and relevant answers.

This chapter is perfect for beginners who want to understand core AI concepts like RAG chatbots and vector embeddings, and gain practical experience with technologies such as Langchain JS, Next.js, Vercel, and OpenAI.

> **Chatbot:** A computer program designed to simulate conversation with human users, especially over the internet. Chatbots can understand and respond to user queries, providing information, assistance, or engaging in dialogue.

> **Generative AI:** A type of artificial intelligence that focuses on creating new content, such as text, images, or code, rather than simply analyzing or acting on existing data. Generative AI models learn patterns from training data and use these patterns to generate novel outputs.

### What You Will Learn

By the end of this chapter, you will:

*   Understand the fundamentals of AI development in JavaScript.
*   Build a functional RAG chatbot capable of answering questions based on current data.
*   Learn how to scrape data from the internet to keep your chatbot up-to-date.
*   Implement vector embeddings to efficiently store and retrieve information.
*   Utilize Langchain JS, Next.js, Vercel, and OpenAI in a practical project.
*   Understand the cost-effectiveness of RAG chatbots compared to retraining large language models.

## Understanding the Power of RAG: Retrieval-Augmented Generation

### The Knowledge Cut-off Challenge

One of the limitations of even advanced chatbots like ChatGPT is their **knowledge cut-off date**.

> **Knowledge cut-off date:** The point in time after which a language model's training data ceases to include new information.  This means the model's knowledge is limited to events and data available up to this date.

As of September 2021, ChatGPT's training data collection ceased, meaning it lacks awareness of events and information that emerged after this date.  This limitation can be a significant drawback when you need a chatbot to provide answers based on the most current information.

### RAG to the Rescue: Bridging the Knowledge Gap

**Retriever Augmented Generation (RAG)** offers a powerful solution to this problem.

> **Retriever Augmented Generation (RAG):** A technique that enhances the output of a Large Language Model (LLM) by providing it with additional context relevant to the user's query. This allows the model to generate more accurate and up-to-date answers by leveraging both its pre-existing knowledge and the newly provided information.

> **Large Language Model (LLM):** A sophisticated type of artificial intelligence model trained on massive datasets of text and code. LLMs are capable of understanding and generating human-like text for a wide range of tasks, including question answering, text completion, and language translation.

Instead of relying solely on the LLM's pre-existing knowledge, RAG empowers the model to access and incorporate external data in real-time.

**How RAG Works (Simplified):**

*   **User Query:** A user asks a question to the chatbot.
*   **Data Retrieval:** The RAG system retrieves relevant information from an external data source (e.g., the internet, a private database) based on the user's query.
*   **Context Augmentation:** This retrieved information is added as context to the original user query.
*   **Generation with Context:** The LLM uses both its internal knowledge and the augmented context to generate a more informed and accurate response.

### Benefits of Using RAG

*   **Up-to-Date Answers:** RAG chatbots can provide answers based on the latest information by dynamically retrieving data from external sources, overcoming the knowledge cut-off limitation.
*   **Cost-Effectiveness:** Retraining a foundation model is computationally and financially expensive. RAG offers a cost-effective alternative by augmenting existing models with new data without requiring retraining.

    > **Foundation Model:** A large, pre-trained AI model that is trained on a broad spectrum of data and serves as the base for more specialized models or applications. Foundation models can be adapted or fine-tuned for specific tasks, but in their original form, they possess general knowledge.

*   **Access to Private Data:** RAG can incorporate data that is not publicly available or part of the LLM's training dataset, such as information from your personal documents or internal company databases. This allows for highly customized and private chatbot applications.

**Example: Formula 1 Chatbot**

Imagine you want to build a chatbot that answers questions about Formula 1 racing. With RAG, you can:

1.  **Scrape up-to-date data:**  Collect the latest Formula 1 news, standings, and driver information from websites.
2.  **Feed data to the chatbot:**  Use RAG to provide this scraped data as context when a user asks a question.
3.  **Get current answers:** The chatbot can then answer questions like "Who is the current Formula 1 World Drivers' Champion?" with the most recent information, even if it's beyond ChatGPT's 2021 knowledge cut-off.

## Course Prerequisites and Technologies

Before diving into building your RAG chatbot, let's review the prerequisites and technologies you will be using in this course.

### Prerequisites

*   **Basic understanding of AI concepts:** Familiarity with concepts like chatbots and AI is helpful but not strictly required. This chapter will explain the necessary concepts as we progress.
*   **Latest version of Node.js:** Ensure you have Node.js installed and updated to the latest version. Node.js is a JavaScript runtime environment that allows you to run JavaScript code outside of a web browser.

    > **Node.js:** An open-source, cross-platform JavaScript runtime environment that executes JavaScript code server-side. Node.js enables developers to use JavaScript for backend development, creating dynamic web pages and applications.

*   **OpenAI Account:** You will need an account with OpenAI to access their APIs, which are essential for leveraging powerful language models and embedding capabilities.
*   **Knowledge of Next.js (Beneficial):** While step-by-step instructions will be provided, a basic understanding of Next.js, a React framework for web development, will be advantageous.

    > **Next.js:** An open-source React framework that enables server-side rendering and the creation of full-stack web applications. Next.js simplifies web development with features like routing, API routes, and optimized performance.

### Key Technologies

*   **Langchain JS:** A JavaScript library designed to simplify the development of applications powered by language models. Langchain provides tools and abstractions for building complex LLM-based applications, including RAG systems.

    > **Langchain JS:** A framework for building applications using language models. It provides modules for model integration, prompt management, chains of operations, data augmentation, and agents, making it easier to develop sophisticated AI-powered applications.

*   **Next.js:** As mentioned, Next.js will be used to build the user interface and structure of your chatbot application.
*   **Vercel:** A cloud platform optimized for deploying frontend applications, particularly Next.js applications. Vercel offers easy deployment and hosting solutions.

    > **Vercel:** A cloud platform for frontend developers that provides serverless functions, global CDN, and automatic scaling. Vercel is popular for deploying modern web applications, especially those built with frameworks like Next.js.

*   **OpenAI:** You will utilize OpenAI's APIs for:
    *   **Large Language Models (LLMs):** Specifically, models like GPT-4 for generating human-like text responses.

        > **GPT-4:** A highly advanced Large Language Model developed by OpenAI, known for its improved reasoning, creative capabilities, and ability to handle more complex and nuanced prompts compared to its predecessors.

    *   **Embeddings Models:**  Models like `text-embedding-3-small` for creating vector embeddings of text data.

        > **Embeddings Model:** A type of AI model that converts text, images, or other data into numerical vector representations called embeddings. These embeddings capture the semantic meaning of the data and enable efficient comparison and similarity calculations.

*   **DataStax Astra DB:** A serverless vector database that will be used to store and efficiently query vector embeddings of your data.

    > **Serverless Vector Database:** A type of database designed to store and efficiently query vector embeddings, and which operates in a serverless computing environment.  **Serverless** means the cloud provider automatically manages the underlying infrastructure, allowing users to focus on the database itself. A **Vector Database** is optimized for storing and searching high-dimensional vector embeddings, enabling similarity searches crucial for RAG systems.

## Understanding Vector Embeddings

**Vector embeddings** are a fundamental concept in modern AI and are crucial for implementing RAG effectively.

> **Vector Embedding:** A numerical representation of information (text, images, audio, etc.) in the form of a vector (an array of numbers).  These vectors capture the semantic meaning and relationships between different pieces of information, allowing computers to understand similarity and context.

Imagine turning words, sentences, or even entire documents into lists of numbers. These lists, or vectors, are designed in such a way that vectors representing similar concepts are located close to each other in a multi-dimensional space.

**Why are Vector Embeddings Important?**

*   **Semantic Meaning:** Vector embeddings capture the semantic meaning of text. Words with similar meanings (e.g., "dog" and "cat") will have embeddings that are closer together in the vector space than words with dissimilar meanings (e.g., "dog" and "car").

    > **Semantic Meaning:** The meaning or interpretation of words, phrases, sentences, and texts, taking into account context and relationships between words. Semantic meaning goes beyond literal definitions to understand the intended message and nuances of language.

*   **Similarity Search:**  Vector databases like Astra DB are optimized for performing similarity searches on vector embeddings. This means you can efficiently find vectors that are most similar to a query vector. In RAG, this allows you to quickly retrieve relevant chunks of text from your database based on the user's question, which is also converted into a vector embedding.

*   **Processing by Algorithms:**  Vector embeddings transform complex information into a format that can be easily processed by algorithms, especially **deep learning models**.

    > **Deep Learning Models:** A subset of machine learning models characterized by artificial neural networks with multiple layers (deep neural networks). Deep learning models are capable of learning complex patterns from large amounts of data and are particularly effective in tasks like image recognition, natural language processing, and speech recognition.

**Example: Word Similarity**

Consider the words "cat" and "dog."  If you convert these words into vector embeddings, a computer can analyze these numerical representations and determine that "cat" and "dog" are semantically similar.  This is because their embeddings will be closer to each other in the vector space compared to the embedding of a word like "dot" or "path," which, while sharing some letters, are not semantically related to "dog" in the same way.

It's important to note that different **Large Language Models (LLMs)** will generate different vector embeddings for the same word.  Embeddings created by OpenAI's models are not directly comparable to embeddings created by other models. Each model has its own way of representing semantic meaning numerically.

> **Lexicographically similar:**  Words that share similar letter patterns or sequences.  For example, "dot" and "dog" are lexicographically similar because they share the letters "do" and "og". This is different from semantic similarity, which focuses on meaning rather than letter patterns.

## Setting Up Your Environment and Accounts

### DataStax Astra DB Setup

1.  **Sign Up for DataStax Astra DB:** Navigate to the DataStax Astra DB website and sign up for a free account. No credit card is required for the free tier.

2.  **Create a Database:** Once logged in, create a new database. Choose the **Serverless Vector Database** option to ensure compatibility with vector embeddings.

    > **Serverless:** A cloud computing execution model where the cloud provider dynamically manages the allocation and provisioning of servers. Users do not need to manage servers, and are typically billed based on actual usage.

    > **Serverless vector database:** A vector database that operates in a serverless environment, offering scalability and ease of use without the need for manual server management.

3.  **Name Your Database:**  Give your database a descriptive name, such as "dbf1" for a Formula 1 chatbot.

4.  **Choose a Provider and Region:** Select a cloud provider (e.g., Amazon Web Services, Google Cloud, Microsoft Azure) and a region that is geographically closest to you for optimal performance.

5.  **Create the Database:** Click the "Create Database" button. Your database will be provisioned, which may take a few moments.

6.  **Gather Database Credentials:** Once the database is active, you will need to collect the following credentials:
    *   **Database Endpoint:**  Found on the "Overview" page of your database in the Astra DB dashboard. This is the address your application will use to connect to the database.
    *   **Application Token:** Generate an application token from the "Overview" page. This token is used for authentication and authorization when accessing your database.
    *   **Namespace (Keyspace):** The default keyspace name is "default\_keyspace." This is the logical container for your data within the database.

### OpenAI Account and API Key Setup

1.  **Sign Up for OpenAI:** Go to the OpenAI website (openai.com) and sign up for an account.

2.  **Access API Keys:** After logging in, navigate to the "API" section (usually found under "Products").

3.  **Create a New Secret Key:**  Go to the "API keys" section and create a new secret key. Give it a descriptive name for easy identification.

4.  **Copy and Secure Your API Key:**  Copy the generated API key and store it securely. **Treat your API key like a password and do not share it publicly.**  You will use this key to authenticate your application with OpenAI's services.

5.  **Billing and Credits (Optional):**  If you plan to use OpenAI's API extensively, you may need to set up billing and purchase credits.  Check your OpenAI account settings under "Billing" to manage your credits and payment information.

6.  **Identify Models:** Note the models you will be using in this course:
    *   **Chat Model:**  GPT-4 (for generating chatbot responses).
    *   **Embeddings Model:** `text-embedding-3-small` (for creating vector embeddings).

## Setting Up Your Project Environment

### Creating a Next.js Project

1.  **Open Your Code Editor:** Launch your preferred code editor (e.g., WebStorm, VS Code).

2.  **Create a New Next.js Project:**
    *   **Using WebStorm:** Select "New Project," choose "Next.js," specify a project directory and name (e.g., "nextjs-f1-gpt"), and ensure "TypeScript" is selected. Click "Create."
    *   **Using Terminal (for any editor):** Open your terminal, navigate to your desired projects directory, and run the following command:

        ```bash
        npx create-next-app@latest nextjs-f1-gpt --typescript
        ```

        Replace "nextjs-f1-gpt" with your desired project name.

3.  **Answer Project Setup Questions:** You will be prompted with a series of questions during project creation:
    *   "Would you like to use ESLint?" (Yes) - For code linting and quality.
    *   "Would you like to use Tailwind CSS?" (No) - We will use custom CSS.
    *   "Would you like to use `src/` directory?" (No) - We will use a different directory structure.
    *   "Would you like to use App Router?" (No) - We will use the Pages Router for simplicity.
    *   "Would you like to customize the default import alias?" (No) - Default settings are fine.

4.  **Wait for Project Creation:**  Next.js will create the project structure and install necessary dependencies.

### Project Directory Structure

After project creation, organize your project directory as follows:

```
nextjs-f1-gpt/
├── app/
│   ├── api/
│   │   └── chat/
│   │       └── route.ts  (API route for chat)
│   └── assets/
│       ├── f1-gpt-logo.png (Logo image)
│       └── background.jpg (Background image)
├── scripts/
│   └── load-db.ts         (Script to load data into Astra DB)
├── public/
│   └── ... (Optional public assets)
├── styles/
│   └── global.css        (Global CSS styles)
├── .env                 (Environment variables file)
├── package.json
├── tsconfig.json
└── ...
```

**Explanation of Key Directories and Files:**

*   **`app/`:**  Contains application-specific code.
    *   **`app/api/chat/route.ts`:**  Defines the API route for handling chatbot requests.

        > **API (Application Programming Interface):** A set of rules and specifications that software programs can follow to communicate with each other. APIs allow different software components to interact and exchange data, enabling integration and functionality extension.

    *   **`app/assets/`:**  Stores static assets like images and logos.
*   **`scripts/`:**  Contains scripts for database seeding and other utilities.
    *   **`scripts/load-db.ts`:**  A TypeScript script to scrape data, create vector embeddings, and load them into Astra DB.
*   **`styles/global.css`:**  Holds global CSS styles for the entire application.
*   **`.env`:**  Stores environment variables, including API keys and database credentials, keeping sensitive information separate from your code.
*   **`package.json`:**  Defines project dependencies and scripts for running and managing your application.
*   **`tsconfig.json`:**  Configuration file for TypeScript settings.

### Creating Essential Files

Create the following files within your project directory as outlined in the structure above:

1.  **`app/api/chat/route.ts`:**  Create `route.ts` within `app/api/chat/`.
2.  **`app/assets/f1-gpt-logo.png` and `app/assets/background.jpg`:** Add your logo and background images to the `app/assets/` directory. You can use placeholder images initially and replace them later.
3.  **`scripts/load-db.ts`:** Create `load-db.ts` within `scripts/`.
4.  **`styles/global.css`:**  Create `global.css` within `styles/`.
5.  **`app/layout.tsx`:** Create `layout.tsx` within `app/`.
6.  **`app/page.tsx`:** Create `page.tsx` within `app/`.
7.  **`app/components/`:** Create a `components` directory within `app/`.
8.  **`app/components/bubble.tsx`:** Create `bubble.tsx` within `app/components/`.
9.  **`app/components/prompt-suggestions-row.tsx`:** Create `prompt-suggestions-row.tsx` within `app/components/`.
10. **`app/components/prompt-suggestion-button.tsx`:** Create `prompt-suggestion-button.tsx` within `app/components/`.
11. **`app/components/loading-bubble.tsx`:** Create `loading-bubble.tsx` within `app/components/`.
12. **`.env`:** Create `.env` at the root of your project.

## Loading Data into Your Vector Database

Now, let's focus on populating your Astra DB vector database with Formula 1 data. This is crucial for enabling your RAG chatbot to answer questions based on up-to-date information.

### Setting Up Environment Variables in `.env`

Open the `.env` file you created and add the following environment variables, replacing the placeholder values with your actual credentials obtained from Astra DB and OpenAI:

```env
ASTRA_DB_NAMESPACE=default_keyspace
ASTRA_DB_COLLECTION_NAME=f1gpt
ASTRA_DB_API_ENDPOINT=YOUR_ASTRA_DB_ENDPOINT
ASTRA_DB_APPLICATION_TOKEN=YOUR_ASTRA_DB_APPLICATION_TOKEN
OPENAI_API_KEY=YOUR_OPENAI_API_KEY
```

### Installing Required Packages

Open your terminal in the project directory and install the necessary npm packages:

```bash
npm install @datastax/astra-db-ts langchain openai dotenv puppeteer ts-node ai
```

> **NPM (Node Package Manager):** The default package manager for Node.js. NPM is used to install, manage, and share JavaScript packages and modules, simplifying dependency management for Node.js projects.

> **TS Node:** A package that allows you to execute TypeScript files directly in Node.js without needing to compile them to JavaScript first. This is useful for running scripts during development.

### Modifying `tsconfig.json` for `ts-node`

To ensure `ts-node` works correctly with your TypeScript configuration, modify your `tsconfig.json` file. Locate the `"compilerOptions"` section and add the following:

```json
{
  "compilerOptions": {
    // ... other options
    "module": "CommonJS"
  },
  "ts-node": {
    "compilerOptions": {
      "module": "CommonJS"
    }
  }
}
```

> **TypeScript:** A superset of JavaScript that adds optional static typing. TypeScript enhances code maintainability and readability, especially in large projects, by catching type-related errors during development.

### Writing the `load-db.ts` Script

Open the `scripts/load-db.ts` file and paste the following code. This script will:

*   Import necessary packages.
*   Load environment variables from `.env`.
*   Connect to Astra DB and OpenAI.
*   Define URLs to scrape Formula 1 data from (Wikipedia, news sites, etc.).
*   Scrape content from these URLs using **Puppeteer**.

    > **Puppeteer:** A Node.js library that provides a high-level API to control Chrome or Chromium over the DevTools Protocol. Puppeteer is commonly used for web scraping, automated testing, and generating screenshots and PDFs of web pages.

*   Chunk the scraped text into smaller pieces using **RecursiveCharacterTextSplitter** from Langchain.

    > **Recursive Character Text Splitter:** A text splitting method provided by Langchain that recursively splits text into smaller chunks based on specified separators (e.g., newlines, sentences, words). This method is designed to maintain semantic coherence by attempting to split at meaningful boundaries.

*   Generate vector embeddings for each chunk using OpenAI's embeddings API (`text-embedding-3-small` model).
*   Insert these vector embeddings and their corresponding text chunks into your Astra DB collection.

```typescript
// Paste the code from the transcript's load-db.ts file here,
// ensuring you have installed all the packages and set up environment variables.
// ... (Code from transcript) ...
```

**Key parts of the `load-db.ts` script:**

*   **Import Statements:**  Imports necessary libraries for database interaction, web scraping, embedding generation, and environment variable handling.
*   **Environment Variable Loading:** Uses `dotenv` to load environment variables from your `.env` file.
*   **Database and OpenAI Client Initialization:** Establishes connections to Astra DB and OpenAI using your API keys and credentials.
*   **URL List:** Defines an array of URLs (`f1DataArray`) pointing to websites containing Formula 1 information. These URLs are scraped to gather data for your chatbot.
*   **`scrapePage` Function:** Uses Puppeteer to scrape the text content from a given URL. It launches a headless browser, navigates to the URL, waits for the DOM to load, extracts the inner HTML of the document body, and returns the text content after removing HTML tags using a regular expression.

    > **DOM (Document Object Model):** A programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as a tree structure where each node is an object representing a part of the document.

    > **Regular Expression (Rex):** A sequence of characters that define a search pattern. Regular expressions are used for string matching and manipulation, allowing for complex searches and replacements within text.

*   **`splitter` Initialization:** Creates a `RecursiveCharacterTextSplitter` instance to divide large text documents into smaller, manageable chunks.
*   **`createCollection` Function:** Asynchronously creates a new collection in Astra DB named as defined in your environment variables (`ASTRA_DB_COLLECTION_NAME`). It sets up vector indexing with a dimension size of 1536 (matching OpenAI's `text-embedding-3-small` model) and uses the dot product similarity metric.

    > **Similarity Metric:** A function used to quantify the similarity between two vectors. Common similarity metrics for vector embeddings include dot product, cosine similarity, and Euclidean distance. These metrics help determine how closely related two pieces of information are in the vector space.

    > **Dot product:** A similarity metric used to calculate the similarity between two vectors. A higher dot product value generally indicates greater similarity, especially when vectors are normalized.

    > **Cosine:** A similarity metric that measures the cosine of the angle between two vectors. Cosine similarity ranges from -1 to 1, with 1 indicating perfect similarity, 0 indicating orthogonality (no similarity), and -1 indicating opposite similarity.

    > **Euclidean similarity metrics:**  Measures the straight-line distance between two vectors in a vector space. A smaller Euclidean distance indicates greater similarity between the vectors.

*   **`loadSampleData` Function:**  This asynchronous function orchestrates the data loading process:
    *   Retrieves the Astra DB collection.
    *   Iterates through each URL in `f1DataArray`.
    *   Calls `scrapePage` to get the text content for each URL.
    *   Splits the text content into chunks using the `splitter`.
    *   For each chunk:
        *   Generates a vector embedding using OpenAI's embeddings API.
        *   Inserts the vector embedding and the original text chunk into the Astra DB collection.
    *   Logs the insertion responses to the console.
*   **Script Execution:** Calls `createCollection` followed by `loadSampleData` in a `.then()` chain to ensure the collection is created before data loading begins.

### Running the `load-db.ts` Script

1.  **Open your terminal** in the project directory.
2.  **Run the seeding script:** Execute the following command to run the `load-db.ts` script using `ts-node`:

    ```bash
    npm run seed
    ```

    This command will execute the script, which will scrape the websites, generate vector embeddings, and populate your Astra DB database. **This process may take some time**, depending on the number of URLs and the amount of data being scraped. You can monitor the progress in your terminal console, as the script logs each insertion into the database.

3.  **Verify Data in Astra DB:** After the script completes, go to your Astra DB dashboard and navigate to your database.  You should see the collection you created (e.g., "f1gpt") populated with documents. Each document will contain a vector embedding and the corresponding text chunk.

## Building the Chatbot Frontend with Next.js

With your data loaded into Astra DB, you can now build the frontend of your chatbot using Next.js.

### Setting Up the Layout (`app/layout.tsx`)

Open `app/layout.tsx` and paste the following code. This sets up the basic layout of your Next.js application, including:

*   Importing global CSS styles.
*   Defining metadata (title and description) for SEO purposes.

    > **SEO (Search Engine Optimization):** The practice of improving the visibility of a website or a web page in a search engine's unpaid results—often referred to as "natural," "organic," or "earned" results. SEO involves optimizing website content and structure to rank higher in search engine results pages (SERPs) for relevant keywords.

*   Creating a root layout component (`RootLayout`) that wraps your application content in HTML and body tags.

```typescript
// Paste the code from the transcript's layout.tsx file here.
// ... (Code from transcript) ...
```

### Building the Main Page (`app/page.tsx`)

Open `app/page.tsx` and paste the code for the main page component. This component will handle:

*   Importing necessary components and images.
*   Using the `useChat` hook from Vercel AI to manage chat state (messages, input, loading state).

    > **Hook (React):**  A special function in React that lets you "hook into" React state and lifecycle features from within functional components. Hooks enable functional components to manage state and perform side effects, which were previously only possible in class components.

    > **State (React):** Data that changes over time within a React component. State is used to manage dynamic content and user interactions in a React application. When state changes, React re-renders the component to reflect the updated data.

*   Displaying the chatbot interface, including:
    *   Logo.
    *   Starter text and prompt suggestions when no messages exist.
    *   Chat message bubbles.
    *   Loading bubble indicator.
    *   Input form for user queries.

```typescript
// Paste the code from the transcript's page.tsx file here.
// ... (Code from transcript) ...
```

**Key parts of the `app/page.tsx` component:**

*   **`'use client'` directive:**  Specifies that this component is a client-side component, enabling the use of React hooks and browser APIs.
*   **Import Statements:** Imports `Image` from `next/image` for image rendering, `useChat` hook from `ai/vercel` for chat state management, and custom components (`Bubble`, `LoadingBubble`, `PromptSuggestionsRow`).
*   **`Home` Component:** The main functional component for the page.
    *   **`useChat` Hook:**  Initializes the `useChat` hook to manage chat state. This hook returns functions and state variables like `messages`, `input`, `handleInputChange`, `handleSubmit`, `append`, and `isLoading`.

        > **`useChat` Hook:** A React Hook provided by the `ai/vercel` library that simplifies the creation of chat interfaces. It manages chat message history, input state, loading state, and provides functions for sending messages and appending new messages to the chat.

    *   **`noMessages` Variable:**  Determines if there are any messages in the chat history to conditionally render different UI elements.
    *   **Conditional Rendering:**  Uses conditional rendering to display either starter text and prompt suggestions (when `noMessages` is true) or chat messages and a loading indicator (when `noMessages` is false).
    *   **Message Mapping:** Maps over the `messages` array to render a `Bubble` component for each message.
    *   **`LoadingBubble` Component:**  Conditionally renders the `LoadingBubble` component when `isLoading` is true, indicating that the chatbot is processing a request.
    *   **`PromptSuggestionsRow` Component:** Renders a row of prompt suggestion buttons.
    *   **Input Form:**  Creates a form with an input field for user queries and a submit button. The input field is controlled by the `input` state and `handleInputChange` function from the `useChat` hook. The form submission is handled by the `handleSubmit` function from the `useChat` hook.

### Creating Chat Components (`app/components/`)

Create the following components within the `app/components/` directory:

1.  **`bubble.tsx`:**  Represents a single chat message bubble.

```typescript
// Paste the code from the transcript's bubble.tsx file here.
// ... (Code from transcript) ...
```

2.  **`loading-bubble.tsx`:**  Displays a loading animation to indicate chatbot activity.

```typescript
// Paste the code from the transcript's loading-bubble.tsx file here.
// ... (Code from transcript) ...
```

3.  **`prompt-suggestions-row.tsx`:**  Renders a row of prompt suggestion buttons.

```typescript
// Paste the code from the transcript's prompt-suggestions-row.tsx file here.
// ... (Code from transcript) ...
```

4.  **`prompt-suggestion-button.tsx`:** Represents a single prompt suggestion button.

```typescript
// Paste the code from the transcript's prompt-suggestion-button.tsx file here.
// ... (Code from transcript) ...
```

**Key aspects of the components:**

*   **`Bubble` Component:**  Receives a `message` prop (containing `content` and `role`) and renders a chat bubble with the message content. The styling of the bubble is conditionally adjusted based on the `role` (user or assistant) using CSS classes.
*   **`LoadingBubble` Component:**  Renders a simple loading animation using CSS keyframes to indicate that the chatbot is processing.

    > **Keyframes:** In CSS animations, keyframes define specific points in time during an animation sequence. Each keyframe specifies the styles that an element should have at that particular time, allowing for precise control over animation transitions and effects.

*   **`PromptSuggestionsRow` Component:**  Renders a horizontal row of `PromptSuggestionButton` components. It defines an array of example prompts and maps over them to create buttons for each prompt. It also passes a `handlePrompt` function down as a prop to handle button clicks.
*   **`PromptSuggestionButton` Component:**  Renders a button element that displays a prompt text. It receives `text` and `onPromptClick` props. When clicked, it calls the `onPromptClick` function, passing the button's text as an argument. This triggers the prompt handling logic in the parent component (`page.tsx`).

### Styling with CSS (`styles/global.css`)

Open `styles/global.css` and paste the CSS styles from the transcript. These styles provide basic styling for your chatbot application, including:

*   Font family and base body styles.
*   Styling for the main container, sections, text, form, input fields, buttons, bubbles, loading animation, and prompt suggestion buttons.

```css
/* Paste the code from the transcript's global.css file here. */
/* ... (Code from transcript) ... */
```

### Creating the Chat API Route (`app/api/chat/route.ts`)

Finally, create the API route in `app/api/chat/route.ts`. This route will handle the backend logic for your chatbot:

*   Import necessary packages (OpenAI, OpenAIStream, StreamingTextResponse, DataStax Astra DB).
*   Load environment variables.
*   Initialize OpenAI and Astra DB clients.
*   Define a `POST` route handler function (`POST`) to process incoming chat requests.

    > **Post request:** An HTTP request method used to send data to a server to create or update a resource. In the context of a chatbot, a POST request is typically used to send the user's message to the backend API for processing and response generation.

*   Within the `POST` handler:
    *   Extract the latest message from the request body.
    *   Generate a vector embedding of the user's message using OpenAI's embeddings API.
    *   Query Astra DB to find the most similar documents (text chunks) based on the embedding.
    *   Construct a prompt for OpenAI's chat completions API, including:
        *   A system message defining the chatbot's role and instructions.

            > **System Message:** In the context of OpenAI's chat completions API, a system message is used to set the behavior and persona of the chatbot. It provides instructions and context to guide the model's responses.

        *   The retrieved context from Astra DB.
        *   The user's original message.
    *   Call OpenAI's chat completions API (`gpt-4` model) with the prompt and stream the response.

        > **Stream (data):** In the context of APIs and data transfer, streaming refers to the process of sending data in a continuous flow rather than in discrete chunks. This allows for real-time or near real-time data processing and delivery, improving responsiveness and user experience, especially in applications like chatbots where immediate feedback is desired.

    *   Return a `StreamingTextResponse` to send the streamed response back to the frontend.

```typescript
// Paste the code from the transcript's route.ts file here.
// ... (Code from transcript) ...
```

**Key parts of the `app/api/chat/route.ts` file:**

*   **Import Statements:** Imports necessary libraries for OpenAI API interaction, streaming responses, and Astra DB interaction.
*   **Environment Variable Loading:** Loads environment variables from `.env`.
*   **Client Initialization:** Initializes OpenAI and Astra DB clients using your API keys and credentials.
*   **`POST` Route Handler:** Defines an asynchronous `POST` function to handle incoming API requests.
    *   **Request Processing:** Extracts the latest message from the incoming request's JSON body.
    *   **Embedding Generation:** Generates a vector embedding for the user's message using OpenAI's embeddings API.
    *   **Database Query:** Queries the Astra DB collection using the generated embedding to find semantically similar documents. It uses a `find` operation with a `$vector` sort to perform a similarity search and limits the results to 10 documents.

        > **Cursor (database):**  In database terms, a cursor is a control structure that enables traversal over the records in a database. Cursors are used to retrieve data row by row or in chunks, allowing for efficient processing of large datasets, especially when streaming results.

    *   **Prompt Construction:** Creates a prompt for OpenAI's chat completions API. The prompt includes a system message defining the chatbot's persona as a Formula 1 expert, instructions to use provided context, and the user's original question.
    *   **OpenAI Chat Completion API Call:** Calls OpenAI's chat completions API (`openai.chat.completions.create`) with the constructed prompt and streaming enabled (`stream: true`). It uses the `gpt-4` model for response generation.
    *   **Streaming Response:**  Wraps the OpenAI API response stream in an `OpenAIStream` and then returns a `StreamingTextResponse`. This streams the chatbot's response back to the frontend in real-time.

        > **Promise (JavaScript):** An object representing the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises are used to handle asynchronous operations in JavaScript, such as API calls, in a more structured and manageable way.

    *   **Error Handling:** Includes `try...catch` blocks to handle potential errors during database queries and API calls.

## Running Your RAG Chatbot

1.  **Start the Next.js Development Server:** Open your terminal in the project directory and run:

    ```bash
    npm run dev
    ```

    This command starts the Next.js development server.

2.  **Access Your Chatbot:** Open your web browser and navigate to `http://localhost:3000`. You should see your Formula 1 chatbot application running.

3.  **Test Your Chatbot:** Try asking Formula 1 related questions in the input field or click on the prompt suggestion buttons. Observe how your chatbot responds with up-to-date answers powered by the data you loaded into Astra DB.

## Conclusion

Congratulations! You have successfully built a functional RAG chatbot using JavaScript, Langchain JS, Next.js, Vercel, OpenAI, and DataStax Astra DB. You now have a solid understanding of:

*   Retrieval-Augmented Generation (RAG) and its benefits.
*   Vector embeddings and their role in semantic search.
*   Building a full-stack chatbot application using modern JavaScript technologies.
*   Integrating external data sources to enhance the knowledge of language models.

This chapter provides a foundation for you to explore further possibilities with RAG chatbots. You can expand upon this project by:

*   Adding more data sources to scrape from to broaden the chatbot's knowledge base.
*   Fine-tuning the prompt template to improve response quality and style.
*   Implementing user authentication and chat history persistence.
*   Deploying your chatbot to Vercel for public access.

Remember to handle your API keys and database credentials securely and explore the documentation of each technology to deepen your understanding and build even more sophisticated AI-powered applications. Happy coding!
```
