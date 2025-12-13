# hiivmind

**Persistent context for Claude Code.**

Skills that establish and maintain long-term knowldege without filling your context window.

---

## Core Plugins

### [hiivmind-corpus](https://github.com/hiivmind/hiivmind-corpus)

**Persistent documentation indexes for any project.**

Think of it like Claude Projects for Claude Code, but better. With Projects, you dump docs, code, and PDFs into a collection that persists across chats. But everything consumes context, there's no way to prioritize what matters, no freshness tracking, no namespacing, no search.

A corpus solves all of this. You build a curated index once, Claude searches it directly without filling your context window, and the index tracks exactly where everything came from and how fresh it is. Install as many as you need. They're lightweight and independent.

This implements the ["just in time" context pattern](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) recommended by Anthropic: lightweight identifiers that load content on demand, like how humans use indexes rather than memorizing corpuses.

```
/hiivmind-corpus
```

One command, natural language:

```
"Create a corpus for Polars"
"How do lazy frames work?"
"Add the TanStack Query docs to my fullstack corpus"
"Is my React corpus up to date?"
```

Combine git repos, local documents, and web articles into unified corpora. Eight skills handle the full lifecycle—discover, navigate, init, add-source, build, enhance, refresh, upgrade.

---

## Corpus Marketplaces

Pre-built documentation indexes, ready to install.

### [hiivmind-corpus-data](https://github.com/hiivmind/hiivmind-corpus-data)

**Data engineering libraries:**

| Corpus | Library |
|--------|---------|
| `hiivmind-corpus-polars` | Fast DataFrames in Python and Rust |
| `hiivmind-corpus-ibis` | Portable expressions across 20+ SQL backends |
| `hiivmind-corpus-narwhals` | DataFrame-agnostic code for pandas, Polars, PyArrow |
| `hiivmind-corpus-substrait` | Cross-language query plans and compute interop |

### [hiivmind-corpus-claude](https://github.com/hiivmind/hiivmind-corpus-claude)

**Claude ecosystem:**

| Corpus | Library |
|--------|---------|
| `hiivmind-corpus-claude-agent-sdk` | Claude Agent SDK documentation |

---

## Philosophy

**Discover once, use forever.** Structure is stable; data changes constantly. Cache the IDs, fields, and mappings — not the content.

**Skills over MCP.** Load on-demand, not all upfront. Better context efficiency for complex workflows.

**Human-readable everything.** YAML configs, markdown indexes. If a human can't read it, a human can't fix it.

---

## Getting Started

Install via the Claude Code marketplace:

```bash
# GitHub automation
/plugin marketplace add hiivmind/hiivmind-pulse-gh
/plugin install hiivmind-pulse-gh@hiivmind-pulse-gh

# Documentation corpus tooling
/plugin marketplace add hiivmind/hiivmind-corpus
/plugin install hiivmind-corpus@hiivmind-corpus

# Pre-built corpora (install what you need)
/plugin marketplace add hiivmind/hiivmind-corpus-data
/plugin install hiivmind-corpus-polars

/plugin marketplace add hiivmind/hiivmind-corpus-claude
/plugin install hiivmind-corpus-claude-agent-sdk
```

---

<sub>Melbourne, AU</sub>
