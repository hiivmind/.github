# hiivmind

**Open-source plugins and Python libraries for coding agents and agent automation.**

[![Harnesses](https://img.shields.io/badge/Harnesses-Claude_Code_%C2%B7_Codex_%C2%B7_Cursor_%C2%B7_Gemini_CLI_%C2%B7_more-555555?style=flat-square)](#projects)
[![Corpora](https://img.shields.io/badge/Corpora-18_public-2E7D32?style=flat-square)](#published-corpora)
[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?style=flat-square&logo=python&logoColor=white)](#status)
[![Status](https://img.shields.io/badge/Status-experimental-orange?style=flat-square)](#status)

> **Experimental.** hiivmind-corpus and Swingle are released. The corpus agent, hiivmind-corpus-lib and hiivmind-agent-core are newer, and their formats and interfaces may still change.

---

## What this is

The projects here fall into three groups.

**Documentation corpora.** [Context7](https://context7.com) and [Ref](https://ref.tools) give coding agents up-to-date documentation for public libraries, indexed and served from their own platforms. Material outside that set is harder to reach. Context7 takes private sources only on its paid plans, and Ref's private index takes GitHub repositories and uploaded PDF or Markdown files.

hiivmind-corpus indexes documentation from any source you can point it at: git repositories, web pages such as blog posts, articles and wiki pages, PDFs, Obsidian vaults, `llms.txt` files, generated API references and local documents. One corpus can mix several of them, so a library's official docs can sit next to the papers, posts and internal notes that explain how it is used.

A corpus is a git repository. Each entry in its index points to a document or section and has a title, summary, keywords and concepts. Embeddings of the entries can be committed alongside the index, so retrieval runs locally: vector search over the entries, boosted by the concept graph and reranked. The agent then reads only the documents it needs, the ["just in time" context approach](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) described by Anthropic. Because the index is plain files in git, nothing runs on a hosted service, and anyone can publish a corpus or register someone else's. The plugin works inside Claude Code, Codex, Cursor, Gemini CLI and Antigravity, and the corpus agent keeps published corpora up to date with pull requests.

**agent-core.** A Python harness for agentic automation jobs. A job is a set of steps, each written as Markdown instructions, arranged into sequences in YAML. agent-core runs them against a model, journals each run so a crashed run can resume, and records what happened. It isn't specific to corpora; the corpus agent is one job built on it.

**Swingle.** A skills plugin that lets the coding agent you're working in hand one job to another CLI installed on your machine, such as Codex, Claude Code, opencode or Pi. Each delegation has a written brief, a return contract and a ledger entry.

---

## Projects

### Documentation corpora

| Project | What it does | Status |
|---|---|---|
| [hiivmind-corpus](https://github.com/hiivmind/hiivmind-corpus) | Plugin for building, registering, searching and refreshing corpora. Installs in Claude Code, Codex, Cursor, Gemini CLI and Antigravity. Sources can be git repos, local files, web pages, PDFs, Obsidian vaults and `llms.txt`. Search combines embeddings with the concept graph, and bridges link concepts across corpora. | Released |
| [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent) | An agent-core job that maintains corpora. Runs `refresh`, `enrich`, `migrate`, `status` and `graph-validate` without a person present, commits to a new branch, opens a pull request, and keeps a record of every run. | In development |
| [hiivmind-corpus-lib](https://github.com/hiivmind/hiivmind-corpus-lib) | Python library that reads and writes a corpus directory: config, index, concept graph, rendered indexes, embeddings and search. Files are written in a fixed format, so a refresh diff contains only the entries that changed. | In development |

### Agent automation

| Project | What it does | Status |
|---|---|---|
| [hiivmind-agent-core](https://github.com/hiivmind/hiivmind-agent-core) | Python harness for model-driven automation jobs. A job declares its steps as Markdown instruction files, its sequences in YAML, and a policy the model must follow. The harness runs them through a pluggable backend (LangGraph today, with Anthropic or OpenAI models), journals runs with DBOS so a crashed run can resume, and can run unattended or ask a person at the terminal. | In development |

### Delegation

| Project | What it does | Status |
|---|---|---|
| [swingle](https://github.com/hiivmind/swingle) | Skills plugin that lets the driving coding agent delegate a job to another provider CLI already installed and signed in on the machine: `codex`, `claude`, `opencode`, `grok`, `pi`, `agy`, `omp`, `cursor-agent`, `devin` or `copilot`. The model writes the brief, picks the CLI, runs it and checks the result; each run is recorded in `.swingle/delegate/`. Installs in Claude Code, Codex, Pi, Antigravity and Oh My Pi. | Released |

### Published corpora

Entry counts are from each corpus's `index.yaml`.

| Corpus | Covers | Entries |
|---|---|---|
| **Data engineering** ([hiivmind-corpus-data](https://github.com/hiivmind/hiivmind-corpus-data)) | | |
| [polars](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-polars) | Polars DataFrames in Python and Rust | 112 |
| [ibis](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-ibis) | Portable dataframe expressions across 20+ SQL backends | 95 |
| [narwhals](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-narwhals) | Dataframe-agnostic code for pandas, Polars and PyArrow | 67 |
| [substrait](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-substrait) | Cross-language query plan specification | 62 |
| [datafusion](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-datafusion) | Apache DataFusion and its Python bindings | 116 |
| [dlt](https://github.com/hiivmind/hiivmind-corpus-data/tree/main/hiivmind-corpus-dlt) | dlt data load tool | 219 |
| [frictionless](https://github.com/hiivmind/hiivmind-corpus-frictionless) | Frictionless Framework and the Data Package standard | 293 |
| [lancedb](https://github.com/hiivmind/hiivmind-corpus-lancedb) | LanceDB vector database | 193 |
| **Agents and AI** | | |
| [agno](https://github.com/hiivmind/hiivmind-corpus-agno) | Agno agent framework and AgentOS | 3,801 |
| [claude-agent-sdk](https://github.com/hiivmind/hiivmind-corpus-claude/tree/main/hiivmind-corpus-claude-agent-sdk) | Claude Agent SDK for Python and TypeScript | v1 |
| [claudecodebook](https://github.com/hiivmind/hiivmind-corpus-claudecodebook) | *Claude Code from Source*, an 18-chapter architecture analysis | 18 |
| [midjourney](https://github.com/hiivmind/hiivmind-corpus-midjourney) | Midjourney prompting, parameters and features | 68 |
| **Platforms and tools** | | |
| [github](https://github.com/hiivmind/hiivmind-corpus-github) | GitHub Docs, the GraphQL schema and the `gh` manual | v1 |
| [flyio](https://github.com/hiivmind/hiivmind-corpus-flyio) | Fly.io apps, Machines, networking and the `flyctl` CLI | 180 |
| [dbos](https://github.com/hiivmind/hiivmind-corpus-dbos) | DBOS durable workflows | 155 |
| [obsidian](https://github.com/hiivmind/hiivmind-corpus-obsidian) | Obsidian help documentation | 171 |
| [fastmail](https://github.com/hiivmind/hiivmind-corpus-fastmail) | Fastmail API, JMAP specifications and samples | v1 |
| [stakpak](https://github.com/hiivmind/hiivmind-corpus-stakpak) | Stakpak infrastructure-as-code platform and REST API | v1 |

*v1*: an older index format (`index.md` only). The corpus agent's `migrate` job converts these to the current format.

---

## How the corpus projects fit together

```
  upstream docs                                 coding agent
  (git repos, sites, PDFs)                (Claude Code, Codex, ...)
         |                                          |
         |                                    hiivmind-corpus
         |                               (register, search, build)
         v                                          v
  hiivmind-corpus-agent  -- pull request -->      corpus
  (refresh, enrich, migrate)               (git repo: index, graph,
         |                                       embeddings)
    +----+-----------------+
    |                      |
  hiivmind-agent-core    hiivmind-corpus-lib
  (runs the job)         (reads and writes the corpus)
```

A corpus is only files: YAML, Markdown and an embeddings table, with no server or database. It can be forked, published and reviewed like any other repository. The plugin reads corpora, the corpus agent updates them, and its changes arrive as pull requests. agent-core sits underneath the corpus agent but can run any other job.

---

## Where to start

| If you want to… | Start with | Then |
|---|---|---|
| Ask questions of a library's docs | Install hiivmind-corpus in your coding agent and register a published corpus | Register more; `/hiivmind-corpus bridge` links concepts across them |
| Index your own project, or a library not listed | `/hiivmind-corpus init`, `add-source`, `build` | Publish the repository so others can register it |
| Keep a corpus up to date | `/hiivmind-corpus refresh` in a session | [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent) to run refreshes unattended and open pull requests |
| Automate a multi-step job with a model | [hiivmind-agent-core](https://github.com/hiivmind/hiivmind-agent-core): write the steps, sequences and policy for your job | Read [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent) as a complete example |
| Hand a job to another CLI without leaving your session | Install [Swingle](https://github.com/hiivmind/swingle) | `swingle-delegate` for one job, `swingle-sdd` to run a written plan |

In Claude Code, for example:

```bash
/plugin marketplace add hiivmind/hiivmind-corpus
/plugin install hiivmind-corpus@hiivmind-corpus

/hiivmind-corpus register github:hiivmind/hiivmind-corpus-data/hiivmind-corpus-polars
```

Then ask a question, for example *"How do lazy frames work in Polars?"* [INSTALL.md](https://github.com/hiivmind/hiivmind-corpus/blob/main/INSTALL.md) has the steps for Codex, Cursor, Gemini CLI and Antigravity.

---

## Corpus design notes

1. Entries are curated. Each has a summary, keywords and concepts, so an agent can choose documents before reading them.
2. Corpora are plain YAML and Markdown in git, so they can be read, diffed and edited by hand.
3. Each source records the upstream commit it was indexed at, and each entry records its source and path. A refresh rescans only the files that changed upstream.
4. The corpus agent commits to a branch and opens a pull request. It does not force-push or rewrite history.
5. Embeddings are committed next to the index and searched locally. A refresh does not download an embedding model.

---

## Built on

[LangGraph](https://www.langchain.com/langgraph) · [DBOS](https://www.dbos.dev) · [LanceDB](https://lancedb.com) · [FastEmbed](https://github.com/qdrant/fastembed) · [GitHub CLI](https://cli.github.com)

---

## Status

hiivmind-corpus, Swingle, hiivmind-agent-core and hiivmind-corpus-agent are MIT licensed; hiivmind-corpus-lib is AGPL-3.0-or-later. The published corpora are public. The Python projects need Python 3.12 or later and are not on PyPI yet; the corpus agent expects agent-core and hiivmind-corpus-lib checked out beside it. The corpus agent has opened its first refresh pull requests on live corpora, for example [hiivmind-corpus-data#17](https://github.com/hiivmind/hiivmind-corpus-data/pull/17).

---

Maintained by [Nathaniel Ramm](https://github.com/discreteds) in Melbourne. Bug reports, corpus requests and contributions are welcome as issues on the relevant repository, or get in touch on [LinkedIn](https://linkedin.com/in/nathaniel-ramm).
