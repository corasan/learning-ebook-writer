---
name: codebase-explainer
description: Turn an unfamiliar codebase into a full onboarding "book" that covers what it does, how it's organized, how data flows through it, and the concepts behind its design choices, grounded entirely in what's in the repo, never guessed. Use this whenever the user asks to "explain this codebase," "help me understand this repo," "onboard me onto X," "how does this project work," or wants a real architectural map instead of a file-by-file summary. Companion skill to learning-topic, same book format and writing rules, different research method (reading real code instead of external sources).
---

# Codebase Explainer

This skill turns a codebase into and onboarding document. It shares its book format, writing style, and unslop pass with `learn-topic`. What's different is Step 1: no web research and every claim has to be checked against real files.

## Step 0: Scope the exploration

1. **Which codebase, and how much of it.** If the user pointed at a whole large monorepo, ask whether they want the whole thing or a specific subsystem or service. Guessing the scope on a huge codebase wastes the research pass. A single focused repo needs no scoping question.
2. **Why they need this.** Default assumption if unstated: "onboarding a new contributor who's never seen this code." If they mention a specific task ("I need to add a new payment provider"), bias the book toward the parts of the codebase that task touches, without skipping the orientation chapters entirely.
3. **Depth of concept deep-dives.** Same default as learn-topic: explain underlying software-engineering and CS concepts in depth wherever the codebase leans on one, not just enough to name-drop it. This can serve as a helpful reminder in case these are concepts the user hasn't worked in a while.

## Step 1: Investigate the codebase, don't summarize file names

This step replaces learn-topic's web-research step. Do these roughly in order:

1. **Read what the maintainers already wrote.** README, CONTRIBUTING, docs/, architecture decision records, inline comments on non-obvious code. This tells you what they think matters, and often answers "why" questions you'd otherwise have to guess at.
2. **Map the shape before the details.** Walk the directory structure and note the manifest file (package.json, pyproject.toml, Cargo.toml, go.mod) before opening individual source files. You need the shape of the forest before the trees make sense.
3. **Find the real entry points.** main(), an index file, a CLI entry, a server bootstrap, a Lambda handler. Find what actually runs first, not what looks important.
4. **Trace one real flow end to end.** Pick a representative request, command, or job and follow it from entry point to output, file by file. This single traced flow becomes the spine of Part I, and it's how real understanding forms. Reading files in isolation doesn't build it.
5. **Identify the load-bearing abstractions.** Every non-trivial codebase has 3-6 concepts everything else is built on: a core model class, a plugin or middleware system, a state store, a schema layer. Find these deliberately; they become Part II's chapters.
6. **Read the tests.** Tests are often the most honest documentation of intended behavior: what the authors expected to happen, as opposed to what a docstring claims.
7. **Note conventions, and any deliberate departures from them.** A codebase that mostly does X but has one module doing Y differently usually has a real (and often instructive) reason.
8. **Never guess at behavior you haven't read.** A function's name is a hypothesis about what it does, not proof. Open it and check before you describe it in the book. An onboarding book that's confidently wrong about the code is worse than no book at all.

## Step 2: Structure it like an onboarding book, not a wiki

```
Title Page / What This Book Covers (and what codebase and version it maps to)
Table of Contents

PART I: Orientation
  Ch 1: What this does (product-level, plain language, no jargon yet)
  Ch 2: How it's organized (directory tour, tech stack, how to run it locally)
  Ch 3: How a request or job moves through it (the one flow you traced in Step 1, start to finish)

PART II: Architecture deep dive
  One chapter per load-bearing abstraction found in Step 1, each following the
  chapter pattern below, with the "small example" always being a real excerpt
  from the code, cited by file path

PART III: Working in this codebase
  Conventions, testing approach, common pitfalls and footguns, and "if you needed
  to add X, here's where it would go and what it would touch"

Glossary (every jargon term, defined in plain language)
Sources (the real files, docs, and commit and PR history you consulted;
no external links unless the codebase's own docs point to them)
```

Chapter-level pattern (same DNA as learn-topic, adapted):

1. **Motivate before defining.** Open with the real problem this part of the codebase solves, not a dry description of its structure.
2. **Build the mental model first**, then attach the codebase's own vocabulary (class names, module names) to it.
3. **Small real example, then explanation, then a slightly bigger real example.** Every code excerpt is copied verbatim from the repo, with its file path stated. Never fabricate a plausible-looking snippet.
4. **Concept deep-dive box** (Step 3) wherever the codebase leans on a transferable software-engineering idea.
5. **A "where this bites people" callout** with the mistake a new contributor actually makes with this part of the code (a footgun, a non-obvious invariant, a place two things must stay in sync).
6. **Recap** in 3-5 plain sentences.

## Step 3: The concept deep-dive rule

Whenever the codebase leans on a broader, transferable idea (dependency injection, event sourcing, a specific design pattern, a consistency or caching model, a build system's core mechanism, a particular concurrency approach), stop and explain the general concept in depth in its own boxed section, then show precisely how this codebase implements it. This is what turns "here's what the code does" into "you now understand this whole class of system," which is the goal of onboarding someone well.

Rule of thumb: if the concept would help the reader understand a *different* codebase that used the same pattern, it earns a deep-dive. If it's purely this-codebase trivia, a short note is enough.

## Step 4: Writing style rules

Same rules as learn-topic: plain language always, define jargon the moment it's introduced, analogies over abstraction, second person and direct, assume nothing but condescend never, short paragraphs around hard ideas. The one addition specific to this skill: **never invent a plausible-sounding code example.** If you need an example and can't find a clean real one, either simplify by trimming an existing real snippet (clearly marked as trimmed) or describe the behavior in prose instead of faking code.

## Step 5: Verify before you publish

- For every factual claim about behavior: did you open and read the relevant code, or infer it from a name or a comment alone? Names and comments can be stale. Verify against the code that actually runs.
- For every code excerpt: does it match the repo verbatim, and is the cited file path correct?
- For every "why was this built this way" claim: is it backed by real evidence (a comment, a doc, a commit message, an ADR), or is it your own inference? If it's inference, label it as such ("likely reason, based on X") rather than stating it as settled fact.
- Does Part II cover the abstractions a new contributor would hit first, or did easier-to-explain but less important pieces crowd them out?

## Step 5.5: Run an unslop pass

Same as learn-topic: before final assembly, run every chapter through the `unslop` skill if it's available in your environment (it ships alongside this one at `skills/unslop/SKILL.md` in this repo, or install standalone via `npx skills add https://github.com/cursor/plugins --skill unslop`). If it isn't available, reread each chapter for AI writing tells (significance inflation, stock AI vocabulary, em dashes, chatbot filler, hedge-on-hedge phrasing) and fix them by hand.

## Step 6: Assemble and deliver

Same default as learn-topic: **a single self-contained HTML file, styled and structured like mdBook**. That means a fixed sidebar table of contents (Parts, Chapters, Glossary, Sources), one chapter shown at a time, prev/next links at the bottom of each chapter, clean typography, a distinct visual treatment for the concept deep-dive and "where this bites people" boxes, and all CSS and JS inline so it works offline with no external dependencies.

One addition specific to this skill: every code excerpt block should visibly show its source file path (e.g. as a small caption above or below the block) so the reader can find it in their own editor.

**Fallback.** If the tool you're running in truly cannot output an HTML file, fall back to a single flowing Markdown document with the same structure.
