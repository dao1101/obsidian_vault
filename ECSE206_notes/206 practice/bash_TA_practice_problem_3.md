<!-- Written by TA Shiyan -->
# Q1. The Maze

The goal of this question is to write a Bash script that solves an 8x8 maze. The question will be split up into a few parts that test various aspects of Bash. Note that the full script should be in one file.

## a)

Write a Bash script that takes as input a text file that represents a maze-like structure. The maze starts at the **top-left** and ends at the **bottom-right**.

The characters `R`, `L`, `U`, and `D` represent the cardinal directions, while `e` and `E` represent the **entry** and **exit**, respectively.

An example maze is shown below. You can either test with this one or use AI to generate your own maze. (Make sure that you prompt it to output a maze that is possible.)

**Note:** Please do not use AI to write your full script.

You can figure out how you want to store it. My recommendation would be to use 8 separate strings to store the 8 rows. If you want to be more efficient, you can use an associative array (outside of the scope of this course).

```text
e R R R R R R D
D D L R U L D D
L U R D L R U D
R L U R D L R D
D R L U R D L D
U L R D U R L D
R D U L R U D D
U R L U D R L E
```

## b)

A cell that is denoted `R` means that you must move to the right, and the same applies for the other directions. The only difference is the entry and exit cells.

In the entry cell, you can move **right**, **down**, or **diagonally down-right**. Exactly one of these paths should lead you to the exit. (You should tell the AI this if you're generating your own maze.)

Using your representation of the maze, continue your script to try each of these three paths to determine which one leads to the exit. (Note that if your first path works, you don't necessarily need to try the others. You can use a true/false variable to keep track of this.) Make use of temporary variables 'i' and 'j' to indicate your position in the maze. The start is at i=j=0.

Note that there are two ways that a path can be incorrect.

1. It goes outside of the maze. (The down path in the example maze)
2. It gets you stuck in an endless loop. (The diagonally down-right path in the example maze.)

The first is easy to check, but the second is harder. Since the maze is small (8x8), we can use a string as indicator of positions that we've been to before, "0 11 17" for example. At each step of your traversal, you can iterate through this string to see if your current position has already been visited. Use this and your 'i' and 'j' variables for this. (Note that this pretty inefficient, if you are using associative arrays there is a much cleaner way to do this.) Make sure to reset this string if you're starting a different path from the entry cell.

You do not have to do this, but it might be helpful to write a helper function find() that takes as input a row string and column number and returns you the character at that position in the maze.

## c).

The script should output the exact sequence of moves that are needed to solve the maze. In the example given, the script should output "RIGHT RIGHT RIGHT RIGHT RIGHT RIGHT RIGHT DOWN DOWN DOWN DOWN DOWN DOWN DOWN". Note that by output we just mean printing to terminal.
