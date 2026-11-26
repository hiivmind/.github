# hiivmind

**Documentation corpora for coding agents, kept current by an agent of their own.**

[![Claude Code plugin](https://img.shields.io/badge/Claude_Code-plugin-D97757?style=flat-square&logo=claude&logoColor=white)](https://github.com/hiivmind/hiivmind-corpus)
[![Corpora](https://img.shields.io/badge/Corpora-18_public-2E7D32?style=flat-square)](#published-corpora)
[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?style=flat-square&logo=python&logoColor=white)](#status)
[![Status](https://img.shields.io/badge/Status-experimental-orange?style=flat-square)](#status)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](https://github.com/hiivmind/hiivmind-corpus/blob/main/LICENSE)

> **Experimental.** Everything here is public and in development. The corpus agent and the libraries under it are newest: their formats and interfaces can still change between commits.

---

## Why hiivmind

A coding agent that meets a library it does not know has three bad options: trust training data that is out of date, search the web and hope, or fetch pages one at a time with no map of what exists. Every session rediscovers the same things, and each rediscovery fills the context window.

A **corpus** is the map. It is a plain git repository holding a curated index of a project's documentation: one entry per document or section, each with a title, summary, keywords and concepts, plus a concept graph and embeddings for semantic search. The agent searches the index and fetches only the documents it needs, the ["just in time" context pattern](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) Anthropic recommends. Each source records the upstream commit it was indexed at, so the corpus knows when it is stale.

An index is only useful while it is current, and upstream documentation moves every week. The **corpus agent** does that upkeep without a person at the terminal: it checks each corpus against its upstream sources, rescans and re-summarises what changed, removes entries whose files are gone, verifies a sample, and opens a pull request with the result. A person reviews a diff instead of rebuilding an index.

---

## Projects

### Corpus tooling

| Project | What it does | Status |
|---|---|---|
| [hiivmind-corpus](https://github.com/hiivmind/hiivmind-corpus) | Claude Code plugin to build, register, search and refresh corpora in plain language. Sources can be git repos, local files, web pages, PDFs, Obsidian vaults and `llms.txt`. Includes semantic search with concept-graph boosting and bridges between corpora. | Released |
| [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent) | The unattended maintainer. Runs `refresh`, `enrich`, `migrate`, `status` and `graph-validate` jobs over a corpus as sequences of model-driven nodes. Commits to a new branch and opens a pull request, never force-pushes, and records every run. | In development |
| [hiivmind-corpus-lib](https://github.com/hiivmind/hiivmind-corpus-lib) | Python library that reads and writes a corpus directory: config, index, concept graph, rendered indexes, embeddings and search. Canonical formats, so a refresh diff shows only the entries that changed. | In development |
| [hiivmind-agent-core](https://github.com/hiivmind/hiivmind-agent-core) | Small harness the corpus agent runs on. Executes nodes and sequences behind a pluggable model backend, with a journal so a crashed run can resume. | In development |

### Published corpora

Open corpora, ready to register. Entry counts come from each corpus's `index.yaml`.

| Corpus | Covers | Entries |
|---|---|---|
| **Data engineering** — [hiivmind-corpus-data](https://github.com/hiivmind/hiivmind-corpus-data) | | |
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

*v1*: an earlier index format (`index.md` only). The agent's `migrate` job converts these to the current format.

---

## How they fit together

```
  upstream docs                                Claude Code
  (git repos, sites, PDFs)                          |
         |                                    hiivmind-corpus
         |                               (register, search, build)
         v                                          v
  hiivmind-corpus-agent  -- pull request -->      corpus
  (refresh, enrich, migrate)               (git repo: index, graph,
         |                                       embeddings)
    +----+-----------------+
    |                      |
  hiivmind-agent-core    hiivmind-corpus-lib
  (runs the nodes)       (reads and writes the corpus)
```

A corpus is data only: no server and no database, so anyone can fork, publish or review one like any other repository. The plugin reads it; the agent maintains it; people review the pull requests.

---

## Where to start

| If you want to… | Start with | Then |
|---|---|---|
| **Ask questions of a library's docs** | Install hiivmind-corpus and register a published corpus | Register more; `/hiivmind-corpus bridge` links concepts across them |
| **Index your own project or a library not listed** | `/hiivmind-corpus init`, `add-source`, `build` | Publish the repository so others can register it |
| **Keep a corpus current** | `/hiivmind-corpus refresh` in a session | [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent) for unattended refreshes that arrive as pull requests |

```bash
/plugin marketplace add hiivmind/hiivmind-corpus
/plugin install hiivmind-corpus@hiivmind-corpus

/hiivmind-corpus register github:hiivmind/hiivmind-corpus-data/hiivmind-corpus-polars
```

Then ask: *"How do lazy frames work in Polars?"*

---

## Design principles

1. **The index is the product.** Curated entries with summaries and concepts, not a dump of pages. The agent loads what it needs and nothing else.
2. **A corpus is a git repository.** Plain YAML and Markdown that a person can read, diff, review and fix. If a person can't read it, a person can't fix it.
3. **Freshness is a fact, not a guess.** Each source records the commit it was indexed at, and each entry its source and path, so a refresh rescans exactly what changed upstream.
4. **Maintenance proposes; people decide.** The agent works on a branch and opens a pull request. It never force-pushes or rewrites history.
5. **Search without a service.** Embeddings are committed next to the index and searched locally. A refresh never downloads a model.

---

## Built on

[Claude Code](https://docs.claude.com/en/docs/claude-code/overview) · [LangGraph](https://www.langchain.com/langgraph) · [DBOS](https://www.dbos.dev) · [LanceDB](https://lancedb.com) · [FastEmbed](https://github.com/qdrant/fastembed) · [GitHub CLI](https://cli.github.com)

---

## Status

hiivmind-corpus is open source under the MIT License, and the published corpora are public. [hiivmind-corpus-agent](https://github.com/hiivmind/hiivmind-corpus-agent), [hiivmind-corpus-lib](https://github.com/hiivmind/hiivmind-corpus-lib) and [hiivmind-agent-core](https://github.com/hiivmind/hiivmind-agent-core) are public and in development, require Python 3.12 or later, and are not yet on PyPI; the agent takes the other two as checkouts beside it. The agent has opened its first refresh pull requests against live corpora, such as [hiivmind-corpus-data#17](https://github.com/hiivmind/hiivmind-corpus-data/pull/17). Repositories still in an earlier format are listed as *v1* above.

---

Maintained by [Nathaniel Ramm](https://github.com/discreteds) in Melbourne. Bug reports, corpus requests and contributions are welcome as issues on the relevant repository, or get in touch on [LinkedIn](https://linkedin.com/in/nathaniel-ramm).
