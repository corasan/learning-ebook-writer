# learning-ebook-writer

An [Agent Skill](https://agentskills.io) that turns any topic into a full, researched ebook that teaches you from zero, in the style of [mdBook](https://github.com/rust-lang/mdbook). By default it produces one self-contained HTML file styled like mdBook, with sidebar navigation, one chapter per page, and prev/next links.

Works with Claude Code, Codex, Cursor, and 70+ other agents via [`skills`](https://skills.sh).

## What it does

- Splits a topic into a broad foundation plus an optional deep-dive
- Researches primary and trusted sources before it writes a word, and fact-checks before it publishes
- Gives every chapter the same shape: motivation, mental model, worked example, concept deep-dive, recap
- Goes in depth on any underlying CS, ML, or systems concept the topic touches, not just the tool's syntax
- Writes in plain language, defines every jargon term, and never talks down to the reader
- Outputs a single self-contained HTML file, with a Markdown fallback for text-only tools

## Install

```bash
npx skills add corasan/learning-ebook-writer
```

## License

MIT. See [LICENSE](./LICENSE).
