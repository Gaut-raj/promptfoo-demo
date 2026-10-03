# FastAPI + Promptfoo demo

Uses free local `llama3.2:3b` through Ollama for the app, test grading,
and attack generation. No paid API calls or API key are needed.

Install [Ollama](https://ollama.com/download/windows), then download the model:

```sh
ollama pull llama3.2:3b
```

Keep Ollama running. Your existing `.env` now points to the local server.

Start the API in one terminal:

```sh
python -m pip install -r requirements.txt
python -m uvicorn app:app --port 8000
```

In another terminal:

```sh
curl -s http://localhost:8000/chat -H 'Content-Type: application/json' -d '{"prompt":"What is the annual management fee?"}'
npx promptfoo@0.123.1 eval --no-cache -j 1
npx promptfoo@0.123.1 redteam run --no-cache -j 1
npx promptfoo@0.123.1 view
```

For the five-minute walkthrough: show the endpoint, run the tests, open a real
security failure in the dashboard, edit `SYSTEM_PROMPT` or add a small guardrail
in `app.py`, restart the API, and replay the same generated attacks:

```sh
npx promptfoo@0.123.1 eval -c redteam.yaml --no-cache -j 1
```

Generate and review attacks before presenting. A failure is not guaranteed;
connection or grader errors do not count as security findings.
`prompt-injection` is Promptfoo's legacy strategy name; the required
`pii:session` and `contracts` checks are plugins.
