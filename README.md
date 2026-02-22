# SafeSpace AI Therapist

SafeSpace is an AI-powered mental health support assistant. It provides empathetic conversational support, can suggest nearby therapists, and includes an emergency escalation pathway for high-risk situations.

## What This Project Does

- Accepts user messages from a chat UI.
- Runs an AI agent that decides whether to:
  - provide therapeutic-style conversational support,
  - find nearby therapists based on location,
  - trigger an emergency call workflow for crisis scenarios.
- Returns the final response (and tool usage) back to the frontend.

## How It Works (High-Level)

1. User sends a message from the Streamlit frontend.
2. FastAPI backend receives the message at `/ask`.
3. A LangGraph ReAct agent processes the message with available tools.
4. The backend returns the generated response to the frontend.

## Tech Stack

### Backend
- Python 3.11+
- FastAPI + Uvicorn
- Pydantic

### AI / Agent Orchestration
- LangChain
- LangGraph (ReAct agent)
- Groq (via `langchain-groq`) for agent LLM routing
- Ollama with `alibayram/medgemma:4b` for therapist-style responses

### Integrations
- Twilio (emergency call trigger)
- Google Maps API (`googlemaps` client) for therapist discovery

### Frontend
- Streamlit
- Requests (frontend-to-backend API calls)

### Dependency / Env Management
- `uv` + `uv.lock`

## Key Files

- `frontend.py`: Streamlit chat interface
- `backend/main.py`: FastAPI app and endpoints
- `backend/ai_agent.py`: Agent + tool wiring and response parsing
- `backend/tools.py`: MedGemma query + Twilio emergency call logic
- `backend/config.py`: API keys and runtime config values

## Quick Start

```bash
uv sync
```

Then run backend and frontend in separate terminals:

```bash
uv run python backend/main.py
uv run streamlit run frontend.py
```

## Configuration

Set required credentials in `backend/config.py` (or migrate to environment variables):

- `GROQ_API_KEY`
- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`
- `TWILIO_FROM_NUMBER`
- `EMERGENCY_CONTACT`
- `GOOGLE_MAPS_API_KEY`

## Safety Note

This project is a support tool, not a replacement for licensed medical care. In emergencies, contact local emergency services immediately.
