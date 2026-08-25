---
layout: post
title: Computer Science A Lessons 25-26
description: >
  A guided sequence of hands-on and learning tasks to help you master the frameworks that power our course.
author: Pranav Santhosh (Curators)
courses: {'csa': {'week': 38}}
type: hacks
permalink: /navigation/csa-lessons/
hubTitle: "CSA Collegeboard Lesson Homepage"
hubDescription: "Explore foundational computer science concepts through interactive lessons. Master data types, using objects and methods, selection and iteration, and class creation."
units:
  - Title: "Using Objects and Methods"
    Description: "Learn about variables, data types, and class methods through interactive coding challenges like building a calculator."
    Categories: ["Algorithms", "Variables", "Expressions", "InputOutput", "Casting", "Operators", "APILibraries", "Comments", "Methods", "MathClass", "Objects", "Instantiation", "StringMethods"]
    Lessons: "/csa/calculator-lesson"
    Image: "/images/classroomcsa/unit1.jpg"
    Alt: "Unit 1 Image"
    Level: 1

  - Title: "Selection and Iteration"
    Description: "Experiment with logic, conditionals, and loops to develop games like Rock Paper Scissors."
    Categories: ["Selection", "Booleans", "IfStatements", "Loops", "Iteration", "StringAlgorithms", "NestedLoops", "RunTime"]
    Lessons: "/csa/rock-paper-scissors-lesson"
    Image: "/images/classroomcsa/unit2.jpg"
    Alt: "Unit 2 Image"
    Level: 2

  - Title: "Class Creation"
    Description: "Understand abstraction, program design, and object-oriented structures by creating your own classes in a Tic Tac Toe project."
    Categories: ["Abstraction", "ProgramDesign", "Classes", "Constructors", "MethodsWriting", "References", "ClassVariables", "Scope", "ThisKeyword"]
    Lessons: "/csa/tictactoe-lesson"
    Image: "/images/classroomcsa/unit3.jpg"
    Alt: "Unit 3 Image"
    Level: 3

  - Title: "Data Collections"
    Description: "Explore data structures and algorithms including arrays, ArrayLists, and recursion through interactive coding projects."
    Categories: ["Ethics", "DataSets", "Arrays", "ArrayTraversals", "ArrayAlgorithms", "TextFiles", "WrapperClasses", "ArrayLists", "ArrayListTraversals", "ArrayListAlgorithms", "TwoDArrays", "TwoDTraversals", "TwoDAlgorithms", "Searching", "Sorting", "Recursion"]
    Lessons: "/csa/data-collections-lesson"
    Image: "/images/classroomcsa/unit4.jpg"
    Alt: "Unit 4 Image"
    Level: 4
---

<div class="csa-hub">
  <div class="csa-hub__header">
    <h1>{{ page.hubTitle }}</h1>
    <p>{{ page.hubDescription }}</p>
  </div>

  <div class="csa-hub__grid">
    {% for unit in page.units %}
    <a class="csa-hub__card" href="{{ unit.Lessons }}">
      <div class="csa-hub__image" style="background-image: url('{{ unit.Image }}');" role="img" aria-label="{{ unit.Alt }}">
        <span class="csa-hub__level">Unit {{ unit.Level }}</span>
      </div>
      <div class="csa-hub__body">
        <h2>{{ unit.Title }}</h2>
        <p>{{ unit.Description }}</p>
        <div class="csa-hub__tags">
          {% for cat in unit.Categories limit: 5 %}
          <span class="csa-hub__tag">{{ cat }}</span>
          {% endfor %}
          {% if unit.Categories.size > 5 %}
          <span class="csa-hub__tag csa-hub__tag--more">+{{ unit.Categories.size | minus: 5 }} more</span>
          {% endif %}
        </div>
        <span class="csa-hub__cta">Start Lesson <span aria-hidden="true">&rarr;</span></span>
      </div>
    </a>
    {% endfor %}
  </div>

  <div class="csa-hub__final-quiz" id="csa-final-quiz" hidden>
    <p class="csa-hub__final-quiz-label">You've opened all 4 units.</p>
    <a class="csa-hub__final-quiz-btn" href="/csa/final-quiz">
      Final Quiz <span aria-hidden="true">&rarr;</span>
    </a>
  </div>
