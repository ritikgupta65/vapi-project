
<img width="1535" height="695" alt="image" src="https://github.com/user-attachments/assets/beaa03dc-f9a0-478c-ba92-1cfc2304d3ea" />

<img width="1532" height="682" alt="image" src="https://github.com/user-attachments/assets/8532bc7a-9368-4c35-9860-536cffb13046" />

<img width="1522" height="631" alt="image" src="https://github.com/user-attachments/assets/fe5f540d-dbc5-4bbf-81e6-37305506152f" />

<img width="1517" height="680" alt="image" src="https://github.com/user-attachments/assets/92fe1100-ffaf-42f0-893b-3990cab4cf1b" />


# Speech-to-Speech Conversational AI System

A production-ready, real-time voice conversation system with Speech-to-Text (STT), Large Language Model (LLM), and Text-to-Speech (TTS) integration.

## 🎯 Features

- **Real-time voice conversation** with turn-by-turn interaction
- **Barge-in support** - interrupt the AI while it's speaking
- **Streaming responses** - AI starts speaking before completing its thought
- **Live transcripts** - see the conversation unfold in real-time
- **Pluggable architecture** - easily swap STT/TTS providers
- **Clean APIs** - reusable in any project
- **Modern UI** - built with React, TypeScript, and Tailwind CSS

## 🏗️ Architecture

### Backend (Python + FastAPI)

The backend is organized into 4 modular layers:

1. **STT Layer** (`stt_layer.py`)
   - Deepgram WebSocket streaming
   - Partial and final transcripts
   - Automatic silence detection
   - Voice activity detection (VAD)

2. **Conversation Orchestrator** (`orchestrator.py`)
   - State machine: LISTENING → THINKING → SPEAKING
   - Turn-taking management
   - Barge-in handling (user can interrupt AI)
   - Conversation history maintenance

3. **LLM Layer** (`llm_layer.py`)
   - OpenAI/Azure OpenAI integration
   - Streaming responses
   - Voice-optimized system prompts

4. **TTS Layer** (`tts_layer.py`)
   - Pluggable providers: Deepgram, ElevenLabs, OpenAI
   - Streaming audio synthesis
   - Sentence-by-sentence output
   - Immediate interruption support

### Frontend (React + TypeScript)

- **Web Audio API** for microphone access and audio playback
- **WebSocket connections** for real-time communication
- **Modern UI** with Tailwind CSS
- **Responsive design** for all screen sizes

## 📦 Installation

### Prerequisites

- Python 3.14+ (backend)
- Node.js 18+ (frontend)
- API Keys:
  - OpenAI API key
  - Deepgram API key
  - (Optional) ElevenLabs API key

### Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements_flask.txt

# Copy environment file
cp .env.example .env

# Edit .env and add your API keys
# Required: OPENAI_API_KEY, DEEPGRAM_API_KEY
```

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# (Optional) Create .env file for custom API URL
echo "VITE_API_URL=http://localhost:8000" > .env
```

## 🚀 Running the Application

### Start project

```bash
python app_working.py
```

project will run on `http://localhost:3000/dashboard`

## ⚙️ Configuration

### Backend Configuration

Edit `backend/.env`:

```bash
# OpenAI / Azure OpenAI
OPENAI_API_KEY=your_key_here
OPENAI_MODEL=gpt-4o-mini

# Deepgram
DEEPGRAM_API_KEY=your_key_here

# ElevenLabs (optional)
ELEVENLABS_API_KEY=your_key_here
ELEVENLABS_VOICE_ID=21m00Tcm4TlvDq8ikWAM

# TTS Provider: deepgram, elevenlabs, or openai
TTS_PROVIDER=deepgram

# Server
HOST=0.0.0.0
PORT=8000
```



### Adjust LLM Model

Set `OPENAI_MODEL` in `backend/.env`:
- `gpt-4o-mini` - Fast and cost-effective
- `gpt-4o` - Higher quality
- Any OpenAI-compatible model

## 🛠️ Development

### Project Structure

```
.
├── backend/
│   ├── main.py                 # FastAPI app and WebSocket handlers
│   ├── config.py               # Configuration management
│   ├── models.py               # Pydantic models
│   ├── stt_layer.py            # Speech-to-Text layer
│   ├── llm_layer.py            # LLM integration
│   ├── tts_layer.py            # Text-to-Speech layer
│   ├── orchestrator.py         # Conversation orchestrator
│   ├── requirements.txt        # Python dependencies
│   └── .env.example            # Environment variables template
│
└── frontend/
    ├── src/
    │   ├── App.tsx             # Main application component
    │   ├── main.tsx            # Entry point
    │   ├── types.ts            # TypeScript types
    │   ├── api.ts              # API client
    │   ├── audioManager.ts     # Audio handling
    │   └── components/         # React components
    │       ├── MessageBubble.tsx
    │       ├── MicButton.tsx
    │       └── TranscriptPanel.tsx
    ├── package.json
    ├── vite.config.ts
    ├── tailwind.config.js
    └── tsconfig.json
```

