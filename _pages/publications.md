---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

For a complete and up-to-date list of my publications, please visit my <u><a href="https://scholar.google.com/citations?user=ZRSyjGIAAAAJ&hl=en">Google Scholar profile</a></u>.

<style>
.pub-filters {
  margin: 1.5em 0 1em 0;
}
.pub-filters label {
  font-weight: bold;
  font-size: 0.85em;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: #494e52;
  display: block;
  margin-bottom: 0.4em;
}
.filter-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4em;
  margin-bottom: 1em;
}
.filter-pill {
  display: inline-block;
  padding: 0.3em 0.85em;
  font-size: 0.82em;
  border: 1.5px solid #7a8288;
  border-radius: 20px;
  background: #fff;
  color: #494e52;
  cursor: pointer;
  transition: all 0.15s ease;
  user-select: none;
  font-family: -apple-system, ".SFNSText-Regular", "San Francisco", "Roboto", "Segoe UI", "Helvetica Neue", "Lucida Grande", Arial, sans-serif;
}
.filter-pill:hover {
  background: #f0f0f0;
}
.filter-pill.active {
  background: #494e52;
  color: #fff;
  border-color: #494e52;
}
.year-select {
  padding: 0.35em 0.7em;
  font-size: 0.85em;
  border: 1.5px solid #7a8288;
  border-radius: 6px;
  background: #fff;
  color: #494e52;
  font-family: inherit;
  cursor: pointer;
}
.pub-count {
  font-size: 0.82em;
  color: #7a8288;
  margin-top: 0.3em;
}
.pub-entry {
  transition: opacity 0.2s ease;
}
.pub-entry.hidden {
  display: none;
}
</style>

<div class="pub-filters">
  <label>Research Area</label>
  <div class="filter-pills" id="area-filters">
    <span class="filter-pill active" data-area="all">All</span>
    <span class="filter-pill" data-area="Agent-Based Modelling">Agent-Based Modelling</span>
    <span class="filter-pill" data-area="AI Ethics & Fairness">AI Ethics & Fairness</span>
    <span class="filter-pill" data-area="Autonomous Vehicles & Society">Autonomous Vehicles & Society</span>
    <span class="filter-pill" data-area="Computer Vision & VR">Computer Vision & VR</span>
    <span class="filter-pill" data-area="Microbiology & Bioinformatics">Microbiology & Bioinformatics</span>
    <span class="filter-pill" data-area="Public Health & Policy">Public Health & Policy</span>
  </div>

  <label>Year</label>
  <select class="year-select" id="year-filter">
    <option value="all">All years</option>
  </select>

  <div class="pub-count" id="pub-count"></div>
</div>

{% assign sorted_pubs = site.publications | sort: 'date' | reverse %}
{% for post in sorted_pubs %}
  <div class="pub-entry" data-area="{{ post.research_area }}" data-year="{{ post.date | date: '%Y' }}">
    <hr>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p><em>{{ post.venue }}, {{ post.date | date: "%Y" }}</em></p>
    <p>{{ post.excerpt }}</p>
  </div>
{% endfor %}

<script>
(function() {
  var entries = document.querySelectorAll('.pub-entry');
  var pills = document.querySelectorAll('.filter-pill');
  var yearSelect = document.getElementById('year-filter');
  var countEl = document.getElementById('pub-count');

  var years = {};
  entries.forEach(function(e) { years[e.dataset.year] = true; });
  var sortedYears = Object.keys(years).sort().reverse();
  sortedYears.forEach(function(y) {
    var opt = document.createElement('option');
    opt.value = y;
    opt.textContent = y;
    yearSelect.appendChild(opt);
  });

  function applyFilters() {
    var activeArea = document.querySelector('.filter-pill.active').dataset.area;
    var activeYear = yearSelect.value;
    var shown = 0;

    entries.forEach(function(entry) {
      var matchArea = (activeArea === 'all') || (entry.dataset.area === activeArea);
      var matchYear = (activeYear === 'all') || (entry.dataset.year === activeYear);
      if (matchArea && matchYear) {
        entry.classList.remove('hidden');
        shown++;
      } else {
        entry.classList.add('hidden');
      }
    });

    countEl.textContent = 'Showing ' + shown + ' of ' + entries.length + ' publications';
  }

  pills.forEach(function(pill) {
    pill.addEventListener('click', function() {
      pills.forEach(function(p) { p.classList.remove('active'); });
      pill.classList.add('active');
      applyFilters();
    });
  });

  yearSelect.addEventListener('change', applyFilters);

  applyFilters();
})();
</script>
