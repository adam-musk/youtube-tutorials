---
layout: "../../layouts/BlogPost.astro"
title: "Analyzing Multimodal Data with Large Language Models: A Comprehensive Guide"
pubDate: "2025-02-28 15:26:24.123131"
youtubeVideoID: "3-4qAkFRpAk"
index: 53
---

# Analyzing Multimodal Data with Large Language Models: A Comprehensive Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/3-4qAkFRpAk" frameborder="0" allowfullscreen></iframe>


## Introduction

Welcome to this educational exploration of analyzing multimodal data leveraging the power of cutting-edge Large Language Models (LLMs) and Python. In this chapter, we will delve into the capabilities of models like **GPT-4 Omni**, which are revolutionizing data analysis by processing diverse data types including text, images, and audio. You will learn practical techniques to classify text sentiment, answer questions based on image content, transcribe speech to text, and even build natural language interfaces for querying SQL databases. By the end of this chapter, you will be equipped to start developing your own LLM-powered applications and unlock the transformative potential of LLMs in your data analysis workflows.

This chapter is based on the teachings of Emanuel Trumer, an Associate Professor at Cornell University with a PhD in Computer Science. His expertise will guide you through the practical applications of these powerful technologies.

## 1. The Rise of Multimodal Large Language Models

**Large Language Models (LLMs)** have emerged as a disruptive force in computer science, demonstrating remarkable abilities in areas such as text processing and code generation.

> **Large Language Models (LLMs):**  Advanced artificial intelligence models trained on vast amounts of text data. They are capable of understanding, generating, and manipulating human language for various tasks.

The latest generation of these models, exemplified by **GPT-4 Omni**, exhibits **multimodal** capabilities.

> **Multimodal:**  Refers to the ability of a system or model to process and understand multiple types of data input, such as text, images, audio, and video, simultaneously.

This signifies a significant leap forward, as these models can now process not only textual input but also various other data formats like images and sound files. This chapter will guide you through using these LLMs with Python to analyze diverse data types, all through a unified and accessible Python API.

## 2. Setting Up Your Python Environment for LLM Interaction

To begin working with LLMs in Python, specifically focusing on OpenAI models like GPT-4 Omni, we need to set up our development environment. This involves installing the necessary Python library and configuring access to your OpenAI account.

### 2.1 Installing the OpenAI Python Library

The first step is to install the official OpenAI Python library. This library provides the necessary tools to interact with OpenAI's models programmatically. Open your terminal or command prompt and execute the following command using **pip**, the Python package installer:

```bash
pip install openai
```

> **pip:**  A package installer for Python. It allows you to easily install and manage libraries and dependencies for your Python projects.

This command will download and install the latest version of the `openai` library. You might see a message indicating that the library is already installed if you have used it before. The transcript mentions version `1.2.9` as an example, and while minor version differences usually don't cause issues, you can ensure compatibility by specifying a version during installation:

```bash
pip install openai==1.2.9
```

### 2.2 Configuring OpenAI API Access

After installing the library, you need to connect it to your OpenAI account to authorize your requests to use their models. This involves obtaining an **API key** and setting it as an **environment variable**.

> **API Key:**  A unique secret key that authenticates your requests to an Application Programming Interface (API), like the OpenAI API, allowing you to access and use its services.

> **Environment Variable:**  A named value that is part of the operating system's environment. It can be accessed by programs running in that environment, allowing for configuration settings to be set outside of the code itself.

**Steps to Obtain and Set Your API Key:**

1.  **Visit the OpenAI Platform:** Go to [platform.openai.com](platform.openai.com) in your web browser.
2.  **Log In or Sign Up:** Log in if you already have an OpenAI account. If not, you will need to create one.
3.  **Navigate to API Keys:** Once logged in, go to your profile page and find the "User API Keys" section (often found under "Profile" or similar).
4.  **Create a New Secret Key:** Click on the "Create new secret key" button. You can provide a name for your key for easy identification.
5.  **Copy Your Secret Key:**  After creation, you will be presented with your secret API key. **Copy this key immediately and store it securely.** You will not be able to see it again.

