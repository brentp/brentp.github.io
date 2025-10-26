---
title: Brent Pedersen
description: Genomics researcher
---

I am a genomics researcher and software developer focused on creating useful, simple, fast and reliable tools for variant analysis and genomic data processing. I use rust/python/nim and other programming languages where suitable. I use git, nextflow, AWS, and machine learning as needed for WGS, WES and other sequencing data. I am looking for contract work that is interesting and impactful and where my skills can be best utilized.

## Work With Me

 I am interested in longer projects where I am more integrated than a contractor, but less commitment (to you) than a staff member. A model I have in mind is *16 weeks* (~1/3rd year) of focused work for $25K commitment. This could be for a pilot study or a focused project or certainly a long-term collaboration. Most universities can support this via vendor contract or even simpler.
If you have a smaller project or something else in mind, feel free to <a href="mailto:bpederse@gmail.com?subject=Genomics%20Contracting" target="_blank" rel="noopener">contact me</a>.

---

## Recommendations

<div id="recommendations-rotator" aria-live="polite">Loading recommendations...</div>
<script>
(function() {
  const el = document.getElementById('recommendations-rotator');
  if (!el) return;
  fetch('recs.txt')
    .then(function(r) { return r.text(); })
    .then(function(t) {
      const entries = t.split(/^---\s*$/m).map(function(s) { return s.trim(); }).filter(function(s) { return s.length; });
      if (!entries.length) {
        el.textContent = 'No recommendations available.';
        return;
      }
      var i = 0;
      function render() {
        var lines = entries[i].split('\n').map(function(line) { return line.trim(); }).filter(function(s){ return s.length; });
        var person = '';
        if (lines.length && /^-\s*/.test(lines[lines.length - 1])) {
          person = lines.pop().replace(/^-\s*/, '');
        }
        var bodyHtml = lines.join('<br>');
        el.innerHTML = '<blockquote class="rec-body">' + bodyHtml + '</blockquote>' +
                       '<div class="rec-person">— <em>' + (person || '') + '</em></div>';
        var bodyEl = el.querySelector('.rec-body');
        if (bodyEl) {
          var cs = window.getComputedStyle(bodyEl);
          var lh = parseFloat(cs.lineHeight);
          if (!isNaN(lh) && lh > 0) {
            bodyEl.style.maxHeight = (lh * 4) + 'px';
            bodyEl.style.overflowY = 'auto';
          }
          bodyEl.scrollTop = 0;
        }
      }
      render();
      setInterval(function() {
        i = (i + 1) % entries.length;
        render();
      }, 8000);
    })
    .catch(function() {
      el.textContent = 'Failed to load recommendations.';
    });
})();
</script>

## Key Projects

<div class="grid cards" markdown>

- :material-speedometer:{ .lg .middle } **[mosdepth](https://github.com/brentp/mosdepth){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/mosdepth?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/mosdepth?style=social)
  <br> Fast BAM/CRAM depth calculation for WGS, exome, or targeted sequencing. Written in Nim for maximum performance.
  <br><hr> :material-book-open-page-variant: [Mosdepth: quick coverage calculation for genomes and exomes.](https://doi.org/10.1093/bioinformatics/btx699){:target="\_blank"}

- :material-dna:{ .lg .middle } **[somalier](https://github.com/brentp/somalier){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/somalier?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/somalier?style=social)
  <br> Fast sample-swap and relatedness checks on BAMs/CRAMs/VCFs/GVCFs. Essential for quality control in genomic studies.
  <br><hr> :material-book-open-page-variant: [Somalier: rapid relatedness estimation for cancer and germline studies using efficient sketches.](https://doi.org/10.1186/s13073-020-00761-2){:target="\_blank"}

- :material-filter:{ .lg .middle } **[slivar](https://github.com/brentp/slivar){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/slivar?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/slivar?style=social)
  <br> Genetic variant expressions, annotation, and filtering for great good. Streamlines variant analysis workflows.
  <br><hr> :material-book-open-page-variant: [Effective variant filtering and expected candidate variant yield in studies of rare human disease.](https://doi.org/10.1038/s41525-021-00227-3){:target="\_blank"}

- :material-language-go:{ .lg .middle } **[vcfanno](https://github.com/brentp/vcfanno){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/vcfanno?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/vcfanno?style=social)
  <br> Annotate a VCF with other VCFs/BEDs/tabixed files. Written in Go for speed and reliability.
  <br><hr> :material-book-open-page-variant: [VCFanno: fast, flexible annotation of genetic variants.](https://doi.org/10.1186/s13059-016-0973-5){:target="\_blank"}

- :material-language-python:{ .lg .middle } **[cyvcf2](https://github.com/brentp/cyvcf2){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/cyvcf2?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/cyvcf2?style=social)
  <br> Cython + htslib for fast VCF and BCF processing. Core library for many Python-based genomic tools.
  <br><hr> :material-book-open-page-variant: [cyvcf2: fast, flexible variant analysis with Python/Cython.](https://doi.org/10.1093/bioinformatics/btx057){:target="\_blank"}

- :material-cog:{ .lg .middle } **[echtvar](https://github.com/brentp/echtvar){:target="\_blank"}** ![GitHub stars](https://img.shields.io/github/stars/brentp/echtvar?style=social) ![GitHub forks](https://img.shields.io/github/forks/brentp/echtvar?style=social)
  <br> Using all the bits for echt rapid variant annotation and filtering. Written in Rust for maximum performance.
  <br><hr> :material-book-open-page-variant: [Echtvar: compressed variant representation for rapid annotation and filtering of SNPs and indels.](https://doi.org/10.1093/nar/gkac931){:target="\_blank"}

</div>

---

## Technical Expertise

I have extensive experience in developing in [rust](https://www.rust-lang.org/), [python/cython](https://cython.org/) (extension modules and entire software), and [nim](https://nim-lang.org/) for high-performance bioinformatics tools. My expertise includes **genomics**, **variant analysis**, and performance optimization for large-scale genomic data processing.

My work has been in developing [efficient](https://github.com/brentp/mosdepth), [algorithms](https://github.com/brentp/echtvar), largely in [variant filtering](https://github.com/brentp/slivar), and [QC](https://github.com/brentp/somalier)

---

## Recent Activity

Check out the [blog section](blog/index.md) for the latest posts and updates on my research and software development work.

---

## Connect

- **GitHub**: [github.com/brentp](https://github.com/brentp)
- **Google Scholar**: [Profile](https://scholar.google.com/citations?user=tDf0VkUAAAAJ&hl=en)
- **Location**: Oregon, USA
- **Twitter**: [@brent_p](https://twitter.com/brent_p)
- [**email**](mailto:bpederse@gmail.com)
