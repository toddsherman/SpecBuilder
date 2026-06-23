# product-spec-interviewer (Claude Code plugin marketplace)

A Claude Code plugin marketplace containing **product-spec-interviewer** — a
manually-invoked slash command that runs a structured product & technology
requirements interview and turns a raw idea into a detailed spec, an executive
summary, and a decision log.

## Install

In an interactive Claude Code session:

```
/plugin marketplace add toddsherman/product-spec-interviewer
/plugin install product-spec-interviewer@spec-tools
```

Then start an interview by typing:

```
/spec-interview
```

(optionally pass your idea inline: `/spec-interview a habit-tracking app for runners`)

## What's in here

- `.claude-plugin/marketplace.json` — the marketplace manifest (marketplace name: `spec-tools`).
- `plugins/product-spec-interviewer/` — the plugin itself (`plugin.json`, `commands/spec-interview.md`, and its own README).
