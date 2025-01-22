# Recursion: N Queens Lab

## Numbrix Lab

**Robert Glen Martin**  
School for the Talented and Gifted  

Based on puzzles by  
**Marilyn vos Savan**  
*(Parade Magazine’s “Ask Marilyn”)*  

[Parade Numbrix Website](http://www.parade.com/numbrix)

---

### Description
In this lab, you will write a program that solves Numbrix puzzles. Numbrix puzzles were invented by Marilyn vos Savan, the author of the “Ask Marilyn” column in Parade Magazine. These puzzles consist of a grid with numbers in some of the cells.  

The example puzzle provided for this assignment is shown below:  

| 49 | -  | 51 | -  | 63 | -  | 69 | -  | 71 |
|----|----|----|----|----|----|----|----|----|
| -  | -  | -  | -  | -  | -  | -  | -  | -  |
| 47 | -  | -  | -  | -  | -  | -  | -  | 77 |
| -  | -  | -  | -  | -  | -  | -  | -  | -  |
| 45 | -  | -  | -  | -  | -  | -  | -  | 81 |
| -  | -  | -  | -  | -  | -  | -  | -  | -  |
| 43 | -  | -  | -  | -  | -  | -  | -  | 19 |
| -  | -  | -  | -  | -  | -  | -  | -  | -  |
| 41 | -  | 37 | -  | 9  | -  | 13 | -  | 15 |

A solved Numbrix puzzle contains all the numbers from 1 to `rows x cols` (e.g., 9 x 9 = 81) filled in, where:

1. The original numbers remain unchanged.
2. Consecutive numbers are adjacent either vertically or horizontally.

The solution to the example puzzle is:

| 49 | 50 | 51 | 62 | 63 | 68 | 69 | 70 | 71 |
|----|----|----|----|----|----|----|----|----|
| 48 | 53 | 52 | 61 | 64 | 67 | 74 | 73 | 72 |
| 47 | 54 | 59 | 60 | 65 | 66 | 75 | 76 | 77 |
| 46 | 55 | 58 | 27 | 26 | 25 | 24 | 79 | 78 |
| 45 | 56 | 57 | 28 | 5  | 4  | 23 | 80 | 81 |
| 44 | 31 | 30 | 29 | 6  | 3  | 22 | 21 | 20 |
| 43 | 32 | 33 | 34 | 7  | 2  | 1  | 18 | 19 |
| 42 | 39 | 38 | 35 | 8  | 11 | 12 | 17 | 16 |
| 41 | 40 | 37 | 36 | 9  | 10 | 13 | 14 | 15 |

---

### Lab Overview
You will use a **recursive depth-first search with pruning** to solve the puzzle.

---

### Steps to Complete the Lab

#### Part 1: Understanding Recursive Solving
1. **Base Cases:**
   - Check if row (`r`) or column (`c`) is outside the grid.
   - Verify the placement of a number based on grid rules and pruning.
2. **Recursive Calls:**
   - Attempt to place the next number in adjacent cells.

#### Part 2: Writing the Code
1. **Complete the `Numbrix` Constructor:**
   - Read input from a file.
   - Initialize the `grid` and `used` arrays.

2. **Implement the `toString` Method:**
   - Convert the `grid` to a string in row-major order.
   - Replace `0`s with `-` and format the output with tabs and newlines.

3. **Complete the `solve` Method:**
   - Start solving by placing `1` in every possible cell.
   - Use the `recursiveSolve` method to explore solutions.

4. **Write the `recursiveSolve` Method:**
   - Implement base cases to handle pruning and successful placement.
   - Print the solution when the puzzle is solved.

---

### Testing
- Verify the `toString` method produces correctly formatted grids.
- Ensure the program finds all solutions for puzzles with multiple valid outcomes.

---

© 2011 Robert Glen Martin  
*All rights reserved.*