**Setting the Environment Variable:**

The method for setting environment variables depends on your operating system.

*   **macOS/Linux (Terminal):** Open your terminal and use the `export` command:

    ```bash
    export OPENAI_API_KEY='your_secret_api_key_here'
    ```
    Replace `'your_secret_api_key_here'` with the actual key you copied.

*   **Windows (Command Prompt):** Open your command prompt and use the `setx` command:

    ```bash
    setx OPENAI_API_KEY "your_secret_api_key_here"
    ```
    Replace `"your_secret_api_key_here"` with your API key. Note that `setx` changes environment variables permanently for future sessions. You might need to restart your command prompt for the changes to take effect.

*   **Windows (PowerShell):**  Use the `$env:` syntax:

    ```powershell
    $env:OPENAI_API_KEY = "your_secret_api_key_here"
    ```
    Replace `"your_secret_api_key_here"` with your API key. This sets the variable for the current PowerShell session. To make it permanent, you can use `setx` as in the Command Prompt instructions.

After setting the environment variable, the OpenAI Python library will automatically detect it and use it to authenticate your requests. You no longer need to explicitly pass the API key in your Python code, enhancing security and code cleanliness.

With the library installed and API key configured, you are now ready to start using OpenAI's LLMs in Python.

## 3. Text Classification: Sentiment Analysis with LLMs

One of the fundamental applications of LLMs is text classification. A common example is **sentiment classification**, also known as sentiment analysis, where the goal is to determine the emotional tone or sentiment expressed in a piece of text, typically as positive, negative, or neutral.

> **Sentiment Classification (Sentiment Analysis):**  A natural language processing task that involves determining the emotional tone or subjective opinion expressed in text. It is often categorized into positive, negative, and neutral sentiments.

Let's explore how to implement sentiment classification using GPT-4 Omni and Python.

### 3.1 Python Implementation for Sentiment Classification

We will create a Python script that takes text input (either directly or from a CSV file) and uses GPT-4 Omni to classify its sentiment as positive or negative.

**3.1.1 Setting up the Python Script**

First, import the necessary libraries: `openai` to interact with the OpenAI API and `argparse` to handle command-line arguments. We'll also import `pandas` later when we process CSV files.

```python
import openai
import argparse
import pandas as pd # Import pandas for CSV processing
```

**3.1.2 Creating the OpenAI Client**

Instantiate an OpenAI client object. This object will be used to send requests to the OpenAI API. As we've set the `OPENAI_API_KEY` as an environment variable, the client will automatically authenticate.

```python
client = openai.OpenAI()
```

**3.1.3 Creating a Prompt Function**

The **prompt** is the instruction you give to the LLM, guiding it to perform the desired task.  For sentiment classification, the prompt should include the text to be classified and clear instructions on what the LLM should do.

> **Prompt:** In the context of Large Language Models, a prompt is the input text you provide to the model to elicit a specific response or action. It serves as instructions and context for the model.

Let's define a function `create_prompt` that takes text as input and generates a well-structured prompt:

```python
def create_prompt(text):
    """
    Creates the input prompt for the language model for sentiment classification.

    Args:
        text (str): The text to classify.

    Returns:
        str: The prompt for text classification.
    """
    instruction = "Determine if the sentiment of the following text is positive or negative."
    formatting_instructions = "Answer with either 'positive' or 'negative'."
    prompt_text = f"""
    Text to classify:
    {text}

    Instructions:
    {instruction}

    Format your answer as:
    {formatting_instructions}

    Sentiment:
    """
    return prompt_text
```

This function constructs a prompt that clearly presents the text to be analyzed, instructs the model to determine the sentiment (positive or negative), and specifies the desired output format ("positive" or "negative").

