---
title: AI Scripting
date: 2026-04-28
description: Scripting interfaces help users.
tags: [llms, ai, coding, vcf, rust, javascript]
comments: true
---


# Scripting all the things

For AI in genomics as it currently stands, there's an aspect I haven't
seen mentioned that has been on my mind. In short, it's easier to provide
more complex, powerful, and complete functionality to users without them being overwhelmed
now that they can use an LLM. One way to expose more functionality
is to **provide a scripting interface** to a command-line tool or low-level
library. 

Most often, knobs have been exposed in command-line tools as arguments, and often, not at all (think
of all of the `constant`s that are not exposed to the user). But now, given how good LLMs are
at generating code, it's even more powerful to expose a scripting interface. Then, instead of 200
command-line arguments, it's possible to offer even finer control by embedding a scripting interface.
Previously, this would have required more from users; now it requires that the scripting API be documented.
We can then drop the docs into a [custom GPT](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts) or a [SKILL.md](https://www.gitbook.com/blog/skill-md) and the user can use the full power by writing plain-text
prompts. 

This can, of course, work for command-line tools without a scripting 
interface, but scripting gives LLMs a richer surface to work with. Likewise, Claude or Codex or [Pi](https://pi.dev) can help a user to
modify low-level code, but if there's already a scripting interface,
like there is for [vcfanno](https://github.com/brentp/vcfanno) 
or [slivar](https://github.com/brentp/slivar), then it's quite powerful
and reduces the maintenance burden. For example, a user can ask for a slivar expression that flags rare compound heterozygotes instead of learning every available field and helper function up front.

I've been doing this for some time. Get in touch if you have a relevant project.
