# Recursion 
## Numbrix Lab

*Originally created by:*
**Robert Glen Martin**  
School for the Talented and Gifted  

Based on puzzles by  
**Marilyn vos Savan**  
*(Parade Magazine’s “Ask Marilyn”)*  

[Parade Numbrix Website](http://www.parade.com/numbrix)

---

### Description
In this lab you will write a program that solves Numbrix puzzles.  Numbrix puzzles were invented by Marilyn vos Savan, the author of the “Ask Marilyn” column in Parade Magazine.  Numbrix puzzles can be found at http://www.parade.com/numbrix and various other online sites.
Numbrix puzzles consist of a grid with numbers in some of the cells.    

The puzzle provided for this assignment is shown below:  

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

A solved Numbrix puzzle contains all the numbers from 1 to rows x cols (9 x 9 = 81 in this example) filled in.  The original numbers must be unchanged, and consecutive numbers must be next to each other either vertically or horizontally.

The solution to the puzzle is:

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

### Why Recursive Depth-First Search?
The most straightforward way to attack this problem is to try all the possible positions for the remaining numbers and see which ones solve the puzzle.  This can be accomplished with a recursive depth-first search.
However, in this puzzle, there are 81 - 16 = 65 numbers to place.  Therefore, there are 65! (65 factorial) possible placements for the remaining 65 numbers, only one of which is correct.  65! is a pretty large number.  It’s even greater than 1090, a one followed by 90 zeros.
How long would it take to try 1090 different possible solutions?  Let’s assume that we have a smoking fast program running on a really fast computer that can compute a quadrillion (1,000,000,000,000,000 = 1015) possible number placements every second.  Then it would take more than 1090 / 1015 = 1075 seconds for our program to complete.  But how long is 1075 seconds?
1075/ 60 / 60 / 24 / 365 is more than 1067 years.  Since the AP Exam is in May, we need a faster algorithm.

The code you are going to write solves a Numbrix using a recursive depth-first search with pruning.  “Pruning” means that your code will check each number before it is placed into the puzzle and if the number doesn’t “fit”, it will not explore that branch of the search any further.  Using this strategy, a puzzle can be solved in seconds!
Our search for a solution begins with the solve method which iterates through each element (row r and column c) of grid and attempts to solve the puzzle by starting with a 1 in that location.  It does this by calling recursiveSolve(r, c, 1) to attempt a solution beginning with a 1 at row r and column c.
recursiveSolve is the method that performs the recursive depth-first search.  After placing a number n, it recursively attempts to place the number n+1 in the location above, below, left, and right of the location where it placed n.  It continues to attempt placing subsequent numbers until the last number is successfully placed.
Obviously, the program is unlikely to be successful on every placement attempt.  When a number n can’t be successfully placed at row r and column c, the recursiveSolve method returns and lets the method invocation that called it attempt a different placement.  recursiveSolve returns when:
 
* either r or c is outside of grid.  This is base case one.
* the current location contains 0 (empty), but the number to be placed was used elsewhere in the original puzzle.  This is base case two and the first “pruning” situation.
* the current location contains a number, but it’s not equal to the number to be placed.  This is base case three and the second “pruning” situation.
* the puzzle is solved.  In this case we print the solution and return to look for more solutions.  This is base case four.
* the four recursion calls have been completed.


---

### Implementation Steps

#### Provided Classes
1. **`NumbrixMain`**  
   - This is the application class.  
   - It has been fully written for you. **Do not make changes or additions!!!**  
2. **`Numbrix`**  
   - This class represents the puzzle.  
   - You will write code for this class.
   - This class already contains two instance variables: **`grid`** and **`used`**.  **`grid`** will contain the puzzle and **`used`** will indicate if a number was used in the original puzzle.  These are the only instance variables needed.  **Do not add any additional instance variables.**

---

### Part 1: Constructor
Complete the constructor for the **`Numbrix`** class.  

1. Create a `Scanner` to read from the input file named in `filename`. Use `new Scanner(new File(fileName))` to instantiate your `Scanner`.
2. Read the number of rows and columns from the file. These are the first and second numbers in the data file respectively.
3. Instantiate the `grid` 2D array to have the input number of rows and columns.
4. Instantiate the `used` array to have `rows * cols + 1` elements. The extra element allows you to use the numbers in the puzzle as indices. Otherwise you would need to subtract 1 to prevent an `ArrayOutOfBoundsException`. The element at index 0 is ignored. 
5. Input the puzzle numbers and use them to fill in `grid` and `used`.  `used[num]` should be `true` if `num` is in the original input puzzle.  It should be `false` otherwise.

---

### Part 2: `toString` Method
Complete the `toString` method to return a string representation of the grid.  

- **Format:**
  - The data must be in row-major order
  - 0s must be indicated by dash (minus sign,`-`) characters
  - There must be **one tab character** after each number or dash
  - There must be **one new line character** after each row
  - There must be **no** extraneous spaces of other characters

Test your program and correct any errors.  It should produce the following output (tab width may vary):

**Example Output:**
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

### Part 3: `solve` Method
Complete the `solve` method. This method should attempt to solve the puzzle by starting with a `1` in each available `grid` element.  For each element of `grid`, `solve` should call `recursiveSolve(r, c, 1)` where `r` and `c` are the row and column of the `grid` location in which to attempt to place the `1`.

Test your new `solve` method  by adding temporary code to `recursiveSolve` that prints `r`, `c`, and `n`.  Make sure that `solve` calls `recursiveSolve` for **all** possible `r` and `c`.  Also make sure that `n` is always `1`.  

When you are satisfied that solve is working correctly, comment out the temporary code from `recursiveSolve`.

### Part 4: `recursiveSolve` Method
This is the recursive method that performs the depth-first search for solutions.  **Follow the instructions carefully to complete this method.**  Complete it as follows:
1) Make sure that `r` and `c` specify an element inside the `grid`.  If `r` is an invalid row index, or `c` is an invalid column index, then `return`.  This is base case one.
2) Create and initialize a `boolean` variable named `zero`.  This variable needs to be `true` if and only if `grid[r][c]` contains a 0.  **Do this with <u>one</u> statement of the following form:***  `boolean zero = ... ;`
3) The next two base cases (d) and (e) consist of situations where it does not make sense to place `n` in `grid[r][c]`.  They constitute the pruning discussed earlier.
4) If `zero` is `true` but `n` **is** in the original puzzle, then `n` can’t be placed in `grid[r][c]` because it is already used elsewhere.  In this case, your method should `return`.  Utilize `used` to determine if `n` is in the original puzzle.  This is base case two.
5) If `zero` is `false` and `grid[r][c]` contains a number other than `n`, then your method should `return`.  This is base case three.
6) At this point, it makes sense to store `n` in `grid[r][c]`.  Go ahead and do that.
7) Now check to see if the puzzle is solved.  See if `n` equals the product of the number of rows and columns in `grid`.  If so, you should print this with `System.out.println(this);` which in turn calls `toString` implicity.  This is the fourth base case.  Don’t return yet though because we need to remove the number at `grid[r][c]` and look for other solutions.
8) If the puzzle isn’t solved then make four recursive calls.  These four calls should specify the element that is up, down, left, and right of the current element.  The 3rd parameter should be `n + 1`.
9) Finally, if `zero` is `true`, then set `grid[r][c]` back to `0`.

Test your program and correct any errors.  It should produce the following output (tab width may vary):
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

One final note about Numbrix puzzles and this program:  A well-constructed Numbrix puzzle will only have one solution.  However, in the case where there is more than one solution, your program should find and print all of them.