**3.1.4 Calling the Language Model (LLM)**

Now, we create a function `call_llm` to send the prompt to the GPT-4 Omni model and retrieve its response. We will use the `chat.completions.create` method, as GPT-4 Omni is a **chat model**.

> **Chat Models:** Large Language Models designed and optimized for conversational interactions. They typically expect a sequence of messages as input and are designed to generate responses in a dialogue-like format.

> **Completions Endpoint:** In the OpenAI API, the completions endpoint is used to generate text completions based on a given prompt. For chat models, it's specifically accessed through `chat.completions`.

```python
def call_llm(prompt):
    """
    Calls the Large Language Model with the input prompt to get a reply.

    Args:
        prompt (str): The prompt to send to the language model.

    Returns:
        str: The answer obtained from the language model.
    """
    messages = [{"role": "user", "content": prompt}] # Structure prompt as a user message
    response = client.chat.completions.create(
        model="gpt-4-turbo-preview", # Using GPT-4 Omni (preview model for now)
        messages=messages
    )
    return response.choices[0].message.content # Extract and return the model's answer
```

Here, we structure the prompt as a single "user" message within a list of messages, which is the expected format for chat models. We specify `gpt-4-turbo-preview` as the model (referring to GPT-4 Omni at the time of the transcript). The function then extracts and returns the text content of the model's generated message.

**3.1.5 Command Line Argument Parsing and Execution**

To make our script executable from the command line, we use `argparse` to handle input arguments. In this initial version, we will accept the text to classify directly as a command-line argument.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Classify text sentiment using GPT-4 Omni.")
    parser.add_argument("text", type=str, help="The text to classify.")
    args = parser.parse_args()

    prompt = create_prompt(args.text)
    answer = call_llm(prompt)
    print(f"Sentiment: {answer}")
```

This code block ensures that the following code is executed only when the script is run directly (not imported as a module). It sets up an argument parser to accept a text string as input.  It then creates the prompt, calls the LLM, and prints the resulting sentiment classification.

**3.1.6 Running the Script**

Save the code as a Python file (e.g., `sentiment_classifier.py`).  You can run it from your terminal like this:

```bash
python sentiment_classifier.py "The movie was fantastic!"
```

The output should be something like:

```
Sentiment: positive
```

### 3.2 Processing Sentiment from a CSV File

To handle multiple reviews or text entries efficiently, we can modify the script to read text from a CSV file and classify the sentiment for each entry.

**3.2.1 Modifying Argument Parsing**

Instead of taking text directly as an argument, we will now take the path to a CSV file.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Classify text sentiment from a CSV file using GPT-4 Omni.")
    parser.add_argument("csv_path", type=str, help="Path to the input CSV file.") # Changed argument to csv_path
    args = parser.parse_args()
    csv_path = args.csv_path # Get the path from arguments
```

**3.2.2 Reading CSV with Pandas**

Use pandas to read the CSV file into a DataFrame. We assume the CSV file has a column named 'text' containing the reviews or text entries.

```python
    df = pd.read_csv(csv_path) # Read CSV into a pandas DataFrame
```

**3.2.3 Applying Sentiment Classification to Each Row**

We will define a `classify_text` function that encapsulates the prompt creation and LLM call for a single text entry. This function will then be applied to each row of the DataFrame using pandas' `apply` function.

```python
def classify_text(text):
    """
    Classifies the sentiment of the input text using GPT-4 Omni.

    Args:
        text (str): The text to classify.

    Returns:
        str: The sentiment class ('positive' or 'negative').
    """
    prompt = create_prompt(text)
    answer = call_llm(prompt)
    return answer

    # ... (rest of the script in if __name__ == "__main__": block)

    df['class'] = df['text'].apply(classify_text) # Apply classify_text to each 'text' entry
    print(df) # Print the DataFrame with the added 'class' column
```

