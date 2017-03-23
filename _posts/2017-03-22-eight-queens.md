---
layout: post
title: Eight Queens
tags: algorithm lynda
---

To any developer, **Eight Queens** cannot be more familiar.

<blockquote>
	The eight queens puzzle is the problem of placing eight chess queens on an 8×8 chessboard so that no two queens threaten each other.
</blockquote> 

[Lynda](https://www.lynda.com) has all kinds of code clinic videos to explain algorithm problems in various languages. Today I watched one of the eight queens solutions on Lynda by [Patrick Royal](https://www.lynda.com/Patrick-Royal/2069120-1.html). Now let me jot down the solution ideas.

<p>***********************</p>
Squares on a chessboard are stored as an arraylist of points. 
<code>
	(0,0),(0,1),(0,2) ... (8,7), (8,8)
</code>

Once a queen is placed on the chessboard, the corresponding row, column, and diagonals then cannot hold another queen. Therefore, those squares/points together with the square that's taken by a queen will be *removed* from that chessboard. The rest points will be available and valid for the next queen. The program ends when the number of queens to be put on the chessboard is reduced from 8 to 0.

A method called placeQueens carries out the main function **placing a queen** and **removing points after this placement**. The latter is supported by the method addQueen, which finds valid points and generate a *new* chessboard.

<p>***********************</p>

References:
1. https://en.wikipedia.org/wiki/Eight_queens_puzzle
2. https://www.lynda.com/Java-tutorials/Code-Clinic-Java/162454-2.html