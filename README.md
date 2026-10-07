🤖 Qnexa AI

Qnexa AI is an intelligent, ChatGPT-style conversational AI chatbot built with LangChain, LangGraph, Groq, Google Serper, and Streamlit.

It can answer questions, maintain conversational context across messages, and use Google Search when up-to-date information is required.

Ask anything. Get intelligent answers.

⸻

✨ Features

* 💬 Conversational AI — Chat naturally with the AI assistant.
* 🧠 Conversation Memory — Understands follow-up questions using previous conversation context.
* 🔎 Google Search — Can search the web for current and real-time information.
* ⚡ Streaming Responses — AI responses appear progressively as they are generated.
* 🤖 Groq-powered LLM — Uses Groq for fast AI inference.
* 🦜 LangChain Agent — Uses LangChain’s agent framework to coordinate the LLM and tools.
* 🕸️ LangGraph Checkpointing — Maintains agent conversation state.
* 🎨 Streamlit UI — Simple and interactive chat interface.
* 🔐 Environment Variables — API keys are loaded securely using .env.

⸻

🛠️ Tech Stack

Technology	Purpose
Python	Core programming language
LangChain	AI agent framework
LangGraph	Agent state and memory
Groq	LLM inference
Google Serper	Web search
Streamlit	Frontend / chat interface
python-dotenv	Environment variable management
uv	Python package and environment management

⸻

📁 Project Structure

QNA CHATBOT/
│
├── qna_chatbot.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md

⸻

⚙️ Installation

1. Clone the repository

git clone <YOUR_GITHUB_REPOSITORY_URL>
cd "QNA CHATBOT"

2. Install dependencies

This project uses uv for dependency management.

uv add langchain langgraph langchain-groq langchain-community python-dotenv streamlit

Or, if you already have a requirements.txt:

uv add -r requirements.txt

⸻

🔑 Environment Variables

Create a .env file in the project root:

GROQ_API_KEY=your_groq_api_key
SERPER_API_KEY=your_serper_api_key

API Keys

You need:

* Groq API Key — for the LLM.
* Serper API Key — for Google Search.

Never commit your .env file to GitHub.

⸻

🚫 .gitignore

Make sure your .gitignore contains:

.env
.venv/
__pycache__/
*.pyc
.DS_Store

⸻

▶️ Running the Application

Start the Streamlit application using uv:

uv run streamlit run qna_chatbot.py

Using uv run ensures that the application runs with the project’s installed dependencies.

The application will open in your browser at the local Streamlit address.

⸻

🧠 How It Works

The basic architecture of Qnexa AI looks like this:

                    ┌──────────────────┐
                    │   User Question  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │    Streamlit     │
                    │    Chat UI       │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ LangChain Agent  │
                    └────────┬─────────┘
                             │
                    ┌────────┴────────┐
                    │                 │
                    ▼                 ▼
             ┌─────────────┐   ┌──────────────┐
             │  Groq LLM   │   │ Google Search│
             └─────────────┘   └──────────────┘
                    │                 │
                    └────────┬────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  AI Response     │
                    │    Streaming     │
                    └──────────────────┘

⸻

🧠 Conversation Memory

Qnexa AI uses LangGraph’s checkpointing system to maintain conversation state.

A thread ID is used to identify the conversation:

{
    "configurable": {
        "thread_id": "1"
    }
}

This allows the agent to understand contextual follow-up questions.

Example

User:

Who is Narendra Modi?

Qnexa AI:

Narendra Modi is the Prime Minister of India…

User:

How old is he?

The agent can understand that “he” refers to Narendra Modi based on the previous conversation.

⸻

🔎 Web Search

Qnexa AI can use Google Search through Google Serper.

The search tool is connected to the LangChain agent:

search = GoogleSerperAPIWrapper()
tools = [search.run]

The agent can decide when web search is useful, particularly for information that may have changed recently.

⸻

⚡ Streaming Responses

Instead of waiting for the complete response, Qnexa AI streams the generated response to the interface:

response = agent.stream(
    {
        "messages": [
            {
                "role": "user",
                "content": query
            }
        ]
    },
    {
        "configurable": {
            "thread_id": "1"
        }
    },
    stream_mode="messages"
)

This creates a more responsive chatbot experience.

⸻

📌 Example Questions

Try asking:

What is artificial intelligence?
Explain LangChain in simple terms.
Who is the Prime Minister of India?
What are the latest AI developments?
Who is PM Modi?

Followed by:

How old is he?

⸻

🚀 Future Improvements

Some planned improvements for Qnexa AI:

* Multiple conversation threads
* New Chat button
* Chat history sidebar
* User authentication
* Persistent database-backed memory
* File/PDF upload and Q&A
* Voice input
* Voice output
* Markdown/code rendering improvements
* Better web-search citations
* Custom system prompts
* Model selection
* Dark/light theme
* Deployment to Streamlit Cloud

⸻

🔒 Security

Do not expose API keys in your source code.

❌ Don’t do this:

groq_api_key = "my-secret-api-key"

✅ Use environment variables:

from dotenv import load_dotenv
load_dotenv()

And store your credentials in .env:

GROQ_API_KEY=your_key
SERPER_API_KEY=your_key