We apply the `classify_text` function to the 'text' column of the DataFrame and store the results in a new column named 'class'. Finally, we print the entire DataFrame, now including the sentiment classifications.

**3.2.4 Running with CSV Input**

Create a CSV file (e.g., `reviews.csv`) with a 'text' column containing review texts. Run the script, providing the path to the CSV file as a command-line argument:

```bash
python sentiment_classifier.py data/reviews.csv
```

The output will be the DataFrame printed to the console, with an added 'class' column showing the sentiment classification for each review.

## 4. Image Question Answering: Multimodal Analysis

GPT-4 Omni's multimodal nature extends beyond text to include images. We can build applications that analyze images and answer questions about their content. Let's create a simple image question answering system.

### 4.1 Python Implementation for Image Question Answering

This script will take an image URL and a question as input and use GPT-4 Omni to answer the question based on the image content.

**4.1.1 Setting up the Python Script**

Import necessary libraries: `openai` and `argparse`.

```python
import openai
import argparse
```

**4.1.2 Creating the OpenAI Client (Same as before)**

```python
client = openai.OpenAI()
```

**4.1.3 Creating the `analyze_image` Function**

This function will take the image URL and the question as input and interact with GPT-4 Omni to get the answer.

```python
def analyze_image(image_url, question):
    """
    Answers questions about the input image using GPT-4 Omni.

    Args:
        image_url (str): URL of the image to analyze.
        question (str): The question to ask about the image.

    Returns:
        str: The answer to the question.
    """
    messages = [
        {
            "role": "user",
            "content": [
                {"type": "text", "text": question}, # Text component: the question
                {"type": "image_url", "image_url": {"url": image_url}}, # Image component: URL
            ],
        }
    ]

    response = client.chat.completions.create(
        model="gpt-4-turbo-preview", # GPT-4 Omni model
        messages=messages,
        max_tokens=300 # Limit response length if needed
    )
    return response.choices[0].message.content
```

In this function, the `messages` are structured to include both text and image components within the `content` list. The text component contains the question, and the image component specifies the `image_url` and its URL. We again use `gpt-4-turbo-preview` and the `chat.completions.create` method.

**4.1.4 Command Line Argument Parsing and Execution**

Set up `argparse` to accept the image URL and the question as command-line arguments.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Answer questions about images using GPT-4 Omni.")
    parser.add_argument("image_url", type=str, help="URL of the image.")
    parser.add_argument("question", type=str, help="Question about the image.")
    args = parser.parse_args()

    image_url = args.image_url
    question = args.question

    answer = analyze_image(image_url, question)
    print(f"Answer: {answer}")
```

This section parses the `image_url` and `question` from the command line, calls the `analyze_image` function, and prints the generated answer.

**4.1.5 Running the Image QA Script**

Save the code as `image_qa.py`. Run it from your terminal, providing an image URL and a question:

```bash
python image_qa.py "URL_OF_AN_APPLE_IMAGE" "What kind of fruit is this?"
```

Replace `"URL_OF_AN_APPLE_IMAGE"` with an actual URL of an image. The output will be the LLM's answer to your question about the image.

### 4.2 Comparing Two Images

We can extend this to compare two images by providing two image URLs in the prompt.

**4.2.1 Modifying `analyze_image` for Two Images**

Update the `analyze_image` function to accept two image URLs.

```python
def analyze_image(image_url1, image_url2, question):
    """
    Answers questions about two input images using GPT-4 Omni.

    Args:
        image_url1 (str): URL of the first image.
        image_url2 (str): URL of the second image.
        question (str): Question comparing the images.

    Returns:
        str: The comparative answer.
    """
    messages = [
        {
            "role": "user",
            "content": [
                {"type": "text", "text": question},
                {"type": "image_url", "image_url": {"url": image_url1}},
                {"type": "image_url", "image_url": {"url": image_url2}}, # Added second image
            ],
        }
    ]
    response = client.chat.completions.create(
        model="gpt-4-turbo-preview",
        messages=messages,
        max_tokens=500 # Increased max_tokens for potentially longer comparative answers
    )
    return response.choices[0].message.content
