---
title: Rock Paper Scissors Lesson — Selection & Iteration
description: Build Rock Paper Scissors in Java and practice if/else selection, boolean logic, String comparison, and loops.
layout: post
toc: True
codemirror: True
courses: {'csa': {'week': 2}}
permalink: /csa/rock-paper-scissors-lesson
---

## Rock Paper Scissors: Selection & Iteration

Rock Paper Scissors is a perfect vehicle for the two control structures that run every program: **selection** (deciding what to do) and **iteration** (deciding how many times to do it).

By the end of this lesson you'll have practiced:
- **Selection & Booleans** — `if` / `else if` / `else` chains, boolean expressions
- **`String` comparison** — why `==` doesn't do what you'd expect on `String`s
- **Loops & Iteration** — `while` loops that repeat until a condition changes
- **Nested Loops** — loops inside loops, and how they affect run time

Every code box below is **live** — click **Run ▶** to execute it for real, edit it, and run it again.

---

## Step 1: Who Wins? — Selection

Given two choices, `"rock"`, `"paper"`, or `"scissors"`, an `if` / `else if` chain decides the outcome. Each branch is a **boolean expression** — a condition that's either `true` or `false`.

```java
String player = "rock";
String computer = "scissors";

if (player.equals(computer)) {
    System.out.println("Tie!");
} else if (player.equals("rock") && computer.equals("scissors")) {
    System.out.println("Player wins!");
} else if (player.equals("paper") && computer.equals("rock")) {
    System.out.println("Player wins!");
} else if (player.equals("scissors") && computer.equals("paper")) {
    System.out.println("Player wins!");
} else {
    System.out.println("Computer wins!");
}
```

<div class="rpn-popcorn">
    <div class="rpn-popcorn__header">
        <h3>Popcorn Hack: == vs .equals()</h3>
        <p>In Java, why does this code use <code>player.equals(computer)</code> instead of <code>player == computer</code>?</p>
    </div>
    <div class="rpn-popcorn__body">
        <div class="rpn-popcorn__options" id="rps-ph1-options">
            <button onclick="checkRpsPH1(0)" class="rpn-popcorn__option">A) <code>.equals()</code> is just a style preference — both always work the same</button>
            <button onclick="checkRpsPH1(1)" class="rpn-popcorn__option">B) <code>==</code> compares object references, so two equal-looking Strings can compare unequal</button>
            <button onclick="checkRpsPH1(2)" class="rpn-popcorn__option">C) <code>==</code> only works on numbers, never on objects</button>
            <button onclick="checkRpsPH1(3)" class="rpn-popcorn__option">D) <code>.equals()</code> is faster than <code>==</code></button>
        </div>
        <div id="rps-ph1-feedback" class="rpn-popcorn__feedback"></div>
    </div>
</div>

<script>
function checkRpsPH1(sel) {
    const btns = document.querySelectorAll('#rps-ph1-options .rpn-popcorn__option');
    const fb = document.getElementById('rps-ph1-feedback');
    btns.forEach(b => b.className = 'rpn-popcorn__option');
    if (sel === 1) {
        btns[1].classList.add('rpn-popcorn__option--correct');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--correct';
        fb.innerHTML = '<strong style="color:#2ecc71;">Correct!</strong> <code>==</code> on <code>String</code> objects checks whether both variables point to the <em>same object in memory</em>, not whether their characters match. Two Strings built differently (e.g. one from user input, one literal) can hold identical text but fail <code>==</code>. Always use <code>.equals()</code> to compare String contents.';
    } else {
        btns[sel].classList.add('rpn-popcorn__option--incorrect');
        fb.className = 'rpn-popcorn__feedback rpn-popcorn__feedback--incorrect';
        fb.innerHTML = '<strong style="color:#e74c3c;">Not quite.</strong> The real reason is that <code>==</code> compares <em>references</em> (memory addresses) for objects like <code>String</code>, while <code>.equals()</code> compares the actual characters. This is a classic AP CSA exam trap!';
    }
}
</script>

{% capture challenge_selection %}
Finish the <code>else if</code> chain so all nine combinations of <code>player</code>/<code>computer</code> are handled correctly. Change the values of <code>player</code> and <code>computer</code> and re-run to test different matchups.
{% endcapture %}

{% capture code_selection %}
String player = "paper";
String computer = "rock";

