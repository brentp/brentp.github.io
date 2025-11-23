---
title: Brent Pedersen
description: Genomics researcher
---

I am a genomics researcher and software developer focused on creating useful, simple, fast and reliable tools for variant analysis and genomic data processing. I am looking for contract work that is interesting and impactful and where my skills can be best utilized.

## Work With Me

I am interested in substantial projects, but with less commitment (to you) than a staff member. A model I have in mind is _16 weeks_ (~1/3rd year) of focused work for _$25K_ commitment. This could be an alternative to committing to a staff bioinformatician. It could be for a pilot study or a focused project or certainly a long-term collaboration. Most universities can support this via vendor contract or even simpler.
This is an idea, if you have another mode of work or a project in mind, feel free to <a href="mailto:bpederse@gmail.com?subject=Genomics%20Contracting" target="_blank" rel="noopener">contact me</a>.

---

## Recommendations

<div id="recommendations-rotator" aria-live="polite">Loading recommendations...</div>
<script>
(function() {
  const el = document.getElementById('recommendations-rotator');
  if (!el) return;
  
  var entries = [];
  var currentIndex = 0;
  var isPaused = false;
  var intervalId = null;
  var contentEl, indicatorsEl, prevBtn, nextBtn, pauseBtn;
  
  // SVG icons for buttons
  var chevronLeftSVG = '<svg viewBox="0 0 24 24"><polyline points="15 18 9 12 15 6"></polyline></svg>';
  var chevronRightSVG = '<svg viewBox="0 0 24 24"><polyline points="9 18 15 12 9 6"></polyline></svg>';
  var pauseSVG = '<svg viewBox="0 0 24 24"><rect x="6" y="4" width="4" height="16"></rect><rect x="14" y="4" width="4" height="16"></rect></svg>';
  var playSVG = '<svg viewBox="0 0 24 24"><polygon points="5 3 19 12 5 21 5 3"></polygon></svg>';
  
  function render() {
    if (!entries.length || !contentEl) return;
    
    var lines = entries[currentIndex].split('\n').map(function(line) { return line.trim(); }).filter(function(s){ return s.length; });
    var person = '';
    if (lines.length && /^-\s*/.test(lines[lines.length - 1])) {
      person = lines.pop().replace(/^-\s*/, '');
    }
    var bodyHtml = lines.join('<br>');
    contentEl.innerHTML = '<blockquote class="rec-body">' + bodyHtml + '</blockquote>' +
                          '<div class="rec-person">— <em>' + (person || '') + '</em></div>';
    
    var bodyEl = contentEl.querySelector('.rec-body');
    if (bodyEl) {
      bodyEl.scrollTop = 0;
    }
    
    // Update indicators
    updateIndicators();
  }
  
  function updateIndicators() {
    if (!indicatorsEl) return;
    var indicators = indicatorsEl.querySelectorAll('.rec-indicator');
    indicators.forEach(function(indicator, idx) {
      if (idx === currentIndex) {
        indicator.classList.add('active');
        indicator.setAttribute('aria-current', 'true');
      } else {
        indicator.classList.remove('active');
        indicator.removeAttribute('aria-current');
      }
    });
  }
  
  function goToIndex(newIndex) {
    if (newIndex < 0 || newIndex >= entries.length || newIndex === currentIndex) return;
    currentIndex = newIndex;
    render();
    resetInterval();
  }
  
  function goNext() {
    currentIndex = (currentIndex + 1) % entries.length;
    render();
    resetInterval();
  }
  
  function goPrev() {
    currentIndex = (currentIndex - 1 + entries.length) % entries.length;
    render();
    resetInterval();
  }
  
  function togglePause() {
    isPaused = !isPaused;
    if (pauseBtn) {
      var iconEl = pauseBtn.querySelector('.rec-btn-icon');
      if (iconEl) {
        iconEl.innerHTML = isPaused ? playSVG : pauseSVG;
      }
      pauseBtn.setAttribute('aria-label', isPaused ? 'Play' : 'Pause');
      pauseBtn.setAttribute('title', isPaused ? 'Play' : 'Pause');
    }
    
    if (isPaused) {
      clearInterval(intervalId);
      intervalId = null;
    } else {
      startInterval();
    }
  }
  
  function startInterval() {
    if (intervalId) clearInterval(intervalId);
    intervalId = setInterval(function() {
      if (!isPaused) {
        goNext();
      }
    }, 6000);
  }
  
  function resetInterval() {
    if (!isPaused) {
      startInterval();
    }
  }
  
  function createUI() {
    el.classList.add('recommendations-ready');
    el.innerHTML = '';
    
    // Create content container
    contentEl = document.createElement('div');
    contentEl.className = 'rec-content';
    el.appendChild(contentEl);
    
    // Create footer with controls and indicators
    var footer = document.createElement('div');
    footer.className = 'rec-footer';
    
    // Create controls
    var controls = document.createElement('div');
    controls.className = 'rec-controls';
    
    prevBtn = document.createElement('button');
    prevBtn.className = 'rec-btn';
    prevBtn.setAttribute('aria-label', 'Previous recommendation');
    prevBtn.setAttribute('title', 'Previous');
    prevBtn.innerHTML = '<span class="rec-btn-icon rec-btn-icon--chevron">' + chevronLeftSVG + '</span>';
    prevBtn.onclick = goPrev;
    
    pauseBtn = document.createElement('button');
    pauseBtn.className = 'rec-btn';
    pauseBtn.setAttribute('aria-label', 'Pause');
    pauseBtn.setAttribute('title', 'Pause');
    pauseBtn.innerHTML = '<span class="rec-btn-icon rec-btn-icon--toggle">' + pauseSVG + '</span>';
    pauseBtn.onclick = togglePause;
    
    nextBtn = document.createElement('button');
    nextBtn.className = 'rec-btn';
    nextBtn.setAttribute('aria-label', 'Next recommendation');
    nextBtn.setAttribute('title', 'Next');
    nextBtn.innerHTML = '<span class="rec-btn-icon rec-btn-icon--chevron">' + chevronRightSVG + '</span>';
    nextBtn.onclick = goNext;
    
    controls.appendChild(prevBtn);
    controls.appendChild(pauseBtn);
    controls.appendChild(nextBtn);
    
    // Create indicators
    indicatorsEl = document.createElement('div');
    indicatorsEl.className = 'rec-indicators';
    if (entries.length === 1) {
      indicatorsEl.classList.add('rec-indicators--single');
    }
    
    entries.forEach(function(_, idx) {
      var indicator = document.createElement('button');
      indicator.className = 'rec-indicator';
      indicator.setAttribute('aria-label', 'Go to recommendation ' + (idx + 1));
      indicator.setAttribute('title', 'Recommendation ' + (idx + 1));
      indicator.textContent = (idx + 1).toString();
      indicator.onclick = function() {
        goToIndex(idx);
      };
      if (idx === currentIndex) {
        indicator.classList.add('active');
        indicator.setAttribute('aria-current', 'true');
      }
      indicatorsEl.appendChild(indicator);
    });
    
    footer.appendChild(controls);
    footer.appendChild(indicatorsEl);
    el.appendChild(footer);
    
    // Render initial content
    render();
    startInterval();
  }
  
  fetch('assets/recs.txt')
    .then(function(r) { return r.text(); })
    .then(function(t) {
      entries = t.split(/^---\s*$/m).map(function(s) { return s.trim(); }).filter(function(s) { return s.length; });
      if (!entries.length) {
        el.textContent = 'No recommendations available.';
        return;
      }
      createUI();
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

I have extensive experience in developing in [rust](https://www.rust-lang.org/), [python/cython](https://cython.org/) (extension modules and entire software), [nim](https://nim-lang.org/) and [go](https://golang.org/) for high-performance bioinformatics tools. My expertise includes **genomics**, **variant analysis**, and performance optimization for large-scale genomic data processing.

My work has been in developing [efficient](https://github.com/brentp/mosdepth) [algorithms](https://github.com/brentp/echtvar), largely in [variant filtering](https://github.com/brentp/slivar), [annotation](https://github.com/brentp/vcfanno), and [QC](https://github.com/brentp/somalier). I like to add scripting capabilities to command-line tools to give maximum flexibility.

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