```

We've added a second `image_url` parameter and included a second image URL component in the `messages` list. We also increased `max_tokens` to accommodate potentially longer comparative answers.

**4.2.2 Modifying Command Line Arguments**

Update `argparse` to accept two image URLs.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Compare two images using GPT-4 Omni.")
    parser.add_argument("image_url1", type=str, help="URL of the first image.")
    parser.add_argument("image_url2", type=str, help="URL of the second image.")
    parser.add_argument("question", type=str, help="Question to compare the images.")
    args = parser.parse_args()

    image_url1 = args.image_url1
    image_url2 = args.image_url2
    question = args.question

    answer = analyze_image(image_url1, image_url2, question)
    print(f"Answer: {answer}")
```

**4.2.3 Running the Image Comparison Script**

Run the script with two image URLs and a comparative question:

```bash
python image_qa.py "URL_OF_APPLES_IMAGE" "URL_OF_ORANGES_IMAGE" "Compare these two images."
```

The output will be GPT-4 Omni's comparison of the two images based on your question.

## 5. Audio Transcription: Speech-to-Text Conversion

Another powerful application of LLMs is audio processing, specifically speech-to-text transcription. While GPT-4 Omni's audio capabilities via API might have been limited at the time of the transcript, OpenAI provides the **Whisper model**, specifically designed for audio transcription.

> **Whisper Model:** An OpenAI-developed neural network model specifically trained for robust and accurate speech-to-text transcription across various languages and audio conditions.

We will use the Whisper model to transcribe audio files in Python.

### 5.1 Python Implementation for Audio Transcription

This script will take the path to an audio file as input and output the transcribed text.

**5.1.1 Setting up the Python Script**

Import `openai` and `argparse`.

```python
import openai
import argparse
```

**5.1.2 Creating the OpenAI Client (Same as before)**

```python
client = openai.OpenAI()
```

**5.1.3 Creating the `transcribe_audio` Function**

This function will take the audio file path, open the file in binary mode, and use the Whisper model to transcribe it.

```python
def transcribe_audio(audio_path):
    """
    Transcribes an audio file using the OpenAI Whisper model.

    Args:
        audio_path (str): Path to the audio file.

    Returns:
        str: The transcribed text.
    """
    with open(audio_path, "rb") as audio_file: # Open audio file in binary read mode
        transcript = client.audio.transcriptions.create(
            model="whisper-1", # Using the Whisper-1 model
            file=audio_file
        )
    return transcript.text
```

Here, we open the audio file in binary read mode (`"rb"`) as required by the OpenAI API for audio uploads. We use `client.audio.transcriptions.create` with `model="whisper-1"` to specify the Whisper model. The function returns the transcribed text from the `transcript` object.

**5.1.4 Command Line Argument Parsing and Execution**

Set up `argparse` to accept the audio file path as a command-line argument.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Transcribe audio files using OpenAI Whisper.")
    parser.add_argument("audio_path", type=str, help="Path to the audio file.")
    args = parser.parse_args()

    audio_path = args.audio_path

    transcription = transcribe_audio(audio_path)
    print(f"Transcription: {transcription}")
