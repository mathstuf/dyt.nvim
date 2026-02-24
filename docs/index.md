# Documentation Index

dyt.nvim — Neovim plugin for zero-latency voice dictation via DictateYourTerms.

## Documents

| Document | Purpose | Read When |
|----------|---------|-----------|
| [architecture.md](./architecture.md) | Plugin internals, lifecycle, state machine, error invariants | Modifying core behaviour, debugging, adding features |
| [getting-started.md](./getting-started.md) | Prerequisites, local dev setup, manual testing, release flow | First-time setup, contributing |

## Quick Navigation

**"How does the dictation lifecycle work?"** → [architecture.md § Lifecycle](./architecture.md#lifecycle)

**"How do I add a new config option?"** → [architecture.md § Extending the Plugin](./architecture.md#extending-the-plugin)

**"How do I test my changes?"** → [getting-started.md § Manual Testing](./getting-started.md#manual-testing)

**"What Neovim version is required?"** → [getting-started.md § Prerequisites](./getting-started.md#prerequisites)

## Project Files

```
lua/dyt/init.lua    ← all plugin logic
plugin/dyt.lua      ← auto-init shim
doc/dyt.txt         ← vimdoc help (:h dyt)
README.md           ← user-facing installation and configuration
CLAUDE.md           ← project conventions for AI-assisted development
```
