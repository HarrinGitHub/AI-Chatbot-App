# AI Chatbot App

A simple full-stack AI chatbot: a Node/Express backend that calls the Anthropic Claude API, and a lightweight HTML/CSS/JS frontend chat UI.

```
ai-chatbot-app/
├── backend/
│   ├── server.js         # Express server + Claude API integration
│   ├── package.json      # Backend dependencies
│   └── .env.example      # Copy to .env and add your API key
└── frontend/
    ├── index.html         # Chat UI markup
    ├── style.css          # Chat UI styling
    └── script.js          # Chat logic (talks to backend)
```

## 1. Prerequisites

- [Node.js](https://nodejs.org/) v18 or later
- An Anthropic API key — get one at https://console.anthropic.com/settings/keys

## 2. Backend setup

```bash
cd backend
npm install
cp .env.example .env
```

Open `.env` and paste in your API key:

```
ANTHROPIC_API_KEY=sk-ant-xxxxxxxx
```

Start the server:

```bash
npm start
```

You should see:

```
✅ Backend server running at http://localhost:3001
```

## 3. Frontend setup

No build step needed — it's plain HTML/CSS/JS. Just open `frontend/index.html` in your browser, or serve it locally for a smoother experience:

```bash
cd frontend
npx serve .
```

Then visit the URL it gives you (usually `http://localhost:3000`).

## 4. Try it out

Type a message in the chat box and hit Send. The frontend calls the backend's `/api/chat` endpoint, which forwards the conversation to Claude and streams back a reply.

## How it works

- **Frontend** keeps the running conversation in a JS array and POSTs it to the backend on every new message.
- **Backend** (`server.js`) receives the messages, forwards them to the Anthropic Messages API using the official `@anthropic-ai/sdk`, and returns the reply as JSON.
- Your API key never touches the browser — it stays server-side in `.env`, which is git-ignored.

## Next steps / ideas to extend this

- Add streaming responses (Server-Sent Events) instead of waiting for the full reply
- Persist conversation history to a database
- Add user authentication
- Deploy backend to a service like Render/Fly.io and frontend to Vercel/Netlify
- Swap the vanilla JS frontend for React if you want more structure

## Troubleshooting

- **"could not reach the server"** — make sure the backend is running on port 3001.
- **401/403 errors** — double check your `ANTHROPIC_API_KEY` in `.env`.
- **CORS errors** — the backend already has `cors()` enabled for all origins; make sure you're hitting `http://localhost:3001` and not a typo'd port.
