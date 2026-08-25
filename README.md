# learning-ebook-writer

A skill that turns any topic into a full, researched ebook that teaches you from zero, in the style of [mdBook](https://github.com/rust-lang/mdbook). By default it produces one self-contained HTML file styled like mdBook, with sidebar navigation, one chapter per page, and prev/next links.

Works with Claude Code, Codex, Cursor, and 70+ other agents via [`skills`](https://skills.sh).

## Skills

- [`learn-topic`](./skills/learn-topic/SKILL.md): writes a complete, researched "teach me from zero" ebook on any topic, from external primary sources.
- [`learn-codebase`](./skills/learn-codebase/SKILL.md): turns an unfamiliar codebase into an onboarding book, grounded in the repo's real files instead of external sources.

Both skills run every chapter through [`unslop`](./skills/unslop/SKILL.md) before delivery, a skill that cuts AI writing tells from prose. It comes from Lauren Tan's `pstack` plugin in [`cursor/plugins`](https://github.com/cursor/plugins) and is vendored here unmodified under MIT.

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
