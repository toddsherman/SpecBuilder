# SpecBuilder (Claude Code plugin marketplace)

A Claude Code plugin marketplace containing **product-spec-interviewer** — a
manually-invoked slash command that runs a structured product & technology
requirements interview and turns a raw idea into a detailed spec, an executive
summary, and a decision log.

A readable, copy-pasteable version of the prompt is published at
[todd.sh/specBuilderPrompt](https://www.todd.sh/specBuilderPrompt).

## Install

In an interactive Claude Code session:

```
/plugin marketplace add toddsherman/SpecBuilder
/plugin install product-spec-interviewer@spec-tools
```

Then start an interview by typing:

```
/product-spec-interviewer:spec-interview
```

(optionally pass your idea inline: `/product-spec-interviewer:spec-interview a habit-tracking app for runners`)

### Prefer the shorter `/spec-interview` command?

Copy the single command file into your personal commands directory:

```bash
cp plugins/product-spec-interviewer/commands/spec-interview.md ~/.claude/commands/spec-interview.md
```

Loose commands in `~/.claude/commands/` are not namespaced, so you can invoke it
directly as `/spec-interview`.

## What's in here

- `.claude-plugin/marketplace.json` — the marketplace manifest (marketplace name: `spec-tools`).
- `plugins/product-spec-interviewer/` — the plugin itself (`plugin.json`, `commands/spec-interview.md`, and its own README).
