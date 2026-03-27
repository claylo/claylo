# Markdown Cosplay: How MDX Ruins Everything Markdown Got Right

I spent today writing a parser to extract structured data from a 1,560-line React component that was inlined in a Markdown file.

Read that sentence again. A **fifteen hundred line React component**. In a `.md` file. With `useState`, `useEffect`, `requestAnimationFrame`, fullscreen toggle handlers, CSS custom properties for dark mode, and a blinking cursor animation. In a documentation file about how context windows work.

This is what [MDX](https://mdxjs.com/) has done to us.

## The Sad Trombone Downloads

Claude Code publishes an [`llms.txt`](https://web.archive.org/web/20260317091844/https://code.claude.com/docs/llms.txt) file that links to its documentation. The links end in `.md`. You click one, expecting Markdown -- the universally portable, human-readable, works-everywhere format that John Gruber [designed](https://daringfireball.net/projects/markdown/syntax) to be "publishable as-is, as plain text."

What you get is MDX.

And the only thing it's missing is a sad trombone sound playing as it loads.

Here's what I mean. Open [`context-window.md`](https://web.archive.org/web/20260327020614/https://code.claude.com/docs/en/context-window.md) and you'll find:

```javascript
export const ContextWindow = () => {
  const MAX = 200000;
  const STARTUP_END = 0.2;
  const EVENTS = useMemo(() => [{}, {
    t: 0.015,
    kind: 'auto',
    label: 'System prompt',
    tokens: 4200,
    // ... 1,540 more lines of React
```

That's not documentation. That's a React application wearing a `.md` extension like a fake mustache.

## What's Actually In There

I found three distinct horrors in Claude Code's docs today. Each one is a case study in how MDX lets frontend engineers replace documentation with software.

**Horror #1: [The ContextWindow Component](https://web.archive.org/web/20260327020614/https://code.claude.com/docs/en/context-window.md)** -- 1,560 lines of inline React that renders an animated timeline visualization. It has an EVENTS array with 36 structured data objects containing genuinely useful information about what loads into Claude's context window, when, and how many tokens it costs. That data is *great*. It's buried inside a component that manages animation frames, keyboard event listeners, fullscreen state, scroll positions, and hover indices.

**Horror #2: [The Experiment Component](https://web.archive.org/web/20260327020614/https://code.claude.com/docs/en/quickstart.md)** -- an A/B testing framework. In a documentation file. With FNV-1a hashing for user bucketing, GDPR consent country detection (a hardcoded `Set` of 50+ country codes), cookie parsing, `localStorage` management, and an analytics event POST to `api.anthropic.com`. This isn't documentation infrastructure. This is product analytics infrastructure that someone shoved into [`quickstart.md`](https://web.archive.org/web/20260327020614/https://code.claude.com/docs/en/quickstart.md).

**Horror #3: The InstallConfigurator** — a 500-line interactive install wizard with platform detection (`(/Win/).test(navigator.userAgent)`), clipboard API integration, four provider options (Anthropic, Bedrock, Vertex, Foundry), a team/individual toggle, and 240 lines of CSS. All inline. In the [quickstart](https://web.archive.org/web/20260327020614/https://code.claude.com/docs/en/quickstart.md). Wrapped in the A/B test from Horror #2. The exact same install commands already exist ten lines below in standard Markdown tabs.

## Gruber's Gracious Silence

John Gruber has never publicly mentioned MDX. Not once. Given that the man created Markdown specifically so that documents would be "publishable as-is, as plain text, without looking like it's been marked up with tags or formatting instructions" — his restraint is genuinely impressive.

He *has* spoken, once, about what he envisioned for extending Markdown. When Stripe released Markdoc in 2022 — a format they built specifically because MDX didn't work for their docs at scale — Gruber [blessed it](https://daringfireball.net/linked/2022/05/19/markdoc):

> "I avoided using curly braces in Markdown itself — even though they are very tempting characters — to unofficially reserve them for implementation-specific extensions."

He said it "warms my heart to see Markdown continuing to grow like this."

Markdoc. Not MDX. The format that enforces **separation between code and content**. The one Stripe built because, in their words, "[having content mixed with arbitrary code made it incredibly hard to reason about either](https://markdoc.dev/docs/faq)."

The silence on MDX is deafening.

## "You Can't Unmix Cake"

Knut Melvaer, formerly at Sanity.io, [wrote the definitive takedown](https://dev.to/kmelve/on-the-limits-of-mdx-1c8k) back in 2020 (see also his [Smashing Magazine piece](https://www.smashingmagazine.com/2022/02/thoughts-on-markdown/)). The whole thing is worth reading, but the key line is this:

> "You can't unmix cake."

Once you've mixed React components into your content, **you can't get the content back out** without parsing JavaScript. Your documentation is no longer data. It's code. It requires a React runtime, a JSX parser, and the specific component library it was written against to render. Try moving it to a different site, a different framework, a PDF pipeline, a Dash docset, an LLM context payload -- anything, really -- and you're writing a custom extraction tool.

Which is exactly what I spent today doing.

He also nailed the contributor experience:

> "when I have been made to write MDX. It. just. doesn't. work. I mess the syntax up all the time."

And the fundamental problem:

> "Writing with a markup syntax should be opt-in, not forced upon you."

## The Real Cost

Here's what Anthropic's docs team may not realize: people are building things on top of their documentation. I'm building [a Dash docset](https://github.com/claylo/navel) (and a PDF, and several other things) so developers can search Claude Code docs offline. Others are feeding these docs to LLMs -- which is literally what `llms.txt` was designed for. The format says `.md`. The contract says Markdown. What ships is an application.

Every time they replace readable content with a React component, they're not just making a design choice for their website. They're _breaking the downstream contract_ with everyone who treats their docs as data. (Their choice, yes ... but they should have the decency to be clear. Every file linked from their `llms.txt` should end in `.mdx`, **not** `.md`.)

The `ContextWindow` component is the perfect example. The 36-event `EVENTS` array contains some of the most useful documentation Anthropic has published about how Claude Code actually works. Token counts for every type of context. Visibility indicators for what you see vs. what Claude sees. Tips for reducing context usage. Links to deeper docs. It's **excellent** content.

... and it's trapped inside a `useMemo` hook.

## The Punchline

I ran the numbers.

Anthropic's `context-window.md` — the file their `llms.txt` links to, the one with the 1,560-line React component — is **18,501 tokens**. I counted with [bito](https://github.com/claylo/bito), a token-counting tool I built on top of [ah-ah-ah](https://github.com/claylo/ah-ah-ah), a Rust tokenizer library. Then I verified against Anthropic's own [token counting API](https://docs.anthropic.com/en/docs/build-with-claude/token-counting), because if you're going to put numbers in a blog post, you check them.

The version I extracted with [navel](https://github.com/claylo/navel) -- same content, same data, same documentation value, just without the React component, the animation engine, the keyboard handlers, the CSS custom properties, and the fullscreen toggle?

**551 tokens.**

| | Raw MDX | Extracted Markdown |
|---|---:|---:|
| Anthropic API | 18,501 | 551 |
| bito (claude backend) | 18,239 | 555 |
| Lines | 1,596 | 30 |

That's a **97%** noise ratio. Ninety. Seven. Percent.

And here's the part that should make the `llms.txt` crowd wince: this file is linked from a specification *designed for LLM consumption*. You are feeding an LLM 18,501 tokens so it can try to make sense of 551 tokens of actual content buried inside a `useMemo` hook. That's not documentation. That's a context window attack.

## What Should Happen

Look, I get the appeal. Interactive visualizations are cool! A/B testing your install flow is smart product work. Platform-aware install commands are a nice touch. But **none of this belongs in the content layer**.

Stripe figured this out years ago. Their docs are some of the best in the industry, and they built an entire format — [Markdoc](https://markdoc.dev) — around the principle that content should be declarative data, not imperative code. Components render the content. They don't *contain* it.

Respectfully, Anthropic's docs team should:

1. **Keep the data in Markdown.** The `EVENTS` array is documentation. Write it as a Markdown table, a definition list, or structured YAML frontmatter. Render it however you want on the website. But let the data live in a format that anything can consume.

2. **Keep the interactivity in the rendering layer.** Want an animated timeline? Build a component that *reads* the data from the Markdown. Don't inline the data inside the component inside the Markdown.

3. **Stop shipping `.md` files that aren't Markdown.** If it requires a React runtime to render, call it `.mdx` and be honest about it. Or better yet, ship actual Markdown alongside the MDX for consumers who just want the content. Your `llms.txt` links should point to documents an LLM can actually read.

4. **Absolutely do not put A/B testing infrastructure in documentation files.** What are we even doing here. Did I have to actually write that sentence.

Listen, if we can't trust Anthropic to link to Markdown when they _say_ they're linking to Markdown, where does it end?

<div style="display:flex;justify-content:center"><blockquote class="twitter-tweet"><p lang="en" dir="ltr">nah it's just a bonus 2x, it's not that deep</p>&mdash; Thariq (@trq212) <a href="https://twitter.com/trq212/status/2033217604685647921?ref_src=twsrc%5Etfw">March 15, 2026</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script></div>

... never mind.


## The Pattern Forward

Here's the thing that bugs me most: the trend is accelerating. The `ContextWindow` component didn't exist a few versions ago. The `InstallConfigurator` is wrapped in an A/B test -- meaning someone is measuring whether to *replace* the Markdown tabs with the React widget permanently ([earlier version here](https://web.archive.org/web/20260123031439/https://code.claude.com/docs/en/quickstart.md)). When the test "wins," the standard Markdown goes away, and the only source of truth for "how to install Claude Code" lives inside a 500-line React component in a file with a `.md` extension.

This is the trajectory. And it's the wrong one.

Markdown's genius was never the syntax. It was the contract: **what you write is what you can read, and what you can read is what anything can process.** MDX breaks that contract. Not sometimes. Every time. By design.

You can't unmix cake. But you _can_ stop putting React in the batter.