</div>

<script>
(function () {
  var REQUIRED_UNITS = [
    {% for unit in page.units %}"{{ unit.Lessons | split: '/' | last }}"{% unless forloop.last %},{% endunless %}{% endfor %}
  ];
  var section = document.getElementById('csa-final-quiz');
  if (!section) return;

  try {
    var progress = JSON.parse(localStorage.getItem('csa-hub-progress') || '{}');
    var allOpened = REQUIRED_UNITS.every(function (slug) { return !!progress[slug]; });
    if (allOpened) {
      section.hidden = false;
    }
  } catch (e) {}
})();
</script>

<style>
  .csa-hub {
    max-width: 1000px;
    margin: 0 auto;
    padding: 8px 4px 32px;
  }

  .csa-hub__header {
    text-align: center;
    margin-bottom: 32px;
  }

  .csa-hub__header h1 {
    font-size: 2rem;
    font-weight: 700;
    color: var(--pref-text-color);
    margin: 0 0 10px;
  }

  .csa-hub__header p {
    color: var(--text-muted);
    font-size: 1.05rem;
    line-height: 1.6;
    max-width: 640px;
    margin: 0 auto;
  }

  .csa-hub__grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }

  @media (max-width: 640px) {
    .csa-hub__grid {
      grid-template-columns: 1fr;
    }
  }

  .csa-hub__card {
    display: flex;
    flex-direction: column;
    background: var(--pref-bg-color);
    border: 1px solid var(--ui-border);
    border-radius: 14px;
    overflow: hidden;
    text-decoration: none;
    color: inherit;
    transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  }

  .csa-hub__card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
    border-color: var(--pref-accent-color);
  }

  .csa-hub__image {
    position: relative;
    height: 150px;
    background-size: cover;
    background-position: center;
    background-color: var(--panel-mid);
  }

  .csa-hub__level {
    position: absolute;
    top: 12px;
    left: 12px;
    padding: 4px 10px;
    border-radius: 999px;
    background: var(--pref-accent-color);
    color: var(--pref-bg-color);
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.02em;
  }

  .csa-hub__body {
    display: flex;
    flex-direction: column;
    flex: 1;
    padding: 18px 20px 20px;
  }

  .csa-hub__body h2 {
    font-size: 1.15rem;
    font-weight: 700;
    color: var(--pref-text-color);
    margin: 0 0 8px;
  }

  .csa-hub__body p {
    color: var(--text-muted);
    font-size: 0.9rem;
    line-height: 1.55;
    margin: 0 0 14px;
  }

  .csa-hub__tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-bottom: 16px;
  }

  .csa-hub__tag {
    font-size: 11px;
    font-weight: 600;
    padding: 3px 9px;
    border-radius: 999px;
    background: var(--panel-mid);
    color: var(--text-muted);
  }

  .csa-hub__tag--more {
    background: none;
    border: 1px dashed var(--ui-border);
  }

  .csa-hub__cta {
    margin-top: auto;
    font-size: 0.9rem;
    font-weight: 700;
    color: var(--pref-accent-color);
  }

  .csa-hub__card:hover .csa-hub__cta span {
    margin-left: 4px;
  }

  .csa-hub__cta span {
    display: inline-block;
    transition: margin-left 0.2s ease;
  }

  .csa-hub__final-quiz {
    margin-top: 36px;
    padding: 28px 24px;
    text-align: center;
    background: var(--pref-bg-color);
    border: 1px solid var(--ui-border);
    border-radius: 14px;
  }

  .csa-hub__final-quiz-label {
    margin: 0 0 14px;
    font-size: 0.95rem;
    color: var(--text-muted);
  }

  .csa-hub__final-quiz-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 12px 26px;
    border-radius: 999px;
    background: var(--pref-accent-color);
    color: var(--pref-bg-color);
    text-decoration: none;
    font-size: 1rem;
    font-weight: 700;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .csa-hub__final-quiz-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .csa-hub__final-quiz-btn span {
    transition: margin-left 0.2s ease;
  }

  .csa-hub__final-quiz-btn:hover span {
    margin-left: 4px;
  }
</style>