```

This part parses the `audio_path`, calls `transcribe_audio`, and prints the resulting transcription.

**5.1.5 Running the Audio Transcription Script**

Save the code as `audio_transcriber.py`. Run it from your terminal, providing the path to an audio file (e.g., MP3, WAV, etc.):

```bash
python audio_transcriber.py data/audio_example.mp3
```

Replace `data/audio_example.mp3` with the actual path to your audio file. The output will be the transcribed text of the audio.

## 6. Tabular Data Analysis: Natural Language to SQL Queries

Analyzing tabular data, especially large databases, poses unique challenges for LLMs. Directly feeding large tables to LLMs can be inefficient and costly. A more effective approach is to use LLMs to translate natural language questions into **SQL (Structured Query Language)** queries.

> **SQL (Structured Query Language):** A standard programming language designed for managing and querying data held in a relational database management system (RDBMS).

> **Relational Database Management System (RDBMS):**  A system for managing data that is structured in tables with relationships between them. Examples include MySQL, PostgreSQL, and SQLite.

We will build a system that takes natural language questions about a database and converts them into SQL queries that can be executed against the database.

### 6.1 Python Implementation for Natural Language to SQL

This script will take a database file path and a natural language question as input and output the corresponding SQL query and the query result. We will use **SQLite**, a lightweight and file-based database system.

> **SQLite:** A self-contained, serverless, zero-configuration, transactional SQL database engine. It is widely used for local/client storage in application software.

**6.1.1 Setting up the Python Script**

Import `openai`, `argparse`, `sqlite3`, and `re` (for regular expressions to extract SQL from LLM output).

```python
import openai
import argparse
import sqlite3
import re # For regular expression processing
```

**6.1.2 Creating the OpenAI Client (Same as before)**

```python
client = openai.OpenAI()
```

**6.1.3 Function to Extract Database Structure**

We need to provide the LLM with the database schema (table and column definitions). We create a function `extract_structure` to automatically extract this from an SQLite database file.

```python
def extract_structure(db_path):
    """
    Extracts CREATE TABLE statements from an SQLite database file.

    Args:
        db_path (str): Path to the SQLite database file.

    Returns:
        str: String containing CREATE TABLE statements.
    """
    conn = sqlite3.connect(db_path)
    cursor = conn.cursor()
    cursor.execute("SELECT sql FROM sqlite_master WHERE type='table';") # Query to get CREATE TABLE SQL
    table_schemas = cursor.fetchall()
    conn.close()
    structure_string = "\n".join([schema[0] for schema in table_schemas if schema[0] is not None]) # Join schemas into a single string
    return structure_string
```

This function connects to the SQLite database, queries the `sqlite_master` table to retrieve the SQL `CREATE TABLE` statements, and returns them as a single string.

**6.1.4 Creating the Prompt Function for SQL Translation**

We create a `create_prompt` function that takes the question and the database structure and generates a prompt for SQL translation.

```python
def create_prompt(question, database_structure):
    """
    Creates a prompt for translating natural language questions to SQL queries.

    Args:
        question (str): The natural language question.
        database_structure (str): Database structure description (CREATE TABLE SQL).

    Returns:
        str: The prompt for SQL translation.
    """
    parts = [
        "Database schema:\n" + database_structure, # Database structure description
        "\nTranslate this question to SQL:\n" + question, # Question to translate
    ]
    return "\n".join(parts) # Combine parts with newlines
```

The prompt includes the database schema description followed by the question, instructing the LLM to translate the question into SQL, considering the provided schema.

**6.1.5 Function to Call the LLM (Similar to before)**

```python
def call_llm(prompt):
    """
    Calls the Large Language Model with the input prompt to get a reply.

    Args:
        prompt (str): The prompt to send to the language model.

    Returns:
        str: The answer obtained from the language model.
    """
    messages = [{"role": "user", "content": prompt}]
    response = client.chat.completions.create(
        model="gpt-4-turbo-preview",
        messages=messages,
        max_tokens=500 # Adjust max_tokens as needed
    )
    raw_answer = response.choices[0].message.content
    # Extract SQL query using regular expressions
    sql_query_matches = re.findall(r"```sql\s*(.*?)\s*```", raw_answer, re.DOTALL) # Regex to find SQL code blocks
    if sql_query_matches:
        return sql_query_matches[0].strip() # Return the first matched SQL query
    else:
        return "No SQL query found in the response." # Handle case where no SQL is extracted

