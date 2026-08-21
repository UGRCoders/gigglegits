---
title: Data Collections Lesson — Arrays, ArrayLists & Recursion
description: Practice arrays, 2D arrays, ArrayLists, wrapper classes, searching, sorting, and recursion in Java by tracking a bakery's cookie sales data.
layout: post
toc: True
codemirror: True
courses: {'csa': {'week': 4}}
permalink: /csa/data-collections-lesson
---

## Data Collections: Arrays, ArrayLists & Recursion

Real programs rarely deal with just one number — they deal with **collections** of data: a week of sales, a roster of students, a grid of pixels. This lesson uses one running example, a small bakery's daily cookie sales, to practice every major way Java stores and processes collections.

By the end of this lesson you'll have practiced:
- **Arrays & Traversal** — fixed-size lists, walking through them with a loop
- **Array Algorithms** — computing a sum, max, or average from an array
- **ArrayLists & Wrapper Classes** — growable lists, and why `ArrayList<int>` doesn't compile
- **2D Arrays & Traversal** — grids, walked with nested loops
- **Searching & Sorting** — finding and ordering data
- **Recursion** — a function that calls itself to process a collection

Every code box below is **live** — click **Run ▶** to execute it for real, edit it, and run it again.

---

## Step 1: Arrays — Traversal & Algorithms

An array holds a **fixed number** of values of the same type. A `for` loop **traverses** it — visits every element in order.

```java
int[] cookieSales = {42, 58, 39, 71, 64, 80, 55}; // one week, Sun-Sat

int total = 0;
for (int i = 0; i < cookieSales.length; i++) {
    total += cookieSales[i];
}
double average = (double) total / cookieSales.length;

System.out.println("Total sold: " + total);
System.out.println("Average per day: " + average);
```

Notice `(double) total / cookieSales.length` — without that cast, `int / int` truncates and you'd lose the decimal part of the average.

{% capture challenge_array %}
Run the code to see the weekly total and average. Then add code that finds the <strong>busiest day</strong> — the largest value in <code>cookieSales</code> — by traversing the array and tracking the maximum as you go.
{% endcapture %}

{% capture code_array %}
int[] cookieSales = {42, 58, 39, 71, 64, 80, 55};

int total = 0;
for (int i = 0; i < cookieSales.length; i++) {
    total += cookieSales[i];
}
double average = (double) total / cookieSales.length;

System.out.println("Total sold: " + total);
System.out.println("Average per day: " + average);

// TODO: traverse cookieSales again and find the largest value (busiest day)
{% endcapture %}

{% include runners/code.html
   runner_id="dc_array"
   language="java"
   challenge=challenge_array
   code=code_array
   height="440px"
%}

---

## Step 2: ArrayLists & Wrapper Classes

Arrays can't grow. An `ArrayList` can — but it only stores **objects**, not primitives. That's why `ArrayList<int>` won't compile: you need the **wrapper class** `Integer` instead. Java quietly converts back and forth (**autoboxing**).

```java
import java.util.ArrayList;

ArrayList<Integer> orders = new ArrayList<Integer>();
orders.add(12);   // autoboxed: int 12 -> Integer.valueOf(12)
orders.add(7);
orders.add(19);

int firstOrder = orders.get(0); // auto-unboxed: Integer -> int

for (int order : orders) {
    System.out.println("Order size: " + order);
}
System.out.println("Number of orders: " + orders.size());
```

<div class="rpn-popcorn">
    <div class="rpn-popcorn__header">
        <h3>Popcorn Hack: Wrapper Classes</h3>
        <p>Why does <code>ArrayList&lt;Integer&gt;</code> compile, but <code>ArrayList&lt;int&gt;</code> does not?</p>
    </div>
    <div class="rpn-popcorn__body">
        <div class="rpn-popcorn__options" id="dc-ph1-options">
            <button onclick="checkDcPH1(0)" class="rpn-popcorn__option">A) <code>int</code> is misspelled — Java expects <code>Int</code></button>
            <button onclick="checkDcPH1(1)" class="rpn-popcorn__option">B) Generic types like <code>ArrayList&lt;T&gt;</code> require an object type, and <code>int</code> is a primitive, not an object</button>
            <button onclick="checkDcPH1(2)" class="rpn-popcorn__option">C) <code>ArrayList</code> can only hold <code>String</code>s</button>
            <button onclick="checkDcPH1(3)" class="rpn-popcorn__option">D) There's no real difference; both work identically</button>
        </div>
        <div id="dc-ph1-feedback" class="rpn-popcorn__feedback"></div>
    </div>
</div>

