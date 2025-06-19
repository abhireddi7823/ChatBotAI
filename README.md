# Gemini AI Assistant (Command Line Version)

This is a simple Python-based chatbot that uses **Google Gemini AI (via the `google-generativeai` API)** to respond to user input.

##Features

- Uses `gemini-1.5-flash` model
- Handles API securely via `.env` file
- Keeps chatting until you type `quit`
- Graceful error handling


## Requirements

Install these Python libraries:

pip install google-generativeai python-dotenv

##Setup Your .env File

Create a file named .env in the same folder as your Python file. Add your Gemini API key:

GOOGLE_API_KEY=your_actual_api_key_here

How to Run

python assistant.py  or  uv run main.py


How It Works — Line-by-Line Explanation
1. Import Required Libraries

import os
import google.generativeai as genai
from dotenv import load_dotenv

os: For reading environment variables like the API key.
google.generativeai: Google's library to use Gemini models.
dotenv: To load environment variables from a .env file.

2. Load the API Key from .env File

load_dotenv()
api_key = os.getenv("GOOGLE_API_KEY")
Loads the key from .env and stores it in api_key.

3. Check if Key is Present

if not api_key:
    print("ERROR: GOOGLE_API_KEY not found in .env file.")
    exit()
Stops the program if the key isn't found.

4. Configure the Gemini API

genai.configure(api_key=api_key)
Tells the Gemini library to use your key.

5. Create a Model Instance

model = genai.GenerativeModel("gemini-1.5-flash")
Initializes the AI chatbot using Gemini's gemini-1.5-flash model.

6. Start the Chatbot Loop

print("Welcome to Gemini AI Assistant! Type 'quit' to exit.")
Prints a friendly welcome message.
while True:
    user_input = input("You: ")
Repeats asking the user for input until they type "quit".

    if user_input.lower() == "quit":
        break
Exits the loop when the user wants to stop chatting.

7. Send User Input to Gemini

    try:
        response = model.generate_content(user_input)
        print("Gemini:", response.text)
Sends your question to Gemini and prints the reply.

8. Error Handling

    except Exception as e:
        print("Error:", e)
If anything goes wrong (e.g., no internet or bad API key), it shows the error instead of crashing.

Example

Welcome to Gemini AI Assistant! Type 'quit' to exit.
You: Tell me a joke
Gemini: Why don’t scientists trust atoms? Because they make up everything!
