# Hi, I'm Artem 👋

I build practical AI agents that work across software, messages, browsers, files, and the computer itself to complete real tasks. In [Cortex](https://github.com/artemgetmann/Cortex), I test whether agents can learn from experience and improve across different kinds of work. [Jarvis](https://github.com/artemgetmann/openclaw) turns these kinds of capabilities into a consumer product for everyday work.

I focus on memory, tool use, approvals, monitoring, and verification: helping agents use new tools, keep working, ask before sensitive actions, and show what they actually did.

📍 Dubai, UAE

![Python](https://img.shields.io/badge/-Python-3572A5?style=flat-square&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Swift](https://img.shields.io/badge/-Swift-F05138?style=flat-square&logo=swift&logoColor=white)
![Bash](https://img.shields.io/badge/-Bash-4EAA25?style=flat-square&logo=gnubash&logoColor=white)
![Linux](https://img.shields.io/badge/-Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![MCP](https://img.shields.io/badge/-MCP-111111?style=flat-square)
![AI Agents](https://img.shields.io/badge/-AI%20Agents-111111?style=flat-square)

## Current Work

- 🧪 [Cortex](https://github.com/artemgetmann/Cortex) - a research prototype testing whether AI agents can learn from past attempts and improve across different tasks using persistent memory. The main unsolved problem is making those gains work reliably beyond one specific task.
- 🧿 [Jarvis](https://github.com/artemgetmann/openclaw) - a distinct, local-first consumer product that helps people delegate real work across their Mac, browser, files, messages, and tools. Its repository began as an OpenClaw fork and still contains substantial inherited code. My work includes Jarvis product decisions and specific changes to tool use, orchestration, reliability, macOS packaging, Telegram, approvals, and verification.
- 🧠 [MindMirror](https://github.com/artemgetmann/mindmirror) - memory infrastructure for AI agents, with an MCP backend, retrieval API, vector storage, and an optional web interface.
- 📈 [MarketMirror](https://github.com/artemgetmann/marketmirror) - AI stock-analysis platform for practical, skeptical fundamental research.

## Selected Technical Evidence

The short version: [experiments, failures, production changes, and what I learned](EVIDENCE.md).

Highlights:

- [Cortex architecture A/B](https://github.com/artemgetmann/Cortex/blob/main/docs/archive/memory-v2-history/AB-FINDINGS.md) - the full design won on a difficult holdout domain, while the simpler design won on the easier domain.
- [Cortex learning ON/OFF](https://github.com/artemgetmann/Cortex/blob/main/tracks/cli_sqlite/reports/2026-03-09_shell_hotfix_hard_onoff_step6_10run.md) - learning improved success from 20% to 50% in one controlled 10-run-per-arm test.
- [Jarvis signed-in browser design](https://github.com/artemgetmann/openclaw/pull/831) - gives the agent a separate copy of the user's chosen Chrome account, preserving signed-in state while leaving the user's active window and tabs alone.
- [Jarvis gateway memory diagnosis](https://github.com/artemgetmann/openclaw/pull/1429) - traced repeated crashes to default heap limits, added adaptive sizing, and kept source proof separate from live-runtime claims.

## Earlier Work

- 🎙️ [Jarvis Voice AI](https://github.com/artemgetmann/jarvis-voice-ai) - a separate, earlier cloud voice-first AI web platform with streaming responses, automatic text-to-speech, persistent sessions, and multi-model support. This is not the current local-first Jarvis product.
- 🎤 [OneTapTranscribe](https://github.com/artemgetmann/OneTapTranscribe) - one-tap iOS transcription with an instant transcript-to-clipboard flow.

## Background

I spent seven years co-founding and scaling a business before going all-in on AI products. I build tools around problems I encounter directly: agent memory, reliable computer work, voice interfaces, and practical market research.

## Connect

- X: [@artemgetman_](https://x.com/artemgetman_)
