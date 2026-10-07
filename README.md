<p align="center">
  <img src="https://img.shields.io/badge/React-19-61dafb" alt="React 19">
  <img src="https://img.shields.io/badge/Vite-6-646cff" alt="Vite">
  <img src="https://img.shields.io/badge/Gemini-2.0%20Flash-4285f4" alt="Gemini 2.0 Flash">
  <img src="https://img.shields.io/badge/status-prototype-orange" alt="Status: prototype">
</p>

# hatable — Visual Vibe Architect

**Describe an app in plain words and get a live, single-page Tailwind prototype back.**

hatable (the app calls itself *Visual Vibe Architect*) is an AI design assistant
for people who do not write code. You type an idea into the chat; Gemini writes a
complete `index.html` — Tailwind for styling, plus a small simulated backend
(`window.app.db`) so buttons and forms behave — and it renders in a live preview
beside the chat.

- **Iterate by talking** — each follow-up edits the current page instead of
  starting over.
- **"I'm feeling lucky"** — generates a random app idea when you are stuck.
- **Download** — save the generated `index.html` and open it anywhere.

It started as a Google AI Studio app.

## Quick start

Requires Node.js and a Gemini API key.

```bash
npm install
echo "GEMINI_API_KEY=your-key-here" > .env.local
npm run dev        # http://localhost:3000
```

| command | does |
|---|---|
| `npm run dev` | dev server on port 3000 |
| `npm run build` | production build |
| `npm run preview` | serve the production build |

## Configuration

- `GEMINI_API_KEY` — your Gemini API key, in `.env.local`. Vite inlines it into
  the client bundle at build time, so do not deploy a build publicly with a
  key you care about.

## How it works

```
chat prompt ──► Gemini 2.0 Flash (JSON schema) ──► full index.html
                                                      └─► sandboxed iframe preview
```

`services/geminiService.ts` holds the system prompt and the two calls
(`generateVibe`, `generateRandomIdea`); `components/ChatInterface.tsx` and
`components/PreviewArea.tsx` are the two halves of the screen.
