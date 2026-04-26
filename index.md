---
layout: default
title: Home
show_header: false
---

<style>
.hero {
  padding: 5rem 0 4rem;
}
.hero-eyebrow {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--accent);
  font-weight: 500;
  margin-bottom: 1.25rem;
}
.hero h1 {
  font-family: var(--serif);
  font-size: clamp(2.8rem, 7vw, 4.5rem);
  font-weight: 400;
  line-height: 1.1;
  margin-bottom: 1.5rem;
}
.hero h1 em { font-style: italic; color: var(--accent); }
.hero-desc {
  font-size: 1.05rem;
  color: var(--muted);
  line-height: 1.7;
  margin-bottom: 2.5rem;
  max-width: 480px;
}
.hero-links { display: flex; gap: 1rem; flex-wrap: wrap; }
.btn {
  display: inline-block;
  padding: 0.7rem 1.5rem;
  border-radius: 6px;
  font-size: 0.85rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.2s;
}
.btn-primary { background: var(--accent); color: white; }
.btn-primary:hover { background: #1e3f2a; }
.btn-outline { border: 1px solid var(--border); color: var(--text); background: var(--white); }
.btn-outline:hover { border-color: var(--accent); color: var(--accent); }

.featured-section {
  border-top: 1px solid var(--border);
  padding-top: 3rem;
  margin-top: 2rem;
}
.section-label {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--muted);
  margin-bottom: 1.5rem;
}
.featured-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1.25rem;
}
.feat-card {
  padding: 1.5rem;
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 8px;
  text-decoration: none;
  color: var(--text);
  transition: transform 0.2s, box-shadow 0.2s;
  display: block;
}
.feat-card:hover { transform: translateY(-3px); box-shadow: 0 8px 24px rgba(0,0,0,0.07); }
.feat-icon { font-size: 1.5rem; margin-bottom: 1rem; }
.feat-card h3 { font-family: var(--serif); font-size: 1rem; font-weight: 400; margin-bottom: 0.4rem; }
.feat-card p { font-size: 0.82rem; color: var(--muted); }
</style>

<div class="hero">
  <p class="hero-eyebrow">Data Analyst &amp; Researcher</p>
  <h1>Teo<br/><em>Richard</em></h1>
  <p class="hero-desc">
    I work at the intersection of data, research, and visualization —
    turning complex datasets into clear, compelling stories.
  </p>
  <div class="hero-links">
    <a href="/projects" class="btn btn-primary">View My Work</a>
    <a href="/about" class="btn btn-outline">About Me</a>
  </div>
</div>

<div class="featured-section">
  <p class="section-label">Featured Work</p>
  <div class="featured-grid">
    <a class="feat-card" href="/tidytuesday">
      <div class="feat-icon">📊</div>
      <h3>Tidy Tuesday</h3>
      <p>Weekly data visualization challenges.</p>
    </a>
    <a class="feat-card" href="/wtp">
      <div class="feat-icon">💡</div>
      <h3>Willingness to Pay</h3>
      <p>Consumer valuation research.</p>
    </a>
    <a class="feat-card" href="/energy">
      <div class="feat-icon">⚡</div>
      <h3>Energy Poverty</h3>
      <p>Energy access and policy research.</p>
    </a>
    <a class="feat-card" href="/projects">
      <div class="feat-icon">🗂️</div>
      <h3>Other Projects</h3>
      <p>More data work and visualizations.</p>
    </a>
  </div>
</div>
