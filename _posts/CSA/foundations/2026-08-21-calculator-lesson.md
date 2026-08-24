---
title: Calculator Lesson — Objects & Methods
description: Build a Calculator class in Java and practice objects, instantiation, methods, the Math class, casting, and operators.
layout: post
toc: True
codemirror: True
courses: {'csa': {'week': 1}}
permalink: /csa/calculator-lesson
quiz:
  - q: "What does the `new Calculator(10, 4)` call actually do?"
    choices:
      - "Instantiates a Calculator object and runs its constructor"
      - "Declares a variable named Calculator"
      - "Calls the add() method with 10 and 4"
      - "Imports the Calculator class"
    answer: 0
  - q: "firstNumber and secondNumber are declared as double. Why does that matter for divide()?"
    choices:
      - "It doesn't matter — Java always does decimal division"
      - "double operands make division return a decimal result instead of truncating like int division would"
      - "It makes the method run faster"
      - "It's required for the method to compile"
    answer: 1
  - q: "What's the safest fix for divide() silently returning Infinity or NaN when secondNumber is 0?"
    choices:
      - "Change secondNumber to an int"
      - "Use Math.pow instead of dividing"
      - "Throw an ArithmeticException when secondNumber == 0 before dividing"
      - "Wrap the call in a try/catch that ignores the error"
    answer: 2
---

## Building a Calculator in Java

A calculator is one of the best first projects for learning **object-oriented programming** in Java. Instead of writing one long script, you'll build a `Calculator` **class** — an object that holds its own state (the numbers) and exposes **methods** that act on that state.

By the end of this lesson you'll have practiced:
- **Objects & Instantiation** — creating a `Calculator` with `new`
- **Variables & Expressions** — storing operands and results
- **Operators & Casting** — `+ - * /`, and why `7 / 2` isn't `3.5`
- **The `Math` class** — `Math.pow`, `Math.sqrt` for bonus operations
- **Methods & Comments** — organizing behavior, documenting intent
- **`String` methods & I/O** — formatting and printing results

Every code box below is **live** — click **Run ▶** to execute it for real, edit it, and run it again.

---

## Step 1: Define the Class

Every calculator needs somewhere to keep its numbers. We'll store them as `private` fields and set them through a **constructor** — this is **instantiation** in action.

```java
public class Calculator {
    private double firstNumber;
    private double secondNumber;

    // Constructor: runs once, when you write `new Calculator(...)`
    public Calculator(double firstNumber, double secondNumber) {
        this.firstNumber = firstNumber;
        this.secondNumber = secondNumber;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator(10, 4);
        System.out.println("Calculator created!");
    }
}
```

{% capture challenge_class %}
Run the starter code to instantiate a <code>Calculator</code>. Then add a <code>getFirstNumber()</code> method that returns <code>firstNumber</code>, and print <code>calc.getFirstNumber()</code>.
{% endcapture %}

{% capture code_class %}
public class Calculator {
    private double firstNumber;
    private double secondNumber;

    public Calculator(double firstNumber, double secondNumber) {
        this.firstNumber = firstNumber;
        this.secondNumber = secondNumber;
    }

    // TODO: add a getFirstNumber() method that returns firstNumber

    public static void main(String[] args) {
        Calculator calc = new Calculator(10, 4);
        System.out.println("Calculator created!");
        // TODO: print calc.getFirstNumber()
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="calc_class"
   language="java"
   challenge=challenge_class
   code=code_class
   height="380px"
%}

---

## Step 2: Operations — Methods + the `Math` Class

Now give the calculator something to *do*. Each operation is a **method** that reads the fields and returns a result.

```java
public double add()      { return firstNumber + secondNumber; }
public double subtract() { return firstNumber - secondNumber; }
public double multiply() { return firstNumber * secondNumber; }
public double divide()   { return firstNumber / secondNumber; }

// Bonus: the Math class gives you operations for free
public double power()    { return Math.pow(firstNumber, secondNumber); }
```

<div class="rpn-popcorn">
    <div class="rpn-popcorn__header">
        <h3>Popcorn Hack: Integer Division</h3>
        <p>Suppose <code>int firstNumber = 7;</code> and <code>int secondNumber = 2;</code>, and you compute <code>firstNumber / secondNumber</code>. What's the result?</p>
    </div>
    <div class="rpn-popcorn__body">
        <div class="rpn-popcorn__options" id="calc-ph1-options">
            <button onclick="checkCalcPH1(0)" class="rpn-popcorn__option">A) 3.5</button>
            <button onclick="checkCalcPH1(1)" class="rpn-popcorn__option">B) 3</button>
            <button onclick="checkCalcPH1(2)" class="rpn-popcorn__option">C) 4</button>
            <button onclick="checkCalcPH1(3)" class="rpn-popcorn__option">D) Compilation error</button>
        </div>
        <div id="calc-ph1-feedback" class="rpn-popcorn__feedback"></div>
    </div>
