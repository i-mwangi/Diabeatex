# Diabeatex

Diabeatex is an interactive web app built with Streamlit to support diabetes management. It includes an AI chatbot (powered by LangFlow/OpenAI) for queries, a food helper that analyzes meal images (via URL) to estimate glycemic index and offer advice, and a section for viewing glucose statistics.

## Features

*   **AI Assistant:** Chat with an AI powered by LangFlow and OpenAI models. Interact via text or voice (uses OpenAI Whisper for Speech-to-Text and AIMLAPI for Text-to-Speech).
*   **Food Helper:** Provide a URL to an image of your meal. The app uses GPT-4o vision via AIMLAPI to analyze the food, estimate its glycemic index, and offer dietary suggestions.
*   **Statistics:** View visualizations of blood glucose data (currently uses sample data).
*   **Interactive UI:** Built with Streamlit for a user-friendly web interface.

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/i-mwangi/Diabeatex.git
    cd Diabeatex/Healthpath
    ```
2.  **Create and activate a virtual environment (Recommended):**
    ```bash
    # Windows
    python -m venv venv
    venv\Scripts\activate

    # macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

## Configuration

1.  **OpenAI API Key:**
    *   Create a `.streamlit` directory if it doesn't exist: `mkdir .streamlit`
    *   Create a secrets file: `.streamlit/secrets.toml`
    *   Add your OpenAI API key to the file:
        ```toml
        [openai]
        api_key="YOUR_OPENAI_API_KEY"
        ```
    *   Replace `YOUR_OPENAI_API_KEY` with your actual key.

2.  **AIMLAPI Key:**
    *   The application currently uses a hardcoded key for AIMLAPI services (TTS, Image Analysis) in `app.py`.
    *   **Recommendation:** For better security, modify `app.py` to read this key from `secrets.toml` or environment variables instead.
        *   If using secrets, add it to `.streamlit/secrets.toml`:
            ```toml
            [aimlapi]
            api_key="YOUR_AIMLAPI_KEY"
            ```
        *   Then update the relevant `requests` calls in `app.py` to use `st.secrets["aimlapi"]["api_key"]`.

3.  **LangFlow Flows:**
    *   The application expects specific LangFlow JSON files (e.g., `Memory_Chatbot.json`, `AIML_API_RAG_LANGFLOW.json`) to be present in the main directory.

## Running Locally

Once dependencies are installed and secrets are configured:

```bash
streamlit run app.py
```

This will start the Streamlit server and open the application in your default web browser.

## Deployment

*   **Streamlit Community Cloud:** The easiest way to deploy. Push your code (ensure `secrets.toml` is in `.gitignore` if you commit the `.streamlit` folder) to GitHub and deploy via [share.streamlit.io](https://share.streamlit.io/). Configure secrets directly in the Streamlit Cloud interface.
*   **Other Platforms (AWS, GCP, Azure, Heroku):** Containerize the application using Docker (see example `Dockerfile` in deployment instructions or comments) and deploy according to the platform's Python/Docker app deployment guides. Manage secrets using environment variables on the platform.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.