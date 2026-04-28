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
simply because they can use an LLM. And that a way to expose more functionality
is to provide a scripting interface to a command-line tool or low-level
library. We can drop the docs into a [custom GPT](https://help.openai.com/en/articles/8554397-creating-and-editing-gpts) or a [SKILL.md](https://www.gitbook.com/blog/skill-md) and the user can use the full power by writing plain-text
prompts. 

This can, of course, work for command-line tools without a scripting 
interface. Likewise, claude or codex or pi can help a user to
modify low-level code, but if there's already a scripting interface,
like there is for [vcfanno](https://github.com/brentp/vcfanno) 
or [slivar](https://github.com/brentp/slivar), then it's quite powerful
and reduces the maintainence burden.


