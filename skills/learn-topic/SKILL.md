---
name: learn-topic
description: Write a complete, researched "teach me from zero" ebook on any topic, in the style of technical books like *The Rust Programming Language*. Friendly, progressive, concept-first, and never condescending. Use this whenever the user asks to "make an ebook to learn X," "write a book that teaches me X from scratch," "explain X like the official docs don't," or wants a long-form, structured, plain-language learning resource instead of a quick chat answer. Especially valuable for topics with bad or scattered official documentation, or topics that mix a specific tool with deeper underlying concepts (a framework built on a language, a library built on math or CS or ML ideas, and so on). Trigger even if the user just says "help me really learn X" or "I want a guide, not a cheat sheet."
---

# Learn Topic

This skill turns a topic into a full ebook that takes a reader from "knows nothing about this" to "genuinely understands it," the way a well-written technical book does and the way official docs and blog posts don't. Subject agnostic.

The core promise: **clear language over impressive language, correctness over confidence, and concepts before syntax.**

## Step 0: Scope the book

Before writing anything you need to do these four things:

1. **The topic and the split.** A topic could have two layers, a broad foundation and the specific deep-dive. If the user gave you just a flat topic without an obvious split, that's ok. Build a progressive arc instead of forcing a foundation and the deep-dive.
2. **Reader's starting knowledge.** What can you assume they already know? Default if unstated: "knows general concepts adjacent to the field but nothing about this specific topic." State this assumption explicitly at the start of the book itself, so the reader knows where the floor is.
3. **Depth of theory tangents.** Some topics are "just" a tool; others are a thin wrapper over deep ideas (ML, systems, compilers, cryptography). Ask or infer whether the reader wants the underlying theory explained in depth or just enough to use the tool. When unsure, default to depth. That is what separates this from documentation.
4. **Length and format.** Default to a full ebook-length document (many chapters, thousands of words) delivered as one well-structured file, unless the user asks for something shorter. As long as it makes sense.

## Step 1: Research like a fact-checker, not a summarizer

This is the step to focus on the most as we don't want lazy AI hallucinated information on the book.

- Prefer **primary sources**: official documentation, source code and API references, academic papers, standards docs, maintainer talks and blog posts.
- Use **reputable secondary sources** (well-known textbooks, established tutorials, conference talks) to fill gaps or explain concepts more clearly than the primary source does. Official docs can sometimes be confusing or hard to navigate or simply lack information an context.
- For anything version-specific, fast-moving, or uncertain (API names, function signatures, current best practices, recent library changes), verify against current sources rather than memory. Don't guess API names or signatures. A wrong code example is worse than no code example.
- Cross-check non-trivial factual claims across at least two sources when possible. If sources disagree, or you're not confident, say so plainly in the text rather than presenting a guess as settled fact. Make note of this and link these sources so users can read and decide before they move on.
- Keep a running list of sources as you go. You'll need it for the "Further Reading" section.

## Step 2: Structure it like a real book, not a wiki

Use this shape (adapt part and chapter counts to the topic):

```
Title Page / What This Book Covers (and who it's for)
Table of Contents

PART I: Foundations
  Ch 1: Why does this exist? What problem does it solve?
  Ch 2: Core mental model (the one idea everything else builds on)
  Ch 3-N: Building blocks, one at a time, each with small worked examples

PART II: [The specific deep-dive angle, if there is one]
  Continues from Part I's foundation into the specialized territory
  the reader asked about

Glossary (every jargon or confusing term, defined in plain language)
Further Reading & Sources
```

Chapter-level pattern (this is the "Rust book" DNA; reuse it every chapter):

1. **Motivate before defining.** Open with why this concept exists and what breaks without it. Never start a chapter with a bare definition.
2. **Build the mental model first**, then attach vocabulary to it. Introduce a term only after the reader already understands the thing it names.
3. **Small example, then explanation, then a slightly bigger example.** Never dump a large example before the reader has the pieces to read it.
4. **Concept deep-dive box** (see Step 3) wherever a term is doing more work than it looks like.
5. **A "what could go wrong" or "common confusion" callout** with the mistakes a beginner actually makes with this concept.
6. **Recap** in 3-5 plain sentences at the end of the chapter.

## Step 3: The concept deep-dive rule

Whenever the topic touches a **transferable underlying concept** (computer science, math, ML theory, systems and hardware, networking, statistics, whatever the domain implies), stop and give it a real, in-depth explanation in its own section, even if a one line definition would technically answer the question. The goal is that the reader walks away understanding the *idea*, not just a tool's name for it.