if (player.equals(computer)) {
    System.out.println("Tie!");
} else if (player.equals("rock") && computer.equals("scissors")) {
    System.out.println("Player wins!");
} else if (player.equals("paper") && computer.equals("rock")) {
    System.out.println("Player wins!");
}
// TODO: add the missing branch for scissors beats paper
// TODO: add the final `else` for every case where the computer wins
{% endcapture %}

{% include runners/code.html
   runner_id="rps_selection"
   language="java"
   challenge=challenge_selection
   code=code_selection
   height="420px"
%}

---

## Step 2: Best of Three — Loops & Iteration

A single round isn't a game. A `while` loop lets us **iterate** — repeat the round logic until someone has won twice.

```java
int playerWins = 0;
int computerWins = 0;
int round = 0;

while (playerWins < 2 && computerWins < 2) {
    round++;
    // (Pretend this picks random choices and compares them)
    boolean playerWonThisRound = (round % 2 == 0); // stand-in logic
    if (playerWonThisRound) {
        playerWins++;
    } else {
        computerWins++;
    }
    System.out.println("Round " + round + " — Player: " + playerWins + ", Computer: " + computerWins);
}

System.out.println(playerWins > computerWins ? "Player wins the match!" : "Computer wins the match!");
```

Notice the **loop condition**, `playerWins < 2 && computerWins < 2` — it's a boolean expression, just like Step 1's `if` conditions. The loop keeps iterating as long as it stays `true`.

{% capture challenge_loop %}
Change the loop so it plays <strong>best of five</strong> instead of best of three (first to 3 wins). Then add a <code>round</code> limit so the loop also stops after 5 rounds even if nobody has 3 wins yet (a tie-breaker).
{% endcapture %}

{% capture code_loop %}
int playerWins = 0;
int computerWins = 0;
int round = 0;

while (playerWins < 2 && computerWins < 2) {
    round++;
    boolean playerWonThisRound = (round % 2 == 0); // stand-in logic
    if (playerWonThisRound) {
        playerWins++;
    } else {
        computerWins++;
    }
    System.out.println("Round " + round + " — Player: " + playerWins + ", Computer: " + computerWins);
}

// TODO: change the win target from 2 to 3 (best of five)
// TODO: also stop the loop after round 5, even without a winner
System.out.println(playerWins > computerWins ? "Player wins the match!" : "Computer wins the match!");
{% endcapture %}

{% include runners/code.html
   runner_id="rps_loop"
   language="java"
   challenge=challenge_loop
   code=code_loop
   height="440px"
%}

---

## Step 3: A Tournament — Nested Loops & Run Time

To simulate several players each playing several rounds, put a loop **inside** a loop. The outer loop walks through players; the inner loop walks through that player's rounds.

```java
String[] players = {"Ada", "Grace", "Alan"};
int roundsPerPlayer = 3;

for (int p = 0; p < players.length; p++) {
    System.out.println(players[p] + "'s rounds:");
    for (int r = 1; r <= roundsPerPlayer; r++) {
        System.out.println("  Round " + r + " played");
    }
}
```

**Run time:** the outer loop runs `players.length` times, and for *each* of those, the inner loop runs `roundsPerPlayer` times. The total number of iterations is `players.length * roundsPerPlayer` — this is why nested loops are often described as **O(n × m)**: work grows with the product of the two loop sizes, not just their sum.

{% capture challenge_nested %}
Add a fourth player, <code>"Katherine"</code>, to the <code>players</code> array. Then change <code>roundsPerPlayer</code> to <code>5</code> and predict how many total lines of "Round played" output you'll see before running it — then check your prediction.
{% endcapture %}

{% capture code_nested %}
String[] players = {"Ada", "Grace", "Alan"};
int roundsPerPlayer = 3;

for (int p = 0; p < players.length; p++) {
    System.out.println(players[p] + "'s rounds:");
    for (int r = 1; r <= roundsPerPlayer; r++) {
        System.out.println("  Round " + r + " played");
    }
}
{% endcapture %}

{% include runners/code.html
   runner_id="rps_nested"
   language="java"
   challenge=challenge_nested
   code=code_nested
   height="380px"
%}

---

## Show Solution: Tracking a Win Streak

