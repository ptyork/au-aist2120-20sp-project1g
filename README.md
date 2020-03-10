# Project 1g: Pown Chess

This is going to be a REALLY simple game of chess. Basically there are ONLY pawns. But the pawns are even more useless than they are in real chess, so we'll refer to them as "powns". Stay tuned for an explanation.

First and formost, your script, `pown-chess.py`, is "started" for you. The game "state" (i.e., the positions of each piece on the playing board) is represented by a dictionary named `game_board`. Both books give some examples of using dictionaries for managing board state, so might serve as good reference.

The game itself starts with the 6 x 6 board in the following state:
```
     A   B   C   D   E   F  
   +---+---+---+---+---+---+
1  | w | w | w | w | w | w |
   +---+---+---+---+---+---+
2  |   |   |   |   |   |   |
   +---+---+---+---+---+---+
3  |   |   |   |   |   |   |
   +---+---+---+---+---+---+
4  |   |   |   |   |   |   |
   +---+---+---+---+---+---+
5  |   |   |   |   |   |   |
   +---+---+---+---+---+---+
6  | b | b | b | b | b | b |
   +---+---+---+---+---+---+
```
Note that the above is ALSO an example of how you should display the game board whenever you want to show the board.

The only rules are as follows:

1. Play starts with "w" and then alternates one move at a time between "w" and "b".

2. Each move can ONLY go one square at a time and in one direction ("down" for "w" and "up" for "b").

3. If one player moves to a space occupied by another players piece, the other piece is "removed". For example, B4 is a "w" and B5 is a "b", then if the b player moves the piece at B5, "B5" becomes empty, "B4" becomes "b", and there will simply be one fewer "w" piece on the board.

4. Game is over when the "active" player can't move (either because they have no pieces remaining or all of their remaining pieces are at the far end of the board (row 1 for b or row 6 for w)). The player with most remaining pieces is the winner.

And believe it or not, that's it.

Gameplay is very basic. Here's a partial example. `[display_board]` is shown for brevity, but will display the current gameboard in a form similar to 6x6 grid shown above.
```
[display_board]
w move: B1
w moves from B1 to B2!
[display_board]
b move: F6
b moves from F6 to F5
[display_board]

... clipped for brevity ...

[display_board]
b move: C4
b moves from C4 to C3
b powns a w
[display_board]

... clipped for brevity ...

[display_board]
b move: F2
b moves from F2 to F1
There are no more moves for w
b has 3 pieces
w has 2 pieces
b wins!!
GAME OVER
```

## REQUIRED IMPLEMENTATION NOTES 

0. First and foremost, don't panic. Start small and build up. Initialize your `board`. Then implement and "play with" (i.e., test and retest and retest) `display_board()`, just to get it showing the current board state. Then implement the `moves_remaining()` function and play with it. ONLY THEN move on to writing any of the game play logic. Slow, steady and step-by-step is the way to conquer any "medium-sized" program. And there's plenty of partial credit to be had.

1. As noted, you MUST create a single `game_board` variable to represent your game board as a dictionary.

2. You MUST define and use a function called `display_board()` that iterates over the `game_board` variable and displays the game board as shown in the example above.

3. You MUST define and use a function called `moves_remaining(color)` that iterates over the `game_board` variable and RETURNS the count of pieces on the board that match the `color` parameter THAT CAN BE MOVED. In other words, at the beginning, calling `moves_remaining('w')` should return `6` since there are 6 w's on the board that can move "down" from 1 towards 6. However, if all remaining "w" pieces are in row 6, then the function should return 0.

4. When the player enters their "move" locations, you MUST implement basic error checking logic and enforce game rule #3. If the square doesn't exist OR if the square is empty OR if the square is occupied by the wrong color OR if the selected pieces cannot move because they are at the end of the board, print `INVALID MOVE` to the screen and `continue` to let the next player go (yep, you are to be MEAN to players who can't type or follow rules very well).

And a few hints:

5. Your main game play might work best as a `while True:` loop that will `break` only when somebody wins (i.e., a call to `moves_remaining()` returns 0)

6. The logic for `display_board()` may not be obvious because your "keys" will include letters and numbers, not just sequential numbers. Just to get your brain in the right general location, you might want to create a nested for loop to iterate over each of the board squares (row by row) in the right order:
```
        rows = ('1','2','3','4','5','6')
        cols = ('A','B','C','D','E','F')
        for row in rows:
            # Print row "header" (+---+---, etc.)
            rowstr = ''  # will be used to construct the string for the actual row
            for col in cols:
                # Draw and check each square.
                # '', 'w' or 'b' should be in game_board[col + row].
                # Concatenate the value to the rowstr, including
                # the spaces and "|" required for formatting.
            # Print rowstr
```

7. You MIGHT also want to define and use a `move(from)` function that you can call that better encapsulates the logic of moving a piece. If I were to do this, I would have this `move()` function return True or False depending on whether the move was allowed.

8. You MIGHT also want to define and use a `count_pieces(color)` function that returns the remaining number of pieces on the board for the given color (useful at the end).

When done, be sure to test the heck out of this and then submit the __project1 directory__ in Mimir.

## OPTIONAL CHALLENGES 

1. Show the current "score" in your `display_board` function centered above the board in the form `w: 6  b: 6` (good use for that recommended `count_pieces()` function).

2. In addition to 1, show a move counter above the board. For example `Move #7 -- w: 5  b:4`.

3. Be "nicer". Instead of skipping to the next player if there is an invalid move as described in implementation note #4 above, allow the player to keep trying to enter a valid move.
