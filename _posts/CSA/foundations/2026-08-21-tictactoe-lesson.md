---
title: Tic Tac Toe Lesson — Class Creation
description: Design a TicTacToeBoard class in Java and practice abstraction, constructors, methods, references, scope, class variables, and the this keyword.
layout: post
toc: True
codemirror: True
courses: {'csa': {'week': 3}}
permalink: /csa/tictactoe-lesson
quiz:
  - q: "Inside the constructor, what does this.cells refer to versus a plain cells parameter of the same name?"
    choices:
      - "They always mean the exact same thing"
      - "this.cells is the object's field, while plain cells refers to the closer, local parameter"
      - "this.cells is a typo and would not compile"
      - "plain cells always wins and this.cells is ignored"
    answer: 1
  - q: "You pass a TicTacToeBoard into a method that calls board.markCell(0, 'X'). Does the original board show the mark after the method returns?"
    choices:
      - "No, Java copies the whole object into the method"
      - "Yes, because the method received a reference to the same object in memory"
      - "Only if markCell is declared static"
      - "Only if cells is declared public"
    answer: 1
  - q: "Why is boardsCreated declared static in the TicTacToeBoard class?"
    choices:
      - "So each board object gets its own separate copy of the counter"
      - "static fields run faster than instance fields"
      - "So there is exactly one shared copy of the counter across every TicTacToeBoard instance"
      - "static is required for any int field"
    answer: 2
---

## Designing a Tic-Tac-Toe Board Class

Tic-Tac-Toe is a small enough game that you can hold the whole board in your head — which makes it a great way to practice **abstraction**: deciding what a `TicTacToeBoard` *is* (its data) and what it *can do* (its methods), before worrying about a full game loop.

By the end of this lesson you'll have practiced:
- **Abstraction & Program Design** — modeling a board as an object instead of loose variables
- **Classes & Constructors** — building an object's starting state
- **The `this` keyword** — telling a field apart from a same-named parameter
- **Methods & Scope** — where a variable lives, and who can see it
- **References** — what really happens when you hand an object to a method
- **Class variables** — data shared by *every* instance, not just one

Every code box below is **live** — click **Run ▶** to execute it for real, edit it, and run it again.

---

## Step 1: The Class, the Constructor, and `this`

A `TicTacToeBoard` needs somewhere to store its 9 cells. We'll use a `char[]` array of length 9, all starting as `'-'` for empty.

```java
public class TicTacToeBoard {
    private char[] cells;

    // Constructor: builds the starting state of a new board
    public TicTacToeBoard() {
        this.cells = new char[9];
        for (int i = 0; i < this.cells.length; i++) {
            this.cells[i] = '-';
        }
    }

    public void print() {
        for (int i = 0; i < cells.length; i++) {
            System.out.print(cells[i] + " ");
            if (i % 3 == 2) System.out.println();
        }
    }

    public static void main(String[] args) {
        TicTacToeBoard board = new TicTacToeBoard();
        board.print();
    }
}
```

`this.cells` refers to *this particular object's* array. Without `this`, `cells` inside the constructor could be ambiguous if a parameter happened to share the name — `this` always means "the field that belongs to me."

{% capture challenge_class %}
Run the starter code to see an empty board print. Then add a second constructor parameter, <code>char startSymbol</code>, and use it to fill every cell with <code>startSymbol</code> instead of <code>'-'</code>. Watch how <code>this.cells[i] = startSymbol;</code> uses the parameter, not a field.
{% endcapture %}

{% capture code_class %}
public class TicTacToeBoard {
    private char[] cells;

    public TicTacToeBoard() {
        this.cells = new char[9];
        for (int i = 0; i < this.cells.length; i++) {
            this.cells[i] = '-';
        }
    }

    // TODO: add a constructor that takes `char startSymbol` and fills the board with it

    public void print() {
        for (int i = 0; i < cells.length; i++) {
            System.out.print(cells[i] + " ");
            if (i % 3 == 2) System.out.println();
        }
    }

    public static void main(String[] args) {
        TicTacToeBoard board = new TicTacToeBoard();
        board.print();
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="ttt_class"
   language="java"
   challenge=challenge_class
   code=code_class
   height="480px"
%}

---

## Step 2: Writing Methods — Scope & References

A `markCell` method changes one cell. Notice that `row`, `col`, and `index` only exist *inside* this method — that's **scope**. They disappear the moment the method returns.

```java
public boolean markCell(int index, char player) {
    if (index < 0 || index >= cells.length || cells[index] != '-') {
        return false; // invalid or already taken
    }
    cells[index] = player;
    return true;
}
```

<div class="rpn-popcorn">
    <div class="rpn-popcorn__header">
        <h3>Popcorn Hack: References</h3>
        <p>You pass a <code>TicTacToeBoard</code> object into a method, and that method calls <code>board.markCell(0, 'X')</code> on it. After the method returns, does the <em>original</em> board object (back where you called from) show the mark?</p>
    </div>
    <div class="rpn-popcorn__body">
        <div class="rpn-popcorn__options" id="ttt-ph1-options">
            <button onclick="checkTttPH1(0)" class="rpn-popcorn__option">A) No — Java copies the whole object into the method</button>
            <button onclick="checkTttPH1(1)" class="rpn-popcorn__option">B) Yes — the method received a reference to the same object in memory</button>
            <button onclick="checkTttPH1(2)" class="rpn-popcorn__option">C) Only if the method is <code>static</code></button>
            <button onclick="checkTttPH1(3)" class="rpn-popcorn__option">D) It depends on whether <code>cells</code> is <code>private</code></button>
        </div>
        <div id="ttt-ph1-feedback" class="rpn-popcorn__feedback"></div>
    </div>
