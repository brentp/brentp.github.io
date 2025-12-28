---
title: AI Coding
date: 2025-12-29
description: Writing real software with AI coding tools
tags: [llms, ai, coding, vcf, rust, javascript]
comments: true
---

This post is mostly about AI coding. Jump to the end if you're more interested in genomics libraries.

## AI Coding

I use AI coding tools quite a bit, but over the last couple of weeks without writing a line of code (I may have edited a README), I made

1. a rust package to easily apply javascript expressions to a genomic variant: https://brentp.github.io/htsvcf/latest/htsvcf/

2. a javascript library for reading, writing VCF/BCF and modifying variants: https://www.npmjs.com/package/htsvcf

I mostly used [opencode](https://opencode.ai) and either GPT-5.2 or Claude Opus 4.5 using my [free github credits from having a "popular" open-source project](https://docs.github.com/en/copilot/concepts/billing/individual-plans#github-copilot-pro) (but I do have
a \$20/month Codex sub, a \$20 Cursor sub, and a [$3/month GLM](https://z.ai/subscribe) sub). This was not possible prior to these models (and the progression of CLI coding tools).
Opus 4.5 is very good; like it's different. And faster than GPT-5.2.
Or previously, a project even smaller than this would at least require so much intervention that it would have taken much longer than it did and therefore have been infeasible
as a side project/experiment. And, as a project grew, the complexity would bring down the efficacy of using LLMs; that didn't
happen here. It's still a small project, but it's substantial and I do notice a sea-change. 
I had never published an NPM package prior to this and now have one that's automatically published via github action to be available on
linux x64 and arm along with OSX (can also support whatever [NAPI](https://napi.rs/) supports). The models generally made code that I was
happy with or that was easily adjusted with a single prompt.

This was not a single "vibe-code", but rather on the order of 50 different individual prompts. I would decide a feature:
"Allow setting INFO fields in VCF" or "support extracting genotypes and return as `{ alleles: [0, 1], phase: [false]}` for `0/1`"
and then use `Plan` mode in opencode and then iterate on it and even ask it to find any holes in the plan.
Once the plan was made, I'd let it go Brrrr in `Build` mode and sometimes check in, scroll-back through the output and occasionally
intervene and interrupt it.
My [AGENTS.md](https://agents.md) indicates that the agent should update (specifically) `lib.rs` rust-docs and add tests
and run `cargo clippy` and `fmt`.
When it was done building, I'd look over the diff in [cursor](https://cursor.com) and sometimes ask an LLM there to note any problems
with the diff. Sometimes I'd add a new requirement at this stage and go back into `opencode`. I left opencode to manage
its own context.

I tried Gemini 3.0 a couple times and on brief look the code it generated was fine,
but it was having trouble making edits. It would inject in the wrong place and take time to figure out how to undo the change and then
re-insert it into the correct file location. I didn't notice a single time where this happened with GPT 5.2 or Opus 4.5 though I didn't
review all of the intermediate output.

## The Changing AI Coding Experience

This library that I wrote/managed the writing of is based on something I wanted to do for a long time. I've been embedding scripting interfaces into genomics tools  
[since 2016](https://link.springer.com/article/10.1186/s13059-016-0973-5) and since then have found it quite useful. I prefer 
Javascript syntax but it has always been easier to embed lua and still have good performance.
I had an old `rust` [repo](https://github.com/brentp/help-repositories/tree/976b00c5c4b6d2c023ed92b585cc5b38f0207320)
where I had made a small example and tried to get help to understand why my minimal rust program with V8 scripting was leaking memory. I was not
able to resolve that. In early december, I asked GPT 5.2 to fix the leak and make sure to update to latest v8 crate. It did, in one shot. And we went from 
there. What was striking to me was the rate of change in improvement. I had the sense previously that things were plateauing--the models
were getting better but it wasn't changing that much. This felt very different. I was continually 1, 2, or 3-shotting substantial features with 
tests and documentation. I think writing a wrapper library is probably a nice use-case for the LLMs as they currently are, but the entire experience
was easy. I guess there's a realization that this will continue to improve in months, not years and that what I offer now is taste and high-level guidance.
I am excited about what I can build next. And also wondering what software engineering/programming will look like.
And what will be my place in it. I don't have any deep thoughts here, just noticing this new reality encroaching.

Below I'll write a bit about the actual libraries.

## HTSVCF

Starting from the initial V8 Javascript::rust example project, I built, with opencode and LLMs, a library for
[rust-htslib](https://github.com/rust-bio/rust-htslib) that exposes most attributes 
that are available on a variant in [VCF format](https://pmc.ncbi.nlm.nih.gov/articles/PMC3137218/) to Javascript expressions.
Concurrently, it built a [library](https://www.npmjs.com/package/htsvcf) to read and write VCF files from Javascript (via bun or node).

### rust

I am quite pleased with the syntax of the libraries. For the rust library that facilitates user expressions, the usage looks like this:

```rust
use htsvcf::Evaluator;
use rust_htslib::bcf::{self, Read};

let mut reader = bcf::Reader::from_path("input.vcf.gz")?;
let mut eval = Evaluator::new(reader.header())?;

// Optionally define custom functions
eval.run("function passes(v) { return v.info('DP') > 20 }")?;

for result in reader.records() {
    let record = result?;
    eval.set_record(record);
    
    if eval.eval::<bool>("passes(variant)")? {
        // Use take() to get ownership of the record
        let record = eval.take().unwrap();
        // write record to output, collect it, etc.
    }
}
```

where the optional user function is:

```Javascript
function passes(v) { return v.info('DP') > 20 }
```
and the expression calling it is simply:

```Javascript
eval.eval::<bool>("passes(variant)")
```

so we can handle other return times like i32, f32, f64, and (with some performance consequences) objects that serde::Deserialize can understand.
`variant` is injected into the context for each variant (record) in the VCF file with `set_record`.

There are other examples in the rust docs [here](https://brentp.github.io/htsvcf/latest/htsvcf/index.html)


### Javascript

The Javascript library is available from npm (`bun install -g htsvcf`). And usage looks like:

```Javascript
import { Reader, Writer } from "htsvcf";

const reader = new Reader("samples.vcf.gz");

// Print header info
console.log("Samples:", reader.header.samples());
const dpDef = reader.header.get("INFO", "DP");
console.log(`DP field: ${dpDef.type} (${dpDef.description})`);

// Add a custom INFO field to the header
reader.header.addInfo("HIGHQUAL", "0", "Flag", "Variant passed quality filter");

// Create a writer with the modified header
const writer = new Writer("filtered.vcf.gz", reader.header);

// Process variants. There's also a synchronous variant iterator that will be faster.
for await (const v of reader) {
  // Translate variant to the writer's header (required after modifying header)
  v.translate(writer.header);

  // Filter by quality
  if (v.qual !== null && v.qual < 30) continue;

  // Set our custom flag
  v.set_info("HIGHQUAL", true);

  // Get per-sample data
  for (const s of v.samples()) {
    if (s.DP !== null && s.DP > 10) {
      console.log(`${v.chrom}:${v.pos} ${s.sample_name} DP=${s.DP}`);
    }
  }

  // Write the variant
  writer.write(v);
}

writer.close();
reader.close();
```

I have made efforts to keep both the rust and the Javascript side of things very fast. Please [get in touch](https://github.com/brentp/htsvcf/issues) with any feedback.

AI was *not* used to write this post.

## Shameless Plug

I have been doing contracting work in genomics for some time and am looking for substantial projects in 2026 that are suited to my skills and knowledge with the possibility of helping patients.
Read more about that [here](https://brentp.github.io/latest/) and [send me a message](mailto:bpederse@gmail.com) if you have something in mind.
