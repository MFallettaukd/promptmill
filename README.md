# promptmill

Batch prompt runner with real rate limiting and retries

Started as a weekend hack, grew on me.

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## What it does

- Progress, token counts and a cost estimate on stderr
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- JSONL in, JSONL out: the input is streamed line by line
- Per-row overrides for model, system, temperature and max_tokens
- Idempotent: ids already in the output are skipped on a rerun
- Failures go to a sidecar file with error type, message and status
- Real rate limiting: sliding windows on requests/min and tokens/min
- A bad input line is logged and skipped, never fatal

## Install

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Project structure

```text
├── docs/
│   ├── development.md
│   ├── faq.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── SECURITY.md
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## Notes

- mostly stable, edge cases remain

## License

MIT. Do whatever you want.