</div>

<script>
function checkCalcPH1(sel) {
    const btns = document.querySelectorAll('#calc-ph1-options .rpn-popcorn__option');
    const fb = document.getElementById('calc-ph1-feedback');
    btns.forEach(b => b.className = 'rpn-popcorn__option');
    if (sel === 1) {
        btns[1].classList.add('rpn-popcorn__option--correct');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--correct';
        fb.innerHTML = '<strong style="color:#2ecc71;">Correct!</strong> When both operands are <code>int</code>, Java performs <strong>integer division</strong> and truncates the decimal — <code>7 / 2</code> is <code>3</code>, not <code>3.5</code>. To get a decimal answer, cast at least one operand: <code>(double) firstNumber / secondNumber</code>.';
    } else {
        btns[sel].classList.add('rpn-popcorn__option--incorrect');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--incorrect';
        fb.innerHTML = '<strong style="color:#e74c3c;">Not quite.</strong> Two <code>int</code> operands always produce <code>int</code> division in Java — the result truncates toward zero, giving <code>3</code>.';
    }
}
</script>

{% capture challenge_ops %}
Fill in <code>subtract()</code>, <code>multiply()</code>, and <code>divide()</code> so the test output shows correct values for all four operations. Then add a <code>power()</code> method using <code>Math.pow</code> and test it.
{% endcapture %}

{% capture code_ops %}
public class Calculator {
    private double firstNumber;
    private double secondNumber;

    public Calculator(double firstNumber, double secondNumber) {
        this.firstNumber = firstNumber;
        this.secondNumber = secondNumber;
    }

    public double add() { return firstNumber + secondNumber; }

    // TODO: subtract()
    // TODO: multiply()
    // TODO: divide()
    // TODO: power() using Math.pow

    public static void main(String[] args) {
        Calculator calc = new Calculator(10, 4);
        System.out.println("10 + 4 = " + calc.add());
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="calc_ops"
   language="java"
   challenge=challenge_ops
   code=code_ops
   height="420px"
%}

---

## Step 3: Put It Together

A full calculator ties the class to user-facing output — building `String`s and printing results.

```java
public class Calculator {
    private double firstNumber;
    private double secondNumber;

    public Calculator(double firstNumber, double secondNumber) {
        this.firstNumber = firstNumber;
        this.secondNumber = secondNumber;
    }

    public double add()      { return firstNumber + secondNumber; }
    public double subtract() { return firstNumber - secondNumber; }
    public double multiply() { return firstNumber * secondNumber; }
    public double divide()   { return firstNumber / secondNumber; }
    public double power()    { return Math.pow(firstNumber, secondNumber); }

    public String summary() {
        return String.format("%.1f + %.1f = %.1f", firstNumber, secondNumber, add());
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator(10, 4);
        System.out.println(calc.summary());
        System.out.println("Difference: " + calc.subtract());
        System.out.println("Product: " + calc.multiply());
        System.out.println("Quotient: " + calc.divide());
        System.out.println("Power: " + calc.power());
    }
}
```

{% capture challenge_main %}
Run the finished calculator. Then add a <code>remainder()</code> method using the <code>%</code> operator and print it, and try changing <code>String.format</code> to use two decimal places instead of one.
{% endcapture %}

{% capture code_main %}
public class Calculator {
    private double firstNumber;
    private double secondNumber;

    public Calculator(double firstNumber, double secondNumber) {
        this.firstNumber = firstNumber;
        this.secondNumber = secondNumber;
    }

    public double add()      { return firstNumber + secondNumber; }
    public double subtract() { return firstNumber - secondNumber; }
    public double multiply() { return firstNumber * secondNumber; }
    public double divide()   { return firstNumber / secondNumber; }
    public double power()    { return Math.pow(firstNumber, secondNumber); }

    public String summary() {
        return String.format("%.1f + %.1f = %.1f", firstNumber, secondNumber, add());
    }

    // TODO: add a remainder() method using %

