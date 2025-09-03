# Telegram_Movie_Sentient

# n8n Movie Bot with 2-Step AI

This repository contains an n8n workflow for a sophisticated Telegram movie bot. The bot can understand natural language requests, fetch real-time movie data, and provide witty, in-character responses. It also includes a daily rate-limiting system for users.

<img width="2198" height="756" alt="image" src="https://github.com/user-attachments/assets/ae2dfd67-dfa6-471d-a127-b7b6f0bc03fb" />


## Features

-   **Natural Language Understanding:** Ask for movies, recommendations, or actor filmographies in plain English.
-   **Real-Time Data:** Uses The Movie Database (TMDb) API to access up-to-date movie information, including new releases.
-   **Two-Step AI Process:**
    1.  An initial AI call translates the user's request into a structured API command.
    2.  A second AI call takes the fetched data and crafts a creative, personalized response.
-   **In-Character Persona:** The bot responds as "Dobby by Sentient," adding fun facts and trivia to its answers.
-   **User Rate Limiting:** Built-in logic using Google Sheets to limit users to 3 free messages per day.

## How It Works

1.  **Telegram Trigger:** The workflow starts when a user sends a message to the Telegram bot.
2.  **Rate Limiting (Google Sheets):** It checks a Google Sheet to see if the user has exceeded their daily message limit.
3.  **AI Logic Step (HTTP Request):** The user's message is sent to a Fireworks.ai model (Dobby) with a detailed prompt, instructing it to return a JSON object with the correct TMDb API endpoint and parameters.
4.  **API Call Step (Code Node):** This node parses the JSON from the AI, handles the multi-step logic (e.g., finding an actor's ID first), and calls the TMDb API to get the movie data.
5.  **AI Creative Step (HTTP Request):** The structured data from the TMDb API is sent back to the Dobby model with a new prompt, asking it to generate a fun, natural language response.
6.  **Telegram Sender:** The final, witty response is sent back to the user.

## Setup Instructions

1.  **Download the Workflow:** Download the `MovieBotWorkflow.json` file from this repository.
2.  **Import into n8n:** Open your n8n canvas and import the downloaded JSON file.
3.  **Configure Credentials:** n8n will prompt you to connect credentials for the following nodes:
    -   **Telegram Trigger / Telegram Sender:** Connect your Telegram Bot account.
    -   **Google Sheets Nodes:** Authenticate your Google account.
    -   **HTTP Request Nodes:** Connect your HTTP Header Auth credentials for the Fireworks.ai API.
4.  **Set Up Google Sheet:**
    -   Create a new Google Sheet.
    -   In the first row, create three columns: `UserID`, `MessageCount`, and `Date`.
    -   In the three Google Sheets nodes, replace `YOUR_GOOGLE_SHEET_ID_HERE` with your new sheet's ID.
5.  **Add TMDb API Key:**
    -   Open the **Code1** node.
    -   Replace the placeholder `'YOUR_TMDB_API_KEY_HERE'` with your actual V3 API key from [The Movie Database](https://www.themoviedb.org/settings/api).
6.  **Activate the Workflow:** Save and activate the workflow.

Your movie bot is now ready to use!