<div class="rpn-reveal">
    <div class="rpn-reveal__header">
        <h3>How would you track a win streak?</h3>
        <p>Using the Step 2 loop, how would you count the player's <em>longest consecutive</em> win streak, not just their total wins? Think about it, then reveal one approach.</p>
    </div>
    <div class="rpn-reveal__body">
        <button class="rpn-reveal__toggle-btn" onclick="var a=document.getElementById('rps-reveal-answer'); a.style.display = a.style.display === 'block' ? 'none' : 'block';">Show / Hide Answer</button>
        <div class="rpn-reveal__answer" id="rps-reveal-answer">
            <h4>Two Counters: Current Streak and Best Streak</h4>
            <div class="rpn-reveal__code-block"><pre>int currentStreak = 0;
int bestStreak = 0;

while (/* game not over */ true) {
    if (playerWonThisRound) {
        currentStreak++;
        bestStreak = Math.max(bestStreak, currentStreak);
    } else {
        currentStreak = 0; // streak resets on any loss
    }
}</pre></div>
            <p class="key-detail">The key idea: <code>currentStreak</code> resets to <code>0</code> the moment the condition breaks (a loss), while <code>bestStreak</code> only ever grows — it remembers the high point across the whole loop.</p>
        </div>
    </div>
</div>

---

## Hacks

Extend the Rock Paper Scissors logic above. Check off each one as you finish it — your progress is saved in this browser.

<div class="rps-hacks" id="rps-hacks">
  <div class="rps-hacks__progress">
    <div class="rps-hacks__progress-bar"><div class="rps-hacks__progress-fill" id="rps-hacks-fill"></div></div>
    <span id="rps-hacks-count">0 / 5 complete</span>
  </div>
  <label class="rps-hacks__item"><input type="checkbox" data-hack="0"><span><strong>Hack 1 — Full selection:</strong> Write the complete <code>if</code> / <code>else if</code> chain for all 9 rock/paper/scissors combinations without skipping any.</span></label>
  <label class="rps-hacks__item"><input type="checkbox" data-hack="1"><span><strong>Hack 2 — Best of five:</strong> Rewrite the Step 2 loop to require 3 wins out of 5 rounds.</span></label>
  <label class="rps-hacks__item"><input type="checkbox" data-hack="2"><span><strong>Hack 3 — Nested tournament table:</strong> Extend Step 3 to also print whether each round was a win, loss, or tie for that player.</span></label>
  <label class="rps-hacks__item"><input type="checkbox" data-hack="3"><span><strong>Hack 4 — Win streak:</strong> Implement the streak-tracking logic from the reveal above and test it against a sequence of wins/losses.</span></label>
  <label class="rps-hacks__item"><input type="checkbox" data-hack="4"><span><strong>Hack 5 — Add Lizard/Spock:</strong> Extend the selection logic to support two new choices, <code>"lizard"</code> and <code>"spock"</code>, and all their matchups.</span></label>
</div>

<style>
  .rps-hacks { max-width: 700px; margin: 20px auto; }
  .rps-hacks__progress { display: flex; align-items: center; gap: 12px; margin-bottom: 16px; }
  .rps-hacks__progress-bar { flex: 1; height: 8px; border-radius: 999px; background: var(--panel-mid); overflow: hidden; }
  .rps-hacks__progress-fill { height: 100%; width: 0%; background: var(--pref-accent-color); transition: width 0.3s ease; }
  #rps-hacks-count { font-size: 13px; color: var(--text-muted); white-space: nowrap; }
  .rps-hacks__item { display: flex; align-items: flex-start; gap: 10px; padding: 12px 14px; margin-bottom: 8px; border: 1px solid var(--ui-border); border-radius: 8px; background: var(--pref-bg-color); cursor: pointer; transition: border-color 0.2s ease, background 0.2s ease; }
  .rps-hacks__item:hover { border-color: var(--pref-accent-color); }
  .rps-hacks__item input { margin-top: 3px; accent-color: var(--pref-accent-color); cursor: pointer; }
  .rps-hacks__item span { color: var(--pref-text-color); line-height: 1.5; font-size: 14px; }
  .rps-hacks__item:has(input:checked) { opacity: 0.6; }
  .rps-hacks__item:has(input:checked) span { text-decoration: line-through; }
</style>

<script>
(function () {
  var KEY = 'rps-lesson-hacks';
  var box = document.getElementById('rps-hacks');
  var checks = box.querySelectorAll('input[type=checkbox]');
  var fill = document.getElementById('rps-hacks-fill');
  var count = document.getElementById('rps-hacks-count');

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