    public static void main(String[] args) {
        Calculator calc = new Calculator(10, 4);
        System.out.println(calc.summary());
        System.out.println("Difference: " + calc.subtract());
        System.out.println("Product: " + calc.multiply());
        System.out.println("Quotient: " + calc.divide());
        System.out.println("Power: " + calc.power());
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="calc_main"
   language="java"
   challenge=challenge_main
   code=code_main
   height="480px"
%}

---

## Show Solution: A Safer `divide()`

<div class="rpn-reveal">
    <div class="rpn-reveal__header">
        <h3>What happens when you divide by zero?</h3>
        <p>Try it in Step 3 above by editing the constructor to <code>new Calculator(10, 0)</code> and calling <code>divide()</code>. Think about what should happen, then reveal one way to guard against it.</p>
    </div>
    <div class="rpn-reveal__body">
        <button class="rpn-reveal__toggle-btn" onclick="var a=document.getElementById('calc-reveal-answer'); a.style.display = a.style.display === 'block' ? 'none' : 'block';">Show / Hide Answer</button>
        <div class="rpn-reveal__answer" id="calc-reveal-answer">
            <h4>A Guarded divide()</h4>
            <div class="rpn-reveal__code-block"><pre>public double divide() {
    if (secondNumber == 0) {
        throw new ArithmeticException("Cannot divide by zero");
    }
    return firstNumber / secondNumber;
}</pre></div>
            <p class="key-detail">With <code>double</code> operands, Java doesn't actually crash on <code>x / 0</code> — it returns <code>Infinity</code> or <code>NaN</code>. Throwing an exception yourself is often clearer and safer than letting a silent <code>NaN</code> travel through the rest of your program.</p>
        </div>
    </div>
</div>

---

## Hacks

Extend the `Calculator` class. Check off each one as you finish it — your progress is saved in this browser.

<div class="calc-hacks" id="calc-hacks">
  <div class="calc-hacks__progress">
    <div class="calc-hacks__progress-bar"><div class="calc-hacks__progress-fill" id="calc-hacks-fill"></div></div>
    <span id="calc-hacks-count">0 / 5 complete</span>
  </div>
  <label class="calc-hacks__item"><input type="checkbox" data-hack="0"><span><strong>Hack 1 — Modulo:</strong> Add a <code>remainder()</code> method using <code>%</code>, and print <code>firstNumber % secondNumber</code>.</span></label>
  <label class="calc-hacks__item"><input type="checkbox" data-hack="1"><span><strong>Hack 2 — Guard division:</strong> Make <code>divide()</code> throw or return a message instead of silently producing <code>Infinity</code> / <code>NaN</code> when <code>secondNumber == 0</code>.</span></label>
  <label class="calc-hacks__item"><input type="checkbox" data-hack="2"><span><strong>Hack 3 — Console input:</strong> Use <code>java.util.Scanner</code> to read two numbers and an operator from the user instead of hardcoding them.</span></label>
  <label class="calc-hacks__item"><input type="checkbox" data-hack="3"><span><strong>Hack 4 — <code>toString()</code>:</strong> Override <code>toString()</code> so <code>System.out.println(calc)</code> prints a readable summary automatically.</span></label>
  <label class="calc-hacks__item"><input type="checkbox" data-hack="4"><span><strong>Hack 5 — New operation:</strong> Add <code>sqrt()</code> (via <code>Math.sqrt</code>) or <code>percentage()</code>, with a matching method and test.</span></label>
</div>

<style>
  .calc-hacks { max-width: 700px; margin: 20px auto; }
  .calc-hacks__progress { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
  .calc-hacks__progress-bar { flex: 1; height: 8px; border-radius: 999px; background: var(--panel-mid); overflow: hidden; }
  .calc-hacks__progress-fill { height: 100%; width: 0%; background: var(--pref-accent-color); transition: width 0.3s ease; }
  #calc-hacks-count { font-size: 13px; color: var(--text-muted); white-space: nowrap; }
  .calc-hacks__item { display: flex; align-items: flex-start; gap: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid var(--ui-border); border-radius: 8px; background: var(--pref-bg-color); cursor: pointer; transition: border-color 0.2s ease, background 0.2s ease; }
  .calc-hacks__item:hover { border-color: var(--pref-accent-color); }
  .calc-hacks__item input { margin-top: 3px; accent-color: var(--pref-accent-color); cursor: pointer; }
  .calc-hacks__item span { color: var(--pref-text-color); line-height: 1.5; font-size: 14px; }
  .calc-hacks__item:has(input:checked) { opacity: 0.6; }
  .calc-hacks__item:has(input:checked) span { text-decoration: line-through; }
</style>

<script>
(function () {
  var KEY = 'calc-lesson-hacks';
  var box = document.getElementById('calc-hacks');
  var checks = box.querySelectorAll('input[type=checkbox]');
  var fill = document.getElementById('calc-hacks-fill');
  var count = document.getElementById('calc-hacks-count');

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
