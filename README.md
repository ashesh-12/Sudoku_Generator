# Sudoku Puzzle Generator 

This project is about creating a Sudoku puzzle step by step.  
I started from generating a **fully solved Sudoku board**, then turned it into a playable puzzle depending on the chosen difficulty level.

---

## 1. Solver Functions
To make everything work, I first needed a way to **solve Sudoku**.  

- **`find_empty(board)`**  
  I wrote this function to search for the next empty cell (a `0`).  
  If no empty cells are left, that means the Sudoku is solved.

- **`is_valid(board, num, row, col)`**  
  I did this to check if a number can be placed in a specific spot.  
  It checks three rules:
  1. The number should not already be in the same row.  
  2. The number should not already be in the same column.  
  3. The number should not already be in the 3x3 box.  

- **`solver(board)`**  
  Here I used **backtracking**.  
  I pick an empty cell, shuffle numbers 1–9 randomly (so that solutions look different each time), and try them one by one.  
  If a number is valid, I place it and keep solving.  
  If I get stuck, I backtrack (reset cell to 0) and try another number.  

- **`sudoku_solved_board(board)`**  
  This function just runs the solver on an empty board and gives me a full valid Sudoku solution.

---

## 2. Generator Helper Functions
Once I had a solved board, I needed to **turn it into a puzzle** by removing numbers.

- **`get_difficulty()`**  
  I ask the user whether they want Easy, Medium, or Hard.  
  Based on that, I decide how many clues to leave:
  - Easy → 36 clues  
  - Medium → 30 clues  
  - Hard → 24 clues  

- **`pick_random_filled_cell(board)`**  
  I did this to randomly pick a cell that already has a number (so I can try removing it).

- **`remove_cell(board, row, col)`**  
  This temporarily removes a number (turns it into 0).  

- **`undo_removal(board, row, col, value)`**  
  If the removal causes multiple solutions, I undo it and put the number back.

---

## 3. Unique Solution Checker
When I remove a number, I need to make sure the puzzle still has **only one valid solution**.  
So I built a solution counter:

- **`count_solutions(board, limit=2)`**  
  This is a modified backtracking solver.  
  I count how many solutions exist.  
  If I find 2 or more, I stop early (no need to keep checking).

- **`has_unique_solution(board)`**  
  This just checks if exactly 1 solution exists.  
  I used this to guarantee uniqueness of the puzzle.

---

## 4. Puzzle Generator
- **`sudoku_generator(board)`**  
  Here I put everything together.  
  1. Start with a full solved board.  
  2. Calculate how many numbers need to be removed (based on difficulty).  
  3. Randomly remove cells one by one.  
  4. Each time, I check if the puzzle still has a unique solution.  
     - If yes → keep it removed.  
     - If no → undo the removal.  

In the end, I get a Sudoku puzzle that matches the chosen difficulty.

---

## 5. Main Execution
Finally, I tied it all together:  

1. I created an empty 9x9 board.  
2. I generated a full solved Sudoku using backtracking.  
3. I asked the user for difficulty (Easy/Medium/Hard).  
4. I used the generator to remove cells and create the puzzle.  
5. I printed the final Sudoku puzzle in a clean format.  

---