<script>
function checkDcPH1(sel) {
    const btns = document.querySelectorAll('#dc-ph1-options .rpn-popcorn__option');
    const fb = document.getElementById('dc-ph1-feedback');
    btns.forEach(b => b.className = 'rpn-popcorn__option');
    if (sel === 1) {
        btns[1].classList.add('rpn-popcorn__option--correct');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--correct';
        fb.innerHTML = '<strong style="color:#2ecc71;">Correct!</strong> Generics only work with reference types (objects). <code>Integer</code> is a full object wrapping an <code>int</code> value, so it satisfies that requirement — <code>int</code> itself, a primitive, does not. Java automatically converts between <code>int</code> and <code>Integer</code> for you (autoboxing/unboxing), so you can still write plain <code>int</code> code most of the time.';
    } else {
        btns[sel].classList.add('rpn-popcorn__option--incorrect');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--incorrect';
        fb.innerHTML = '<strong style="color:#e74c3c;">Not quite.</strong> The real rule: Java generics (the <code>&lt;...&gt;</code> part) only accept object types, never primitives like <code>int</code>, <code>double</code>, or <code>boolean</code>. That\'s exactly why wrapper classes like <code>Integer</code> exist.';
    }
}
</script>

{% capture challenge_arraylist %}
Add two more orders to the <code>ArrayList</code>. Then write a loop that computes the <strong>total</strong> of all orders (you'll need a running sum, just like Step 1, but traversing an <code>ArrayList</code> instead of an array).
{% endcapture %}

{% capture code_arraylist %}
import java.util.ArrayList;

ArrayList<Integer> orders = new ArrayList<Integer>();
orders.add(12);
orders.add(7);
orders.add(19);

// TODO: add two more orders

for (int order : orders) {
    System.out.println("Order size: " + order);
}
System.out.println("Number of orders: " + orders.size());
// TODO: compute and print the total of all orders
{% endcapture %}

{% include runners/code.html
   runner_id="dc_arraylist"
   language="java"
   challenge=challenge_arraylist
   code=code_arraylist
   height="440px"
%}

---

## Step 3: 2D Arrays — Grids & Nested Traversal

A `int[][]` is an array of arrays — perfect for a grid, like a month of sales broken into weeks. A **nested loop** traverses it: the outer loop picks the row, the inner loop walks across that row.

```java
int[][] monthlySales = {
    {42, 58, 39, 71, 64, 80, 55}, // Week 1
    {50, 62, 45, 68, 70, 85, 60}, // Week 2
    {38, 55, 40, 65, 58, 75, 50}  // Week 3
};

int monthTotal = 0;
for (int week = 0; week < monthlySales.length; week++) {
    int weekTotal = 0;
    for (int day = 0; day < monthlySales[week].length; day++) {
        weekTotal += monthlySales[week][day];
    }
    System.out.println("Week " + (week + 1) + " total: " + weekTotal);
    monthTotal += weekTotal;
}
System.out.println("Month total: " + monthTotal);
```

{% capture challenge_2d %}
Add a fourth week to <code>monthlySales</code>. Then find the single <strong>busiest day in the whole month</strong> by tracking a maximum as you traverse both dimensions (you'll need variables for the best value found, and which week/day it was on).
{% endcapture %}

{% capture code_2d %}
int[][] monthlySales = {
    {42, 58, 39, 71, 64, 80, 55},
    {50, 62, 45, 68, 70, 85, 60},
    {38, 55, 40, 65, 58, 75, 50}
};

// TODO: add a 4th week array

int monthTotal = 0;
for (int week = 0; week < monthlySales.length; week++) {
    int weekTotal = 0;
    for (int day = 0; day < monthlySales[week].length; day++) {
        weekTotal += monthlySales[week][day];
    }
    System.out.println("Week " + (week + 1) + " total: " + weekTotal);
    monthTotal += weekTotal;
}
System.out.println("Month total: " + monthTotal);

// TODO: traverse monthlySales again to find the single busiest day
{% endcapture %}

{% include runners/code.html
   runner_id="dc_2d"
   language="java"
   challenge=challenge_2d
   code=code_2d
   height="460px"
%}

---

## Step 4: Searching & Sorting

**Linear search** checks every element until it finds a match — it works on any array, sorted or not. **Sorting** first (with `Arrays.sort`) makes a much faster search possible afterward.

```java
import java.util.Arrays;

int[] cookieSales = {42, 58, 39, 71, 64, 80, 55};

// Linear search: is there a day with exactly 71 sales?
boolean found = false;
for (int i = 0; i < cookieSales.length; i++) {
    if (cookieSales[i] == 71) {
        found = true;
        System.out.println("Found 71 sales on day index " + i);
        break;
    }
}
if (!found) System.out.println("No day had exactly 71 sales.");

// Sorting
Arrays.sort(cookieSales);
System.out.println("Sorted: " + Arrays.toString(cookieSales));
```

{% capture challenge_search %}
Run the code, then write your own linear search that looks for a day with <strong>39</strong> sales instead of 71. After that, try <code>Arrays.binarySearch(cookieSales, 55)</code> on the <em>sorted</em> array — binary search only works correctly once the array is sorted.
{% endcapture %}

{% capture code_search %}
import java.util.Arrays;

int[] cookieSales = {42, 58, 39, 71, 64, 80, 55};

boolean found = false;
for (int i = 0; i < cookieSales.length; i++) {
    if (cookieSales[i] == 71) {
        found = true;
        System.out.println("Found 71 sales on day index " + i);
        break;
    }
}
if (!found) System.out.println("No day had exactly 71 sales.");

Arrays.sort(cookieSales);
System.out.println("Sorted: " + Arrays.toString(cookieSales));

// TODO: linear search for 39 in the ORIGINAL (unsorted) order — do it before the sort runs
// TODO: try Arrays.binarySearch(cookieSales, 55) on the sorted array and print the result
{% endcapture %}

{% include runners/code.html
   runner_id="dc_search"
   language="java"
   challenge=challenge_search
   code=code_search
   height="460px"
%}

---

## Step 5: Recursion

A **recursive** method solves a problem by calling itself on a smaller version of the same problem, until it reaches a **base case** simple enough to answer directly.

```java
public static int recursiveSum(int[] arr, int index) {
    if (index == arr.length) {   // base case: nothing left to add
        return 0;
    }
    return arr[index] + recursiveSum(arr, index + 1); // recursive case
}

int[] cookieSales = {42, 58, 39, 71, 64, 80, 55};
System.out.println("Recursive total: " + recursiveSum(cookieSales, 0));
```

Compare this to Step 1's loop-based sum — same answer, different technique. The loop repeats; the recursive method delegates to a smaller version of itself, one element closer to the base case each time.

{% capture challenge_recursion %}
Trace through <code>recursiveSum</code> by hand for a 3-element array before running it — write down what each call returns. Then write a recursive method <code>recursiveMax(int[] arr, int index)</code> that finds the largest value instead of the sum.
{% endcapture %}

{% capture code_recursion %}
public static int recursiveSum(int[] arr, int index) {
    if (index == arr.length) {
        return 0;
    }
    return arr[index] + recursiveSum(arr, index + 1);
}

// TODO: write recursiveMax(int[] arr, int index) — think about what the base case should return

int[] cookieSales = {42, 58, 39, 71, 64, 80, 55};
System.out.println("Recursive total: " + recursiveSum(cookieSales, 0));
// TODO: call and print recursiveMax(cookieSales, 0)
{% endcapture %}

{% include runners/code.html
   runner_id="dc_recursion"
   language="java"
   challenge=challenge_recursion
   code=code_recursion
   height="460px"
%}

---

## Show Solution: `recursiveMax`

<div class="rpn-reveal">
    <div class="rpn-reveal__header">
        <h3>What does the base case return for a maximum?</h3>
        <p><code>recursiveSum</code>'s base case returns <code>0</code> — adding nothing changes nothing. What should <code>recursiveMax</code>'s base case return instead, and why can't it also be <code>0</code>?</p>
    </div>
    <div class="rpn-reveal__body">
        <button class="rpn-reveal__toggle-btn" onclick="var a=document.getElementById('dc-reveal-answer'); a.style.display = a.style.display === 'block' ? 'none' : 'block';">Show / Hide Answer</button>
        <div class="rpn-reveal__answer" id="dc-reveal-answer">
            <h4>Return the Last Element, Not Zero</h4>
            <div class="rpn-reveal__code-block"><pre>public static int recursiveMax(int[] arr, int index) {
    if (index == arr.length - 1) {   // base case: one element left
        return arr[index];
    }
    int maxOfRest = recursiveMax(arr, index + 1);
    return Math.max(arr[index], maxOfRest);
}</pre></div>
            <p class="key-detail">If sales could ever be negative, a base case of <code>0</code> would silently produce a wrong "maximum" of 0 even when every real value was negative. The base case has to return an <em>actual element</em> so every possible array value is honestly considered.</p>
        </div>
    </div>
</div>

---

## Why This Matters: Ethics, Data Sets & Text Files

<div class="rpn-popcorn__key-point">
    <div class="key-title">Beyond the Syntax</div>
    <div class="key-detail">
        Three ideas from the AP CSA Data Collections unit aren't things you type — they're things you think about:
        <br><br>
        <strong>Data Sets:</strong> the <code>cookieSales</code> array in this lesson is a tiny data set. Real programs load much larger ones — sensor readings, survey responses, transaction logs — and the same array/ArrayList techniques scale up to them.
        <br><br>
        <strong>Text Files:</strong> instead of hardcoding <code>{42, 58, 39, ...}</code>, a real program often reads each value from a line of a text file (using classes like <code>Scanner</code> or <code>BufferedReader</code>) and loads it into an array or ArrayList — same collection, different source.
        <br><br>
        <strong>Ethics:</strong> once sales data includes real customers — names, purchase history, locations — collecting and storing it responsibly matters: who can see it, how long it's kept, and whether people consented to it being recorded at all. The technical skill of building a collection doesn't answer the question of whether — or how — it should be built.
    </div>
</div>

---

## Hacks

Extend the examples above. Check off each one as you finish it — your progress is saved in this browser.

<div class="dc-hacks" id="dc-hacks">
  <div class="dc-hacks__progress">
    <div class="dc-hacks__progress-bar"><div class="dc-hacks__progress-fill" id="dc-hacks-fill"></div></div>
    <span id="dc-hacks-count">0 / 6 complete</span>
  </div>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="0"><span><strong>Hack 1 — Array algorithm:</strong> Write a method that returns the <em>minimum</em> value in an <code>int[]</code>, traversing it once.</span></label>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="1"><span><strong>Hack 2 — ArrayList algorithm:</strong> Given an <code>ArrayList&lt;Integer&gt;</code> of orders, write a method that removes every order under a given size.</span></label>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="2"><span><strong>Hack 3 — 2D traversal:</strong> Given the <code>monthlySales</code> grid, print each week's <em>average</em>, not just its total.</span></label>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="3"><span><strong>Hack 4 — Sorting:</strong> Sort <code>monthlySales[0]</code> (one week) in <em>descending</em> order without using <code>Arrays.sort</code> directly — write your own simple sort (e.g. selection sort).</span></label>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="4"><span><strong>Hack 5 — Recursion:</strong> Write a recursive method that counts how many days in an array exceed a given threshold.</span></label>
  <label class="dc-hacks__item"><input type="checkbox" data-hack="5"><span><strong>Hack 6 — Wrapper classes:</strong> Convert an <code>int[]</code> into an <code>ArrayList&lt;Integer&gt;</code> (and back), noting where autoboxing happens.</span></label>
</div>

<style>
  .dc-hacks { max-width: 700px; margin: 20px auto; }
  .dc-hacks__progress { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
  .dc-hacks__progress-bar { flex: 1; height: 8px; border-radius: 999px; background: var(--panel-mid); overflow: hidden; }
  .dc-hacks__progress-fill { height: 100%; width: 0%; background: var(--pref-accent-color); transition: width 0.3s ease; }
  #dc-hacks-count { font-size: 13px; color: var(--text-muted); white-space: nowrap; }
  .dc-hacks__item { display: flex; align-items: flex-start; gap: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid var(--ui-border); border-radius: 8px; background: var(--pref-bg-color); cursor: pointer; transition: border-color 0.2s ease, background 0.2s ease; }
  .dc-hacks__item:hover { border-color: var(--pref-accent-color); }
  .dc-hacks__item input { margin-top: 3px; accent-color: var(--pref-accent-color); cursor: pointer; }
  .dc-hacks__item span { color: var(--pref-text-color); line-height: 1.5; font-size: 14px; }
  .dc-hacks__item:has(input:checked) { opacity: 0.6; }
  .dc-hacks__item:has(input:checked) span { text-decoration: line-through; }
</style>

<script>
(function () {
  var KEY = 'dc-lesson-hacks';
  var box = document.getElementById('dc-hacks');
  var checks = box.querySelectorAll('input[type=checkbox]');
  var fill = document.getElementById('dc-hacks-fill');
  var count = document.getElementById('dc-hacks-count');

  function load() {
    try { return JSON.parse(localStorage.getItem(KEY) || '{}'); } catch (e) { return {}; }
  }
  function save(state) {
    try { localStorage.setItem(KEY, JSON.stringify(state)); } catch (e) {}
  }
  function render() {
    var state = load();
    var done = 0;
    checks.forEach(function (cb) {
      var on = !!state[cb.dataset.hack];
      cb.checked = on;
      if (on) done++;
    });
    fill.style.width = (done / checks.length * 100) + '%';
    count.textContent = done + ' / ' + checks.length + ' complete';
  }

  checks.forEach(function (cb) {
    cb.addEventListener('change', function () {
      var state = load();
      state[cb.dataset.hack] = cb.checked;
      save(state);
      render();
    });
  });

  render();
})();
</script>
