# Chatbot with Flask Web Interface

This project demonstrates how to set up a back-end server using Flask to host a chatbot built with the Hugging Face Transformers library. It also includes a simple front-end web page that communicates with the chatbot, creating a complete, interactive web application.

The backend receives prompts from the user via the web interface, processes them with the `facebook/blenderbot-400M-distill` model, and returns the generated response to be displayed on the webpage.

## ✨ Key Features

- **Backend Server**: A simple and robust backend built with Flask to handle API requests.
- **Chatbot Integration**: Utilizes the `AutoModelForSeq2SeqLM` and `AutoTokenizer` from Hugging Face Transformers to power the conversation.
- **Web Interface**: A pre-built HTML, CSS, and JavaScript template for a clean chat interface.
- **API Endpoint**: A `/chatbot` endpoint that accepts POST requests with a JSON payload and returns the bot's response.
- **CORS Handling**: Includes `flask_cors` to manage Cross-Origin Resource Sharing, allowing the front-end and back-end to communicate smoothly.

## 🚀 Getting Started

Follow these instructions to get the project running on your local machine.

### Prerequisites

- Python 3.x
- pip (Python package installer)
- git

### Setup and Installation

1.  **Clone the template repository which contains the front-end files:**

    ```bash
    git clone [https://github.com/ibm-developer-skills-network/LLM_application_chatbot](https://github.com/ibm-developer-skills-network/LLM_application_chatbot)
    cd LLM_application_chatbot
    ```

2.  **Install all the required Python libraries:**
    The project requires Flask, Flask-Cors, Transformers, and Torch.

    ```bash
    pip install flask flask_cors transformers==4.38.2 torch==2.2.1
    ```

- `flask` and `flask_cors` for the web server.
- `transformers` and `torch` for the chatbot model.

3.  **Create the Flask Application (`app.py`):**
    Create a file named `app.py` inside the `LLM_application_chatbot` directory. Copy and paste the final Python code from the "Final version of your flask app" section of the guide into this file. Your application should be able to:

- Initialize the Flask app and CORS.
- Load the pre-trained model and tokenizer.
- Define a route `/` to render the `index.html` front-end page.
- Define the `/chatbot` endpoint to handle POST requests and return the bot's response.

  Additional details about the included `app.py` (for clarity):

  - Location: The tutorial expects `LLM_application_chatbot/app.py`. If this repository contains a top-level `app.py` file already, you can copy that file into the `LLM_application_chatbot/` folder (or move it) so the front-end and back-end live together.

  - What the example `app.py` does:

    - Imports `Flask`, `flask_cors.CORS`, `json` and Hugging Face `transformers` (`AutoModelForSeq2SeqLM`, `AutoTokenizer`).
    - Loads the pre-trained model `facebook/blenderbot-400M-distill` and its tokenizer on startup.
    - Maintains a simple in-memory `conversation_history` list to provide basic context between turns (note: this is ephemeral — it resets when the server restarts).
    - Exposes a GET route `/` that renders the chat front-end (`templates/index.html`).
    - Exposes a POST route `/chatbot` that expects a JSON payload like `{ "prompt": "Hello" }`, tokenizes the prompt (optionally including the conversation history), generates a reply with the model, updates `conversation_history`, and returns the generated text as a plain response.

  - Run instructions (from inside the `LLM_application_chatbot` folder):

    1. Ensure dependencies are installed (see the Setup and Installation section above).
    2. Either run with Flask's CLI:

       export FLASK_APP=app.py
       flask run

       Or run directly with Python:

       python3 app.py

    3. By default, the server will be available at `http://127.0.0.1:5000/` and the front-end will send requests to `http://127.0.0.1:5000/chatbot`.

  - Quick curl example (test the chatbot endpoint):

    curl -X POST -H "Content-Type: application/json" -d '{"prompt":"Hello, how are you?"}' http://127.0.0.1:5000/chatbot

  - Important notes:
    - `conversation_history` is stored in memory and is not safe for multi-user production use. For persistent or multi-user scenarios, store conversations per-session or in a database.
    - Loading large transformer models requires sufficient memory (GPU recommended for reasonable latency). For development, smaller or distilled models work better.

4.  **Configure the Front-End Endpoint:**

- Open the file `static/script.js`.
- Find the line that defines the `url` constant (initially set to `www.example.com`).
  - Change this URL to your Flask server's chatbot endpoint. If running locally, this will be:
    ```javascript
    const url =
      "[http://127.0.0.1:5000/chatbot](http://127.0.0.1:5000/chatbot)";
    ```

### Running the Application

1.  **Start the Flask Server:**
    Open your terminal, navigate to the `LLM_application_chatbot` directory, and run the following command:

    ```bash
    flask run
    # Or alternatively: python3 app.py
    ```

You should see output indicating the server is running on `http://127.0.0.1:5000`.

2.  **Access the Web Interface:**
    Open your web browser and go to the following address:
    ```
    [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
    ```
    You should now see the chatbot web interface and be able to interact with your bot.

## 🛠️ Technologies Used

- **Backend**: Python, Flask
- **Machine Learning**: PyTorch, Hugging Face Transformers (`facebook/blenderbot-400M-distill`)
- **Frontend**: HTML, CSS, JavaScript
