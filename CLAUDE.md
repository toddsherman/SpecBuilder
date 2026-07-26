# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Claude Code **plugin marketplace** named `spec-tools` containing a single plugin,
**product-spec-interviewer**. There is no application code, build step, test suite, or
lint config — the repo is entirely markdown and JSON that Claude Code loads at runtime.
"Changing the product" means editing a prompt/manifest, not writing executable code.

## Structure & the two manifest layers

The repo has two stacked `.claude-plugin` layers that must agree with each other:

- `/.claude-plugin/marketplace.json` — the **marketplace** manifest (name: `spec-tools`).
  Lists the plugin and points at it via `source: "./plugins/product-spec-interviewer"`,
  and carries a `version` for that entry.
- `/plugins/product-spec-interviewer/.claude-plugin/plugin.json` — the **plugin** manifest
  (metadata only: name, description, version, author, keywords).
- `/plugins/product-spec-interviewer/commands/spec-interview.md` — **the entire product.**
  The command's YAML frontmatter plus the prompt body below it is what actually runs. All
  interview behavior and the three output templates live here.

When bumping the version, update it in **both** `plugin.json` and `marketplace.json` — they
are independent fields and will silently drift apart otherwise. Likewise keep the `name` and
`description` consistent across both manifests and the two READMEs.

## The command contract (spec-interview.md)

This is the file you'll almost always be editing. A few invariants are load-bearing and
easy to break by accident:

- Frontmatter sets `disable-model-invocation: true` — the command is **manual only** and
  must never auto-fire. Don't remove this. The READMEs promise this behavior to users.
- It is invoked as `/product-spec-interviewer:spec-interview` when loaded as a plugin
  (plugin commands are namespaced), or as `/spec-interview` when the bare command file is
  copied into `~/.claude/commands/`. Same file, different invocation prefix.
- The interview produces **three separate output files** — `spec.md`, `summary.md`,
  `decisions.md` — using the exact templates embedded at the bottom of the command. They
  are deliberately separate so each can be edited independently; keep them that way.
- Core behavioral rules the prompt encodes (preserve their intent when editing): explain
  every technology in plain language before asking the user to choose; establish build
  stage (prototype / MVP / production-at-scale) first and let it drive all recommendations;
  bias toward speed-to-validation while flagging expensive-to-reverse decisions; ask in
  batches of 3–5 continuously-numbered questions; web-check concrete tool/version picks for
  currency before recommending them.

## Testing a change

There is nothing to compile or run. To exercise a change, load the plugin into an
interactive Claude Code session and invoke the command:

```bash
claude --plugin-dir /path/to/product-spec-interviewer
# then in the session:
/product-spec-interviewer:spec-interview a couch-to-5k app for nervous beginners
```

Or install through the marketplace flow:

```
/plugin marketplace add toddsherman/product-spec-interviewer
/plugin install product-spec-interviewer@spec-tools
```
