---
title: Final Quiz — Units 1-4
description: A 25-question review covering everything from the Calculator, Rock Paper Scissors, Tic Tac Toe, and Data Collections lessons.
layout: post
courses: {'csa': {'week': 5}}
permalink: /csa/final-quiz
quiz:
  - q: "Unit 1 (Calculator) — What does the new Calculator(10, 4) call actually do?"
    choices:
      - "Instantiates a Calculator object and runs its constructor"
      - "Declares a variable named Calculator"
      - "Calls the add() method with 10 and 4"
      - "Imports the Calculator class"
    answer: 0
  - q: "Unit 1 (Calculator) — Why are firstNumber and secondNumber declared private?"
    choices:
      - "So other classes can access them directly"
      - "So they can only be accessed through the Calculator's own methods (encapsulation)"
      - "So only subclasses can access them"
      - "So they're shared across every Calculator object"
    answer: 1
  - q: "Unit 1 (Calculator) — What does power() use to compute an exponent?"
    choices:
      - "A manual loop multiplying firstNumber by itself"
      - "The ** operator"
      - "Math.pow(firstNumber, secondNumber)"
      - "Math.exp()"
    answer: 2
  - q: "Unit 1 (Calculator) — What is the return type of add(), subtract(), multiply(), and divide()?"
    choices:
      - "void"
      - "int"
      - "double"
      - "String"
    answer: 2
  - q: "Unit 1 (Calculator) — Why doesn't dividing by zero with double operands crash the program immediately?"
    choices:
      - "Java throws a compiler error before it runs"
      - "double division by zero returns Infinity or NaN instead of throwing"
      - "Java automatically substitutes 1 for zero"
      - "The program pauses and asks for new input"
    answer: 1
  - q: "Unit 1 (Calculator) — What does the % operator compute in the remainder() hack?"
    choices:
      - "A percentage of the total"
      - "The remainder left over after integer division"
      - "The square root"
      - "A random number between the two operands"
    answer: 1
  - q: "Unit 2 (Rock Paper Scissors) — What does player.equals(computer) actually check?"
    choices:
      - "Whether the two variables point to the same object in memory"
      - "Whether the character contents of the two Strings are the same"
      - "Whether both Strings have the same length only"
      - "Whether player was declared before computer"
    answer: 1
  - q: "Unit 2 (Rock Paper Scissors) — In the Step 1 if/else if chain, what happens if none of the win conditions match?"
    choices:
      - "The program throws an exception"
      - "Nothing happens, execution just continues"
      - "The final else branch runs, defaulting to Computer wins"
      - "Java picks a random branch to execute"
    answer: 2
  - q: "Unit 2 (Rock Paper Scissors) — What data type tracks whether the player won a given round?"
    choices:
      - "String"
      - "int"
      - "boolean"
      - "char"
    answer: 2
  - q: "Unit 2 (Rock Paper Scissors) — In Step 3, what determines the total number of loop iterations?"
    choices:
      - "players.length + roundsPerPlayer"
      - "players.length times roundsPerPlayer"
      - "Only roundsPerPlayer"
      - "Only players.length"
    answer: 1
  - q: "Unit 2 (Rock Paper Scissors) — Why does bestStreak only ever grow while currentStreak can reset to 0?"
    choices:
      - "bestStreak tracks the highest streak seen so far, while currentStreak tracks the streak in progress right now"
      - "They are actually the same variable with two names"
      - "currentStreak is a constant and cannot change"
      - "bestStreak resets every round automatically"
    answer: 0
  - q: "Unit 2 (Rock Paper Scissors) — What kind of loop repeats rounds until someone wins twice in Step 2?"
    choices:
      - "A for loop with a fixed count"
      - "A do-while loop"
      - "A while loop with a boolean condition"
      - "A nested for loop"
    answer: 2
  - q: "Unit 3 (Tic Tac Toe) — What data structure holds the 9 cells of the board?"
    choices:
      - "An ArrayList<Character>"
      - "A char[] array of length 9"
      - "A 2D int[][] array"
      - "A String with 9 characters"
    answer: 1
  - q: "Unit 3 (Tic Tac Toe) — What does markCell return if the requested index is already taken?"
    choices:
      - "It throws an exception"
      - "false"
      - "true"
      - "The board resets"
    answer: 1
  - q: "Unit 3 (Tic Tac Toe) — What is boardsCreated an example of?"
    choices:
      - "An instance variable, unique to each board"
      - "A local variable inside the constructor"
      - "A class (static) variable, shared by every TicTacToeBoard instance"
      - "A method parameter"
    answer: 2
  - q: "Unit 3 (Tic Tac Toe) — Where does gameId get its value from in the Step 3 hack?"
    choices:
      - "A random number generator"
      - "The shared boardsCreated counter at the moment that board was constructed"
      - "The board's array index"
      - "The system clock"
    answer: 1
  - q: "Unit 3 (Tic Tac Toe) — What does the print() method's if (i % 3 == 2) condition control?"
    choices:
      - "Which player's turn it is"
      - "When to print a newline, so the board displays as 3 rows of 3"
      - "Whether a cell is empty"
      - "How many boards have been created"
    answer: 1
  - q: "Unit 3 (Tic Tac Toe) — Why is getBoardsCreated() called on the class name instead of a specific board?"
    choices:
      - "Because it's a static method operating on class-level shared data, not tied to one object"
      - "Because it's a private method"
      - "Because TicTacToeBoard has no constructor"
      - "Because it modifies the cells array"
    answer: 0
  - q: "Unit 4 (Data Collections) — Why does the code cast total to (double) before dividing by cookieSales.length?"
    choices:
      - "To avoid a compiler error"
      - "Because int divided by int would truncate the decimal part of the average"
      - "To make the array sortable"
      - "It's unnecessary, just a style choice"
    answer: 1
  - q: "Unit 4 (Data Collections) — What happens when you call orders.get(0) on an ArrayList<Integer>?"
    choices:
      - "It throws an exception since Integer isn't a primitive"
      - "Java auto-unboxes the Integer back into an int"
      - "It returns the ArrayList's size"
      - "It removes the first element"
    answer: 1
  - q: "Unit 4 (Data Collections) — In the 2D array step, what does the outer loop index (week) represent?"
    choices:
      - "A single day's sales"
      - "One week's row in the monthlySales grid"
      - "The total number of days"
      - "The busiest day found so far"
    answer: 1
  - q: "Unit 4 (Data Collections) — What must be true about cookieSales before Arrays.binarySearch gives a reliable result?"
    choices:
      - "It must contain only even numbers"
      - "It must be sorted"
      - "It must have exactly 7 elements"
      - "It must already contain the value being searched for"
    answer: 1
  - q: "Unit 4 (Data Collections) — In recursiveSum, what does arr[index] + recursiveSum(arr, index + 1) do?"
    choices:
      - "Adds the current element to the sum of everything after it"
      - "Multiplies every element together"
      - "Removes the current element from the array"
      - "Sorts the array before summing"
    answer: 0
  - q: "Unit 4 (Data Collections) — Which method call performs the sort in the searching and sorting step?"
    choices:
      - "cookieSales.sort()"
      - "Arrays.sort(cookieSales)"
      - "Collections.sort(cookieSales)"
      - "cookieSales.orderBy()"
    answer: 1
  - q: "Across units — Rock Paper Scissors uses an if condition to decide a winner, and Tic Tac Toe's markCell uses the same kind of check before making a move. What's that shared concept called?"
    choices:
      - "A while loop"
      - "Selection: a boolean condition checked before an action proceeds"
      - "A static variable"
      - "A recursive call"
    answer: 1
---

## Final Quiz

You've opened all four units — nice work. This quiz mixes questions from Calculator, Rock Paper Scissors, Tic Tac Toe, and Data Collections to check how everything fits together.