Rule of thumb: if removing the concept would make the reader unable to reason about *any other tool in this space*, it should have a deep dive. If it's really not that important a short note is enough.

Examples of deep-dive-worthy concepts: what a tensor actually is and why shape and dtype matter, what lazy evaluation means and why it exists, CPU vs. GPU vs. unified memory, what a computational graph is, why reference counting differs from garbage collection, what compilation vs. interpretation means for performance, why concurrency primitives exist. Every field has its own version of this. Find it.

## Step 4: Writing style rules

- **Plain language always.** If a simpler word says the same thing, use it. When a technical term is unavoidable, define it in the same sentence or the one right after, in everyday words, before using it again.
- **Analogies over abstraction.** Ground abstract ideas in something physical or familiar, but flag where the analogy breaks down. False intuitions are worse than no intuition.
- **Second person, warm, direct.** Talk to "you," not "the developer" or "one." No academic throat-clearing, no marketing fluff, no filler transitions.
- **Assume nothing. Never condescend** Write for someone smart who genuinely knows nothing about *this*, not for someone who needs baby-talk. Respect the reader's intelligence while assuming zero prior exposure to the subject.
- **Short paragraphs, and short sentences where it matters**, especially right before or after a code sample or a hard idea.
- **Every worked example must be something you're confident actually works**, verified against Step 1's research, not made up for the sake of having a random example.

## Step 5: Verify before you publish

Before delivering the final book, re-check it against its own claims:

- Did every "fact" survive contact with a real source, or did anything sneak in from unverified memory? Fix anything you're not sure of, or soften it ("this is generally true, though check current docs for X").
- Does every jargon or confusing term used in the book appear in the Glossary?
- Does the difficulty actually ramp? Could someone follow Chapter 3 without secretly needing Chapter 7's knowledge first?
- Is there anywhere a definition appears *before* the motivating problem? Reorder if so.

## Step 5.5: Run an unslop pass

A book full of AI writing tells undermines the whole point of this skill: plain, trustworthy explanation. Before final assembly, run every chapter's prose through an unslop pass.

- If the `unslop` skill is available in your environment (it ships alongside this one at `skills/unslop/SKILL.md` in this repo, or install it standalone via `npx skills add https://github.com/cursor/plugins --skill unslop`), run its process on the full text.
- If it isn't available, apply the same idea directly: reread every chapter asking "what makes this obviously AI-written?" Cut significance inflation ("pivotal", "testament to"), stock AI vocabulary ("delve", "underscore", "landscape"), em dashes, title-case headings, bold-label-and-colon list items, chatbot filler ("I hope this helps!"), and hedging piled on hedging. Vary sentence rhythm, use active voice, and let the writer have an actual point of view on the material instead of a neutral, hedge-everything tone.

## Step 6: Assemble and deliver

**Default output: a single self-contained HTML file, styled and structured like mdBook**, the tool that renders books like *The Rust Programming Language*. That means sidebar navigation plus one chapter at a time, not a flat Markdown file.

- **Layout.** A fixed left sidebar holds the full table of contents (Parts as section headers, Chapters as clickable links, plus Glossary and Further Reading at the bottom). The main pane shows one chapter at a time, switched by clicking a sidebar link, with the active chapter highlighted in the sidebar.
- **Navigation.** "← Previous chapter" and "Next chapter →" links at the bottom of each chapter so the reader can read straight through without touching the sidebar.
- **Look and feel.** Clean, readable typography (generous line-height, a comfortable max content width rather than edge-to-edge text), a monospace font with a light background tint for code blocks, clear heading hierarchy, and a distinct visual treatment (border or background tint) for the "concept deep-dive" and "common confusion" boxes so they stand apart from the main narrative.
- **Self-contained.** All CSS and JS inline in the one HTML file, with no external stylesheets, CDNs, or fonts. It should open and fully work offline, exactly like a real mdBook export.
- **Content structure is unchanged.** The Table of Contents, every chapter (still following the Step 2 chapter-level pattern), the Glossary, and Further Reading & Sources are all still written in full. They just live as pages inside this HTML shell instead of as Markdown headings.
**Fallback.** Only if the tool you're running in truly cannot output an HTML file (a plain text-only interface with no file or artifact support), fall back to a single flowing Markdown document with the same Part and Chapter structure, Table of Contents, Glossary, and Sources. Same content, just without the interactive shell.
