---
title: "Hello, World"
description: "First post from the new workbench."
date: 2025-01-31
---

The site is live. Built with Astro, styled with Tailwind v4, running on the claylo brand system.

## What's here

A place to write about:

- Rust development
- CLI tools
- Open source projects
- Whatever else comes up at 2am

## The stack

This site uses:

- **Astro** — static site generation
- **Tailwind v4** — CSS-first configuration
- **Berkeley Mono** — custom font cuts (LL01Display, LL02Code, LL03Text, LL04Caption)
- **MDX** — markdown with components

### A taste of Rust

Here's the kind of thing I'm building these days, styled with [Dusty](https://github.com/claylo/zed-dusty) — my Zed theme:

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

More to come.
