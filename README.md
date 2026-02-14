# Triple Synth

**Role Separation × Model-Specific Formatting × Multi-AI Synthesis**

A single HTML file that generates structured prompts for running multi-AI debates across ChatGPT, Claude, and Gemini — no API keys, no subscriptions, no installs.

[**→ Try it now**](https://Simmon-Gomi.github.io/triple-synth/) ·  [日本語版](https://Simmon-Gomi.github.io/triple-synth/ja/)

---

## What it does

Most people who use multiple AIs just ask the same question three times. Triple Synth adds structure to that workflow:

1. **Role assignment** — Assign each AI a role (Proposer / Critic / Judge) or leave it open
2. **Model-specific prompts** — Generates prompts formatted for each model's strengths (XML tags for Claude, Markdown headers for ChatGPT, context-first for Gemini)
3. **Synthesis** — After pasting all 3 responses back, generates a prompt that integrates them into a single final answer
4. **Dialectic critique** — Alternatively, generates a prompt that finds holes and blind spots for another round of debate

## Why copy-paste instead of API?

Deliberate design choice:

- **Zero setup** — No API keys, no Python, no tokens to manage. Open the HTML, start using it
- **Use each AI's full power** — ChatGPT's web browsing, Claude's extended thinking, Gemini's grounding — none of these work through third-party API wrappers
- **No additional cost** — Works with the subscriptions you already have
- **Your data stays in each provider's standard interface** — No third-party middleman

## Workflow

```
┌─────────────┐
│  Enter topic │
│  Assign roles│
└──────┬──────┘
       │  Generate prompt (×3)
       ▼
┌──────────────────────────────────┐
│  ChatGPT    Claude      Gemini   │
│  (Proposer) (Critic)    (Judge)  │
└──────┬─────────┬─────────┬──────┘
       │  Paste responses back
       ▼
┌─────────────────┐     ┌──────────────────┐
│   Synthesize    │ or  │    Dialectic      │
│  (final answer) │     │  (find holes →    │
│                 │     │   another round)  │
└─────────────────┘     └──────────────────┘
       │
       ▼  Paste into any AI's NEW chat
```

## Quick Start

**Option A: Use online** — Visit the [demo link](https://YOUR_USERNAME.github.io/triple-synth/)

**Option B: Use locally** — Download `index.html`, open in any browser. That's it.

**On iPhone** — Open the URL in Safari → Share button → "Add to Home Screen"

## File Structure

```
triple-synth/
├── index.html      ← English version (default)
├── ja/
│   └── index.html  ← Japanese version
└── README.md
```

## Background

When you ask the same question to ChatGPT, Claude, and Gemini, you typically get three polite, overlapping answers. The real value of using multiple AIs isn't getting three answers — it's making them **disagree productively**.

Research on multi-agent debate (Du et al. 2023, Liang et al. 2024) shows that assigning distinct roles and forcing structured critique significantly reduces hallucination and improves reasoning quality. But existing implementations require Python, API keys, and framework knowledge (LangChain, CrewAI, AutoGen).

Triple Synth brings the same principle to anyone who can open a browser.

## License

MIT