</div>

<script>
function checkTttPH1(sel) {
    const btns = document.querySelectorAll('#ttt-ph1-options .rpn-popcorn__option');
    const fb = document.getElementById('ttt-ph1-feedback');
    btns.forEach(b => b.className = 'rpn-popcorn__option');
    if (sel === 1) {
        btns[1].classList.add('rpn-popcorn__option--correct');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--correct';
        fb.innerHTML = '<strong style="color:#2ecc71;">Correct!</strong> Java passes object <strong>references</strong> by value — the method gets its own copy of the reference, but that reference still points at the exact same board in memory. Mutating the object through it (like calling <code>markCell</code>) is visible everywhere that object is used.';
    } else {
        btns[sel].classList.add('rpn-popcorn__option--incorrect');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--incorrect';
        fb.innerHTML = '<strong style="color:#e74c3c;">Not quite.</strong> Java never copies whole objects into methods — it copies the <em>reference</em> (the "address"), and both the caller and the method end up pointing at the same underlying object. Changing the object\'s fields through either reference is visible to both.';
    }
}
</script>

{% capture challenge_scope %}
Add <code>markCell</code> to the class below. Then write a small test: mark index <code>0</code> with <code>'X'</code>, try marking index <code>0</code> again with <code>'O'</code> (it should fail — print whether each call returned <code>true</code> or <code>false</code>), then print the board.
{% endcapture %}

{% capture code_scope %}
public class TicTacToeBoard {
    private char[] cells;

    public TicTacToeBoard() {
        this.cells = new char[9];
        for (int i = 0; i < this.cells.length; i++) {
            this.cells[i] = '-';
        }
    }

    // TODO: add markCell(int index, char player) — see the lesson text above

    public void print() {
        for (int i = 0; i < cells.length; i++) {
            System.out.print(cells[i] + " ");
            if (i % 3 == 2) System.out.println();
        }
    }

    public static void main(String[] args) {
        TicTacToeBoard board = new TicTacToeBoard();
        // TODO: mark index 0 with 'X', print the result
        // TODO: try marking index 0 again with 'O', print the result
        board.print();
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="ttt_scope"
   language="java"
   challenge=challenge_scope
   code=code_scope
   height="480px"
%}

---

## Step 3: Class Variables — Shared Across Every Board

An **instance variable** like `cells` belongs to one object. A **class variable** (marked `static`) is shared by *every* instance — there's only ever one copy, no matter how many boards you create.

```java
public class TicTacToeBoard {
    private char[] cells;
    private static int boardsCreated = 0; // shared by ALL TicTacToeBoard objects

    public TicTacToeBoard() {
        this.cells = new char[9];
        for (int i = 0; i < this.cells.length; i++) {
            this.cells[i] = '-';
        }
        boardsCreated++; // every new board bumps the SAME shared counter
    }

    public static int getBoardsCreated() {
        return boardsCreated;
    }

    public static void main(String[] args) {
        TicTacToeBoard a = new TicTacToeBoard();
        TicTacToeBoard b = new TicTacToeBoard();
        TicTacToeBoard c = new TicTacToeBoard();
        System.out.println("Boards created: " + TicTacToeBoard.getBoardsCreated());
    }
}
```

Notice `TicTacToeBoard.getBoardsCreated()` is called on the **class**, not on `a`, `b`, or `c` — because the count doesn't belong to any one board, it belongs to the class itself.

{% capture challenge_static %}
Run the code to confirm the counter reads <code>3</code>. Then add a second static field, <code>gameId</code>, that each board stores as an <em>instance</em> field set from the counter at construction time (so each board remembers "I was board #2", etc.) — print each board's <code>gameId</code>.
{% endcapture %}

{% capture code_static %}
public class TicTacToeBoard {
    private char[] cells;
    private static int boardsCreated = 0;

    public TicTacToeBoard() {
        this.cells = new char[9];
        for (int i = 0; i < this.cells.length; i++) {
            this.cells[i] = '-';
        }
        boardsCreated++;
        // TODO: store this board's own id (its boardsCreated value at creation time)
    }

    public static int getBoardsCreated() {
        return boardsCreated;
    }