```

This `call_llm` function is similar to the previous ones, but now it includes regular expression processing to extract the SQL query from the LLM's response. It searches for code blocks enclosed in ```sql ... ``` and returns the extracted SQL query.

**6.1.6 Function to Process SQL Query and Get Results**

We create a `process_query` function to execute the generated SQL query against the database and return the results.

```python
def process_query(db_path, sql_query):
    """
    Processes the input SQL query on the SQLite database and returns results.

    Args:
        db_path (str): Path to the SQLite database file.
        sql_query (str): The SQL query to execute.

    Returns:
        str: Query results as a string.
    """
    conn = sqlite3.connect(db_path)
    cursor = conn.cursor()
    try:
        cursor.execute(sql_query) # Execute the SQL query
        results = cursor.fetchall() # Fetch all results
        conn.close()
        return "\n".join([str(row) for row in results]) # Format results as strings
    except sqlite3.Error as e:
        conn.close()
        return f"Error executing SQL query: {e}" # Handle potential SQL errors
```

This function connects to the database, executes the provided SQL query, fetches all results, formats them as strings (one row per line), and returns the formatted results. It also includes error handling for potential SQL execution errors.

**6.1.7 Command Line Argument Parsing and Interactive Loop**

Set up `argparse` to accept the database path and then create an interactive loop for users to ask questions repeatedly.

```python
if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Natural Language to SQL query interface.")
    parser.add_argument("db_path", type=str, help="Path to the SQLite database file.")
    args = parser.parse_args()
    db_path = args.db_path

    database_structure = extract_structure(db_path) # Extract database structure once

    while True: # Interactive loop
        question = input("Enter your question (or 'quit' to exit): ")
        if question.lower() == "quit":
            break

        prompt = create_prompt(question, database_structure) # Create prompt with question and structure
        sql_query = call_llm(prompt) # Get SQL query from LLM
        print(f"Generated SQL Query: {sql_query}") # Print the generated SQL

        if "No SQL query found" not in sql_query and "Error" not in sql_query: # Check if a valid SQL query was generated
             query_result = process_query(db_path, sql_query) # Process the query
             print(f"Query Result:\n{query_result}") # Print the query result
```

This section first parses the database path. Then, it enters an infinite loop (`while True`). Inside the loop, it prompts the user for a question. If the question is "quit", the loop breaks. Otherwise, it creates the prompt, calls the LLM to get the SQL query, prints the generated query, and if a valid SQL query was obtained, it executes the query using `process_query` and prints the results.

**6.1.8 Running the Natural Language to SQL Script**

Save the code as `nl_to_sql.py`. Run it from your terminal, providing the path to your SQLite database file:

```bash
python nl_to_sql.py data/games.db
```

The script will then start prompting you to enter questions. You can ask questions about the data in your database in natural language, and the system will attempt to translate them into SQL, execute the queries, and show you the results. Type "quit" to exit the interactive session.

## Conclusion

This chapter has provided a comprehensive guide to analyzing multimodal data using Large Language Models and Python. We have explored practical implementations for:

*   **Text Classification (Sentiment Analysis):**  Classifying text sentiment as positive or negative using GPT-4 Omni.
*   **Image Question Answering:**  Answering questions about image content and comparing multiple images with GPT-4 Omni.
*   **Audio Transcription:**  Converting speech in audio files to text using the OpenAI Whisper model.
*   **Tabular Data Analysis (Natural Language to SQL):**  Translating natural language questions into SQL queries to analyze tabular data in SQLite databases using GPT-4 Omni.

These examples demonstrate the versatility and power of LLMs in handling diverse data types. By leveraging Python and the OpenAI API, you can build sophisticated data analysis applications and workflows.

To further explore this field, consider visiting the instructor's website (as mentioned in the original transcript) for additional resources, tutorials, and code samples related to multimodal data analysis and Large Language Models. This rapidly evolving field offers vast opportunities for innovation and problem-solving across various domains.

