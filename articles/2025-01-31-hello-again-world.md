# Hello Again, World

The site is live. Built with Astro, styled with Tailwind v4, running on claylo.dev.

> **Updated 2026-03-05:** Since this post went up, the site grew teeth. Agent-written release posts, per-project RSS feeds, OG images for every article, JSON-LD with dynamic authorship, AI crawler access, and an llms.txt endpoint. The "place to write" became a place to ship.

## What's here

A place to write about building tools—and increasingly, building them **with** AI agents.

- Rust development and CLI tooling
- Agent-assisted open source releases
- The mechanics of shipping with Claude as a collaborator
- Whatever else comes up at 2am

## What's shipping

Two projects are live with agent-written release posts:

- **[claylo-rs](/projects/claylo-rs/)** — a Copier-based Rust project template with 38 feature flags, CI, docs site generation, and Homebrew distribution. Seven betas deep.
- **[gh-coda](/projects/gh-coda/)** — a GitHub CLI extension for declarative repo configuration. Description, topics, secrets, variables—all from a YAML file.

Every release post has a "How We Built This" section written by the agent that helped build it. Not a gimmick—it's the most interesting part. The agent's perspective on dead ends, design tradeoffs, and implementation surprises is genuinely useful context that would otherwise evaporate.

## The stack

This site uses:

- **Astro** — static site generation with content collections
- **Tailwind v4** — CSS-first configuration
- **Atkinson Hyperlegible Next** — body text, designed for readability
- **Berkeley Mono** — custom font cuts for headings, code, and captions
- **Markdown** — plain Markdown in a [separate repo](https://github.com/claylo/claylo), no frontmatter in the files themselves. A custom loader extracts H1 as title and merges external `frontmatter.yml`.

The content pipeline is two repos: [claylo/claylo](https://github.com/claylo/claylo) for prose, [claylo/dev](https://github.com/claylo/dev) for the site. Push to one triggers a build of the other. Content is readable as normal Markdown on GitHub—no components, no frontmatter blocks, no framework lock-in.

## The agent workflow

The interesting part isn't the stack—it's how the site gets built. Claude writes release posts, generates OG images, manages RSS feeds, and runs publish-phase validation gates before anything goes live. Two custom skills enforce quality: one for articles, one for release posts. Both have hard gates that block `draft: false` until description length, tags, images, JSON-LD, and build verification all pass.

It's not "AI-generated content" in the slop sense. It's a collaboration where the agent does the structured work—scaffolding, validation, metadata—and the human does the thinking. The agent writes the "How We Built This" sections because it was literally there. That's not generated, that's reporting.

### A taste of Rust

Here's the kind of thing I'm building these days, styled with [Dusty](https://github.com/claylo/dusty-zed) — my Zed theme:

```rust
/// A builder for greeting messages.
/// Doc comments appear in a lighter blue.
#[derive(Debug, Clone)]
pub struct Greeter<'a> {
    name: &'a str,
    excited: bool,
}

impl<'a> Greeter<'a> {
    // Regular comments are muted and italic
    pub fn new(name: &'a str) -> Self {
        Self { name, excited: false }
    }

    pub fn with_excitement(mut self) -> Self {
        self.excited = true;
        self
    }

    pub fn greet(&self) -> String {
        let punctuation = if self.excited { "!" } else { "." };
        format!("Hello, {}{}", self.name, punctuation)
    }
}

fn main() {
    let message = Greeter::new("world")
        .with_excitement()
        .greet();
    println!("{message}");
}
```

More to come. A lot more, apparently.
