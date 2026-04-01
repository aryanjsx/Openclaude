<p align="center">
  <strong><code>&gt;_ OpenClaude</code></strong>
</p>

<p align="center">
  Claude Code with <strong>any LLM</strong> — not just Claude.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@aryanjsx/openclaude"><img src="https://img.shields.io/npm/v/@aryanjsx/openclaude?style=flat-square&color=7c3aed&label=npm" alt="npm"></a>
  <a href="https://github.com/aryanjsx/Openclaude"><img src="https://img.shields.io/github/stars/aryanjsx/Openclaude?style=flat-square&color=7c3aed" alt="stars"></a>
  <a href="https://github.com/aryanjsx/Openclaude/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-7c3aed?style=flat-square" alt="license"></a>
  <a href="https://github.com/aryanjsx/Openclaude"><img src="https://img.shields.io/badge/node-%3E%3D20-7c3aed?style=flat-square" alt="node"></a>
</p>

<p align="center">
  <a href="#install">Install</a> &bull;
  <a href="#quick-start">Quick Start</a> &bull;
  <a href="#providers">Providers</a> &bull;
  <a href="#model-guide">Model Guide</a> &bull;
  <a href="#how-it-works">How It Works</a>
</p>

---

Plug in **GPT-4o, DeepSeek, Gemini, Llama, Mistral, Ollama**, or any model that speaks the OpenAI chat completions API. All of Claude Code's tools work — bash, file read/write/edit, grep, glob, agents, tasks, MCP — powered by whatever model you choose.

**200+ compatible models. 15 built-in tools. 786 lines of shim code. Zero extra dependencies.**

## Install

**npm (recommended)**

```bash
npm install -g @aryanjsx/openclaude
```

**From source**

```bash
git clone https://github.com/aryanjsx/Openclaude.git
cd Openclaude
bun install
bun run build
```

**Run directly with Bun (no build step)**

```bash
git clone https://github.com/aryanjsx/Openclaude.git
cd Openclaude
bun install
bun run dev
```

## Quick Start

**1. Set your provider**

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=sk-your-key-here
export OPENAI_MODEL=gpt-4o
```

**2. Launch**

```bash
openclaude
```

That's it. Streaming, tool calling, file editing, multi-step reasoning — everything works through the model you pick. The npm package name is `@aryanjsx/openclaude`, but the CLI command is `openclaude`.

## Providers

<table>
<tr><th>Provider</th><th>Setup</th></tr>
<tr>
<td><strong>OpenAI</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=sk-...
export OPENAI_MODEL=gpt-4o
```

</td>
</tr>
<tr>
<td><strong>DeepSeek</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=sk-...
export OPENAI_BASE_URL=https://api.deepseek.com/v1
export OPENAI_MODEL=deepseek-chat
```

</td>
</tr>
<tr>
<td><strong>Gemini</strong><br><sub>via OpenRouter</sub></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=sk-or-...
export OPENAI_BASE_URL=https://openrouter.ai/api/v1
export OPENAI_MODEL=google/gemini-2.0-flash
```

</td>
</tr>
<tr>
<td><strong>Ollama</strong><br><sub>local, free</sub></td>
<td>

```bash
ollama pull llama3.3:70b
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_BASE_URL=http://localhost:11434/v1
export OPENAI_MODEL=llama3.3:70b
```

</td>
</tr>
<tr>
<td><strong>Together AI</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=...
export OPENAI_BASE_URL=https://api.together.xyz/v1
export OPENAI_MODEL=meta-llama/Llama-3.3-70B-Instruct-Turbo
```

</td>
</tr>
<tr>
<td><strong>Groq</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=gsk_...
export OPENAI_BASE_URL=https://api.groq.com/openai/v1
export OPENAI_MODEL=llama-3.3-70b-versatile
```

</td>
</tr>
<tr>
<td><strong>Mistral</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=...
export OPENAI_BASE_URL=https://api.mistral.ai/v1
export OPENAI_MODEL=mistral-large-latest
```

</td>
</tr>
<tr>
<td><strong>Azure OpenAI</strong></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_API_KEY=your-azure-key
export OPENAI_BASE_URL=https://your-resource.openai.azure.com/openai/deployments/your-deployment/v1
export OPENAI_MODEL=gpt-4o
```

</td>
</tr>
<tr>
<td><strong>LM Studio</strong><br><sub>local</sub></td>
<td>

