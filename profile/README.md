# hiivmind

**Meta-skills for Claude Code.** We build orchestration layers that turn complex toolchains into composable, cacheable workflows.

---

## What We Build

Claude Code skills that solve for persistence of knowledge in Claude Code — establishing and maintaining your long-term context without filling your short-term context window!

### [hiivmind-pulse-gh](https://github.com/hiivmind/hiivmind-pulse-gh)

GitHub automation that actually understands your org.

Projects v2, milestones, branch protection — all require hunting for opaque GraphQL node IDs. `pulse-gh` discovers your org structure once, caches it, and lets you work in plain English from then on.

```
"Show me in-progress items assigned to @alice"
"Create a v2.0 milestone for the api repo"
"Protect main with required reviews"
```

No more `PVT_kwDOBx...` or `PVTSSF_...` hunting.

Claude TODO lists can be reliably persisted as github issues and projects. 

Multiple agents can work from the same source of truth, and communicate with each other via comments on issues and PRs. 
Agents can implicitly adopt a role or persona without complex agent orchestration. Just run several open sessions and they can share state via github.


### [hiivmind-corpus](https://github.com/hiivmind/hiivmind-corpus)

Persistent documentation indexes for any open-source project.

Instead of web search or stale training data, `corpus` creates human-curated markdown indexes that track upstream changes. Point it at a repo, build the index collaboratively, refresh when things change.

```
hiivmind-corpus-init → hiivmind-corpus-build → hiivmind-corpus-refresh
       (once)                (once)                  (periodic)
```

Utilises local cache for fast searching. Tracks commit SHAs. Falls back to raw GitHub URLs when needed.

---

## Philosophy

**Discover once, use forever.** Structure is stable; data changes constantly. Cache the IDs, fields, and mappings — not the content.

**Skills over MCP.** Load on-demand, not all upfront. Better context efficiency for complex workflows.

**Human-readable everything.** YAML configs, markdown indexes. If a human can't read it, a human can't fix it.

---

## Getting Started

Both projects are Claude Code plugins. Install via the marketplace:

```
/plugin marketplace add hiivmind/hiivmind-pulse-gh
/plugin install hiivmind-pulse-gh@hiivmind-pulse-gh
```

```
/plugin marketplace add hiivmind/hiivmind-corpus
/plugin install hiivmind-corpus@hiivmind-corpus
```

---

<sub>Built by developers who got tired of the same boilerplate. Melbourne, AU.</sub>