    public static void main(String[] args) {
        TicTacToeBoard a = new TicTacToeBoard();
        TicTacToeBoard b = new TicTacToeBoard();
        TicTacToeBoard c = new TicTacToeBoard();
        System.out.println("Boards created: " + TicTacToeBoard.getBoardsCreated());
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="ttt_static"
   language="java"
   challenge=challenge_static
   code=code_static
   height="480px"
%}

---

## Show Solution: Disambiguating With `this`

<div class="rpn-reveal">
    <div class="rpn-reveal__header">
        <h3>What if a constructor parameter shares a field's name?</h3>
        <p>Suppose you want a constructor parameter literally named <code>cells</code>, same as the field. How does Java know which one you mean inside the constructor?</p>
    </div>
    <div class="rpn-reveal__body">
        <button class="rpn-reveal__toggle-btn" onclick="var a=document.getElementById('ttt-reveal-answer'); a.style.display = a.style.display === 'block' ? 'none' : 'block';">Show / Hide Answer</button>
        <div class="rpn-reveal__answer" id="ttt-reveal-answer">
            <h4><code>this.cells</code> vs. plain <code>cells</code></h4>
            <div class="rpn-reveal__code-block"><pre>public TicTacToeBoard(char[] cells) {
    this.cells = cells; // this.cells = the FIELD, cells = the PARAMETER
}</pre></div>
            <p class="key-detail">Inside that constructor, plain <code>cells</code> always refers to the closer, more local thing — the parameter — because of how <strong>scope</strong> works. <code>this.cells</code> reaches past the parameter to explicitly grab the object's own field. Without <code>this</code>, you'd have no way to assign the parameter's value into the field — you'd just be overwriting the parameter with itself.</p>
        </div>
    </div>
</div>

---

## Hacks

Extend the `TicTacToeBoard` class above. Check off each one as you finish it — your progress is saved in this browser.

<div class="ttt-hacks" id="ttt-hacks">
  <div class="ttt-hacks__progress">
    <div class="ttt-hacks__progress-bar"><div class="ttt-hacks__progress-fill" id="ttt-hacks-fill"></div></div>
    <span id="ttt-hacks-count">0 / 5 complete</span>
  </div>
  <label class="ttt-hacks__item"><input type="checkbox" data-hack="0"><span><strong>Hack 1 — <code>toString()</code>:</strong> Override <code>toString()</code> so <code>System.out.println(board)</code> prints the grid automatically, without calling <code>print()</code>.</span></label>
  <label class="ttt-hacks__item"><input type="checkbox" data-hack="1"><span><strong>Hack 2 — <code>hasWinner()</code>:</strong> Write a method that checks all 8 winning lines (3 rows, 3 columns, 2 diagonals) and returns the winning character, or <code>'-'</code> if none.</span></label>
  <label class="ttt-hacks__item"><input type="checkbox" data-hack="2"><span><strong>Hack 3 — <code>reset()</code>:</strong> Add a method that clears every cell back to <code>'-'</code> without creating a new object.</span></label>
  <label class="ttt-hacks__item"><input type="checkbox" data-hack="3"><span><strong>Hack 4 — Overload the constructor:</strong> Add a constructor that accepts a 9-character <code>String</code> and uses it as the starting board.</span></label>
  <label class="ttt-hacks__item"><input type="checkbox" data-hack="4"><span><strong>Hack 5 — Game IDs:</strong> Finish the <code>gameId</code> hack from Step 3, then add a static method <code>mostRecentGameId()</code> that returns the highest id assigned so far.</span></label>
</div>

<style>
  .ttt-hacks { max-width: 700px; margin: 20px auto; }
  .ttt-hacks__progress { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
  .ttt-hacks__progress-bar { flex: 1; height: 8px; border-radius: 999px; background: var(--panel-mid); overflow: hidden; }
  .ttt-hacks__progress-fill { height: 100%; width: 0%; background: var(--pref-accent-color); transition: width 0.3s ease; }
  #ttt-hacks-count { font-size: 13px; color: var(--text-muted); white-space: nowrap; }
  .ttt-hacks__item { display: flex; align-items: flex-start; gap: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid var(--ui-border); border-radius: 8px; background: var(--pref-bg-color); cursor: pointer; transition: border-color 0.2s ease, background 0.2s ease; }
  .ttt-hacks__item:hover { border-color: var(--pref-accent-color); }
  .ttt-hacks__item input { margin-top: 3px; accent-color: var(--pref-accent-color); cursor: pointer; }
  .ttt-hacks__item span { color: var(--pref-text-color); line-height: 1.5; font-size: 14px; }
  .ttt-hacks__item:has(input:checked) { opacity: 0.6; }
  .ttt-hacks__item:has(input:checked) span { text-decoration: line-through; }
</style>

<script>
(function () {
  var KEY = 'ttt-lesson-hacks';
  var box = document.getElementById('ttt-hacks');
  var checks = box.querySelectorAll('input[type=checkbox]');
  var fill = document.getElementById('ttt-hacks-fill');
  var count = document.getElementById('ttt-hacks-count');

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
