# Exercise SILENT MERIDIAN - Degraded-Comms Decision Trainer (SIH PS 26248)

Fictional, browser-only prototype. React + Vite + Tailwind. No backend, no API keys, no paid services.

## Run
    npm install
    npm run dev          # http://localhost:5173
    npm test             # logic + AI client tests
    npm run build && npm run preview

## Real AI in the Assist chatbot (free)
    cp .env.example .env     # then edit .env
- **Gemini free tier:** get a key at https://aistudio.google.com/apikey, set `VITE_GEMINI_API_KEY`. Model defaults to `gemini-flash-latest` (change `VITE_GEMINI_MODEL` if Google renames it). Free-tier limits apply and Google may use free-tier inputs to improve its products, so never type real or sensitive data.
- **Ollama (offline, no key):** install Ollama, run `ollama pull llama3.2`, set `VITE_AI_PROVIDER=ollama`.
- If the AI is missing or fails, the chatbot automatically falls back to the built-in rules.
- Keys in `VITE_*` variables are visible in the browser bundle. For a public site use the proxy below.

## Deploy as a website (free)
1. Push the folder to GitHub, import it in Vercel (or Netlify). Build command `npm run build`, output `dist`.
2. In the host dashboard set `GEMINI_API_KEY` (server side) and the env var `VITE_AI_PROVIDER=proxy`.
3. `api/chat.js` forwards chat requests, so the key never reaches the browser.

## Demo accounts (password: pass123)
- `trainee`    Lt. Arjun Menon
- `instructor` Cdr. Meera Iyer (also sees the Instructor dashboard)
Demo only: credentials live in `src/data.js`; this is not real authentication.

## Files
- `src/data.js`   scenario, reports, decisions, channels, users (edit content here)
- `src/logic.js`  pure simulation logic (delivery states, scoring, AAR, CSV, fallback bot rules)
- `src/ai.js`     AI client (Gemini / Ollama / proxy)
- `api/chat.js`   optional serverless proxy
- `src/App.jsx`   UI
- `tests/logic.test.mjs`

## Demo guide (about 3 minutes at 2x)
1. Sign in as `instructor`, read the briefing, press Start scenario.
2. T+00:35 Decision 1: R1 and R2 conflict. Pick an option, write a reason, submit.
3. Ask the team a question (chips) and ask Assist for a hint.
4. T+01:00 jamming starts: channels go amber/red, reports arrive late, team replies slow down.
5. R6 shows "Signal lost": press Request retransmit.
6. Open the Instructor dashboard: timeline, decision windows, delivery log. Use "Skip to next decision" to move fast.
7. After the exercise, open After-action review: score, domain breakdown, reasons, feedback. Export JSON/CSV or Print.
8. Refresh the page: your progress is restored (paused). Reset starts over.