```bash
export CLAUDE_CODE_USE_OPENAI=1
export OPENAI_BASE_URL=http://localhost:1234/v1
export OPENAI_MODEL=your-model-name
```

</td>
</tr>
</table>

Any provider that exposes an OpenAI-compatible `/v1/chat/completions` endpoint will work.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `CLAUDE_CODE_USE_OPENAI` | Yes | Set to `1` to enable the OpenAI provider |
| `OPENAI_API_KEY` | Yes\* | Your API key (\*not needed for local models) |
| `OPENAI_MODEL` | Yes | Model name (e.g. `gpt-4o`, `deepseek-chat`, `llama3.3:70b`) |
| `OPENAI_BASE_URL` | No | API endpoint (defaults to `https://api.openai.com/v1`) |

`ANTHROPIC_MODEL` can also override the model name. `OPENAI_MODEL` takes priority.

## What Works

| Feature | Status |
|---------|--------|
| All 15 tools (Bash, FileRead, FileWrite, FileEdit, Glob, Grep, WebFetch, WebSearch, Agent, MCP, LSP, NotebookEdit, Tasks) | Fully working |
| Real-time token streaming | Fully working |
| Multi-step tool chains | Fully working |
| Vision (base64 & URL images) | Fully working |
| Slash commands (/commit, /review, /compact, /diff, /doctor) | Fully working |
| Sub-agents (AgentTool) | Fully working |
| Persistent memory | Fully working |

**What's different from the original:**

- No extended thinking mode (OpenAI models use different reasoning approaches)
- No Anthropic prompt caching or beta headers
- 32K default max output tokens (handled gracefully if a model caps lower)

## Model Guide

| Model | Tool Calling | Code Quality | Speed |
|-------|:---:|:---:|:---:|
| GPT-4o | Excellent | Excellent | Fast |
| DeepSeek-V3 | Great | Great | Fast |
| Gemini 2.0 Flash | Great | Good | Very Fast |
| Llama 3.3 70B | Good | Good | Medium |
| Mistral Large | Good | Good | Fast |
| GPT-4o-mini | Good | Good | Very Fast |
| Qwen 2.5 72B | Good | Good | Medium |
| Smaller models (<7B) | Limited | Limited | Very Fast |

For best results, use models with strong function/tool calling support.

## How It Works

The shim (`src/services/api/openaiShim.ts`) is a thin translation layer between Claude Code's Anthropic SDK interface and any OpenAI-compatible API:

```
Claude Code Tool System
        |
  Anthropic SDK interface (duck-typed)
        |
  openaiShim.ts  ← translates formats
        |
  OpenAI Chat Completions API
        |
  Any compatible model
```

**What it translates:**

- Anthropic message blocks &rarr; OpenAI messages
- Anthropic `tool_use` / `tool_result` &rarr; OpenAI function calls
- OpenAI SSE streaming &rarr; Anthropic stream events
- Anthropic system prompt arrays &rarr; OpenAI system messages

Claude Code doesn't know it's talking to a different model.

## Files Changed

```
src/services/api/openaiShim.ts   — OpenAI-compatible API shim (724 lines)
src/services/api/client.ts       — Routes to shim when CLAUDE_CODE_USE_OPENAI=1
src/utils/model/providers.ts     — Added 'openai' provider type
src/utils/model/configs.ts       — Added openai model mappings
src/utils/model/model.ts         — Respects OPENAI_MODEL for defaults
src/utils/auth.ts                — Recognizes OpenAI as valid 3P provider
```

6 files changed. 786 lines added. Zero dependencies added.

## Runtime Hardening

```bash
bun run smoke              # startup sanity check
bun run doctor:runtime     # validate provider env + reachability
bun run hardening:check    # typecheck + smoke + runtime doctor
bun run hardening:strict   # full strict check
```

**Provider launch profiles** save repeated env setup:

```bash
bun run profile:init                                     # auto-detect provider
bun run profile:init -- --provider openai --api-key sk-... # explicit setup
bun run dev:profile                                      # launch from saved profile
bun run dev:openai                                       # OpenAI shortcut
bun run dev:ollama                                       # Ollama shortcut
```

## Origin

Fork of [instructkr/claude-code](https://github.com/instructkr/claude-code), which mirrored the Claude Code source snapshot that became publicly accessible through an npm source map exposure on March 31, 2026. Not affiliated with or endorsed by Anthropic.

## License

MIT. The original Claude Code source is subject to Anthropic's terms. The OpenAI shim additions are public domain.
