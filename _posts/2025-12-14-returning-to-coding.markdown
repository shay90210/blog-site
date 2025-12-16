---
layout: post
title:  "YAML Is Simple Until It Isn’t: My First Real Config File Mistake"
date:   2025-12-13 05:00:00 +0000
categories: jekyll update
---
YAML feels deceptively friendly. It’s clean, readable, and at first glance looks like something you could casually edit without much risk. That illusion lasted right up until my Jekyll site refused to run — not because of Ruby, not because of a missing gem, but because of a single formatting mistake inside `_config.yml.`

This wasn’t my first time seeing YAML, but it was my first time understanding how unforgiving configuration files can be when a project depends on them.

### The Setup: A File That Looks Harmless

When you start a Jekyll blog, `_config.yml` feels like a safe place. It’s where you set your site title, description, theme, and plugins. No logic. No loops. No functions. Just key–value pairs.

That sense of safety is misleading.

Unlike HTML or CSS, YAML doesn’t fail gracefully. There’s no partial render, no warning banner. If the file can’t be parsed, Jekyll won’t start at all. Running jekyll serve simply stops everything in its tracks.

That’s exactly what happened to me.

### The Error That Looked Bigger Than It Was

When I ran `jekyll serve`, the terminal exploded with a wall of text. Stack traces. File paths. Ruby internals. It looked serious. But buried in the output was the real clue:

{%highlight ruby %}
could not find expected ':' while scanning a simple key at line 24 column 1
{%endhighlight %}

At first, that line didn’t feel helpful. It sounded abstract and overly technical — especially for something as simple as a config file. But this was the moment where I started learning how to read errors instead of reacting to them. The error wasn’t saying YAML was broken. It was saying my file didn’t match what YAML expects.

### The Mistake: One Line, One Character

The issue ended up being small enough to miss entirely while scrolling:

- A key without a colon

- A line of plain text that didn’t belong

- Or indentation that didn’t match the rest of the file

Any one of those is enough to break YAML parsing.

In my case, I had added content that looked reasonable to a human but made no sense to a parser. YAML doesn’t allow free-floating text. Everything must be part of a defined structure. What surprised me most wasn’t the strictness — it was how confidently I assumed I could just “drop something in” and adjust it later.

YAML doesn’t work that way.

### What This Taught Me About Configuration Files

This experience changed how I think about configuration entirely. Config files aren’t documentation. They’re not notes. They’re instructions. And they need to be precise. Unlike application code, configuration errors don’t usually point to logic problems — they point to structure problems. Spacing. Colons. Dashes. Nesting.

It also made something else click: tools like Jekyll are only as flexible as their configuration allows. _config.yml isn’t optional glue — it’s a contract between you and the tool. If you violate that contract, nothing runs.

### Why This Was a Useful Beginner Mistake

It would be easy to dismiss this as a trivial error. But I don’t think it is.

This was my first real exposure to how fragile systems can be when everything depends on a single source of truth. One missing character didn’t just affect a feature — it shut down the entire development environment. That’s a powerful lesson early on.

It taught me to:

- Slow down when editing configuration

- Respect formatting rules even when they feel unnecessary

- Trust error messages more than my initial assumptions

- Most importantly, it reminded me that being a beginner doesn’t mean avoiding complexity — it means learning how to approach it calmly.

### What I’ll Do Differently Next Time

Going forward, I’m more intentional when working in files like `_config.yml`:

- I make smaller changes and test more often

- I pay attention to indentation and nesting

- I treat config edits with the same care as application code

This won’t be the last time a config file trips me up — but it won’t catch me off guard the same way again.

### Still Learning

YAML is simple until it isn’t. And that line between the two is thinner than I expected. If there’s a takeaway here, it’s this: sometimes the most valuable lessons don’t come from building features — they come from figuring out why nothing works at all.

If you’ve had your own moment like this, I’d love to hear about it. Debugging might be solitary work, but learning doesn’t have to be.