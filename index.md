---
layout: post
hide: true
title: Open Coding Society
description: Pick your course to start learning, or jump into the blog and search.
permalink: /
---

{%- assign courseKeys = "csa,csp,csse,csh" | split: "," -%}
{%- assign courseDestinations = "/navigation/csa-lessons/,/navigation/courses/,/navigation/courses/,/navigation/courses/" | split: "," -%}

<div class="site-hub">
  <div class="site-hub__header">
    <h1>Open Coding Society</h1>
    <p>Pick a course below to jump straight into its lessons.</p>
  </div>

  <div class="site-hub__grid">
    {%- for key in courseKeys -%}
    {%- assign courseInfo = site.data[key].course -%}
    {%- assign destination = courseDestinations[forloop.index0] -%}
    <a class="site-hub__card" href="{{ site.baseurl }}{{ destination }}">
      <span class="site-hub__code">{{ courseInfo.code }}</span>
      <h2>{{ courseInfo.title }}</h2>
      <p>{{ courseInfo.subtitle }}</p>
      <span class="site-hub__cta">Start Learning <span aria-hidden="true">&rarr;</span></span>
    </a>
    {%- endfor -%}
  </div>

  <div class="site-hub__links">
    <a href="{{ site.baseurl }}/navigation/blogs/">Blog</a>
    <a href="{{ site.baseurl }}/search/">Search</a>
    <a href="{{ site.baseurl }}/capstone/">Capstone</a>
    <a href="{{ site.baseurl }}/navigation/courses/">My Courses</a>
  </div>
</div>

<style>
  .site-hub {
    max-width: 1000px;
    margin: 0 auto;
    padding: 8px 4px 32px;
  }

  .site-hub__header {
    text-align: center;
    margin-bottom: 32px;
  }

  .site-hub__header h1 {
    font-size: 2.1rem;
    font-weight: 700;
    color: var(--pref-text-color);
    margin: 0 0 10px;
  }

  .site-hub__header p {
    color: var(--text-muted);
    font-size: 1.05rem;
    line-height: 1.6;
    max-width: 640px;
    margin: 0 auto;
  }

  .site-hub__grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  @media (max-width: 640px) {
    .site-hub__grid {
      grid-template-columns: 1fr;
    }
  }

  .site-hub__card {
    display: flex;
    flex-direction: column;
    background: var(--pref-bg-color);
    border: 1px solid var(--ui-border);
    border-radius: 14px;
    padding: 22px 22px 20px;
    text-decoration: none;
    color: inherit;
    transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  }

  .site-hub__card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
    border-color: var(--pref-accent-color);
  }

  .site-hub__code {
    display: inline-block;
    align-self: flex-start;
    padding: 4px 10px;
    border-radius: 999px;
    background: var(--pref-accent-color);
    color: var(--pref-bg-color);
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.03em;
    margin-bottom: 12px;
  }

  .site-hub__card h2 {
    font-size: 1.15rem;
    font-weight: 700;
    color: var(--pref-text-color);
    margin: 0 0 8px;
  }

  .site-hub__card p {
    color: var(--text-muted);
    font-size: 0.9rem;
    line-height: 1.55;
    margin: 0 0 14px;
    flex: 1;
  }

  .site-hub__cta {
    margin-top: auto;
    font-size: 0.9rem;
    font-weight: 700;
    color: var(--pref-accent-color);
  }

  .site-hub__card:hover .site-hub__cta span {
    margin-left: 4px;
  }

  .site-hub__cta span {
    display: inline-block;
    transition: margin-left 0.2s ease;
  }

  .site-hub__links {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 28px;
  }

  .site-hub__links a {
    padding: 8px 16px;
    border-radius: 999px;
    border: 1px solid var(--ui-border);
    color: var(--pref-text-color);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 600;
    transition: border-color 0.2s ease, color 0.2s ease;
  }

  .site-hub__links a:hover {
    border-color: var(--pref-accent-color);
    color: var(--pref-accent-color);
  }
</style>
