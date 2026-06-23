# product-spec-interviewer

A Claude Code plugin with one manually-invoked slash command, `spec-interview`.
It runs a structured product & technology requirements interview: you bring a raw
idea, it interviews you in small batches of options-with-recommendations, and it
writes the result to three editable files — `spec.md`, `summary.md`, and
`decisions.md`.

It is **manual only**. It will never fire on its own; you start it by typing the
command.

## What it does

- Opens by asking about your idea (or takes the idea inline as an argument).
- Talks to you as a capable product thinker who isn't a deep engineer — it
  explains every technology option in plain language before asking you to choose.
- Establishes up front whether you're building a throwaway prototype, a validated
  MVP, or a production-at-scale system, and lets that drive every tech
  recommendation (biased toward speed-to-validation, with expensive-to-reverse
  decisions flagged).
- Asks 3–5 questions per batch, numbered continuously, with options and a clear
  recommendation where real alternatives exist.
- Checkpoints every few batches (what's locked / confidence / what's open) and
  honors "write it now" and "you choose" at any time.
- Web-checks the actual tool/version picks for currency before recommending them.
- Builds the spec as a living document so you can correct it mid-stream, and
  supports resuming a session by pasting the in-progress files back in.

## Install & use (plugin)

The simplest local route — point Claude Code at the plugin directory when you
launch it:

```bash
claude --plugin-dir /path/to/product-spec-interviewer
```

Then, inside the session:

```
/product-spec-interviewer:spec-interview
```

(Plugin commands are namespaced with the plugin name, so the full invocation is
`/product-spec-interviewer:spec-interview`. You can also pass your idea inline:
`/product-spec-interviewer:spec-interview a couch-to-5k app for nervous beginners`.)

To distribute it to others or load it without the `--plugin-dir` flag every time,
add a marketplace manifest and install through `/plugin` — see the Claude Code
plugins documentation for the marketplace flow.

## Prefer to just type `/spec-interview`?

If you don't need the plugin packaging and want the bare command name, copy the
single command file to your personal commands directory:

```bash
cp commands/spec-interview.md ~/.claude/commands/spec-interview.md
```

Loose command files in `~/.claude/commands/` are **not** namespaced, so you'd
invoke it as exactly:

```
/spec-interview
```

Same file, same behavior — only the location and the invocation prefix differ.

## Editing it

Everything that powers the command — the full interview logic and the three
output templates — lives in one human-readable file: `commands/spec-interview.md`.
Edit it directly to change how the interview behaves or what the output files look
like. `plugin.json` only holds metadata (name, version, author); change the
`author` field to whatever you like.
