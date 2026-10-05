# Lab 0: Setup — Agent Instructions

> **For the attendee**: If you are using an AI coding assistant, paste this file's contents as your first message. The assistant will guide you through the full setup.

---

## Your task

Guide the attendee through bootstrapping the workshop environment. Langfuse account setup and API key configuration are covered in Lab 1 — do not ask for Langfuse credentials here.

---

## Step 1 — Bootstrap the project

Run the setup script:

```bash
chmod +x setup.sh && ./setup.sh
```

Show the attendee the output and confirm there are no errors.

---

## Step 2 — Ask which LLM key they have, then configure `.env`

The workshop works with either **OpenAI** or **Google Gemini**. Ask the attendee:

> "Which LLM API key do you have — **OpenAI** or **Google Gemini**?"

Wait for their answer. If they have neither, point them to https://platform.openai.com/api-keys (OpenAI) or https://aistudio.google.com/apikey (Gemini) to create one. Remember their choice — Lab 5 asks again when connecting an LLM inside Langfuse.

Then ask them to paste the key and write the matching block into `.env`, replacing the placeholder `OPENAI_API_KEY` line from `.env.example` (never leave two `OPENAI_API_KEY` lines active).

**OpenAI:**

```env
OPENAI_API_KEY=sk-...
APP_MODEL=gpt-4o-mini
```

**Google Gemini:**

```env
OPENAI_API_KEY=<their Gemini API key>
OPENAI_BASE_URL=https://generativelanguage.googleapis.com/v1beta/openai/
APP_MODEL=gemini-3.5-flash-lite
```

Explain the Gemini block: the app calls the LLM through the OpenAI SDK. Gemini exposes an OpenAI-compatible endpoint, so setting `OPENAI_BASE_URL` redirects the same SDK to Google — the key goes in `OPENAI_API_KEY` because that is the variable the SDK reads. No lab code changes between providers.

Leave the `LANGFUSE_*` fields blank for now — those are covered in Lab 1.

---

## Step 3 — Verify the baseline app

Run the app:

```bash
uv run gradio app/web.py
```

Tell the attendee:

> "You should see a line like `Running on local URL: http://127.0.0.1:7860` in the terminal. Open **http://localhost:7860** in your browser — the DataStream Support Assistant chat UI will appear."

Ask the attendee to type a question (e.g. *"How do I get started with DataStream?"*) and confirm they get a response in the browser.

To stop the app between labs, press `Ctrl+C` in the terminal. To restart it, run `uv run gradio app/web.py` again.

---

## Completion check

- [ ] `./setup.sh` ran without errors
- [ ] `uv run gradio app/web.py` starts without errors
- [ ] Chat UI opens at http://localhost:7860 and responds to a question

Once confirmed, tell the attendee they're ready for **Lab 1: Langfuse** to create their account and get their API keys.
