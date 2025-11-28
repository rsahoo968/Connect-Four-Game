# Connect Four Java Game – Board Class

This project implements the core game logic for a Connect Four board in Java.  
The `Board` class manages player turns, placing moves, checking wins, updating the board, and reporting the game status.

The board is a 6-row by 7-column grid, and players take turns dropping pieces into columns until someone wins or the board is full.

---

## How the Game Works

- The board has **6 rows** and **7 columns**.
- Player **'X'** always goes first.
- Player **'O'** goes second.
- Players take turns placing a piece into a column.
- A piece always drops to the **lowest empty spot** in that column.
- A player wins by connecting **four pieces in a row**, either:
  - Vertically  
  - Horizontally  
  - Diagonally (both diagonal directions)
- If the board becomes full and no player wins, the game ends in a draw.

---

## Class Overview

### `Board()` Constructor
- Creates a new empty game board.
- Fills all spaces with the character `'0'`, representing an empty cell.
- Sets:
  - `firstPlayer = 'X'`
  - `secondPlayer = 'O'`
- Initializes a 6×7 grid stored as a 2D `char[][]` array.

---

## Methods

### `char currentPlayer()`
- Returns `'X'` or `'O'`, depending on whose turn it is.
- The turn is determined by counting how many pieces each player has placed.
- If both players have placed the same number of pieces, it is `'X'`'s turn.
- Otherwise, it is `'O'`'s turn.

---

### `boolean play(int column)`
Allows the current player to attempt a move.

**Rules for a valid move:**
1. The game must still be in progress.
2. The column must be between **1 and 7**.
3. The column must not be full.

**What happens when calling `play(column)`**:
- If the move is valid, the player’s piece is dropped into the correct row.
- The method returns `true`.
- If the move is invalid (column full or out of bounds), it returns `false`.
- If the game has already ended, the method throws a `RuntimeException`.

---

### `char gameStatus()`

Returns one of the following:

| Return Value | Meaning |
|--------------|---------|
| `'X'` | Player X has won |
| `'O'` | Player O has won |
| `'D'` | Game ended in a draw (board full, no winner) |
| `'U'` | Game is still ongoing |

The method checks for:
- Vertical 4-in-a-row
- Horizontal 4-in-a-row
- Down-right diagonal 4-in-a-row
- Up-right diagonal 4-in-a-row

If none of the conditions are met and the board is full, the game is a draw.

---

### `String toString()`
Creates a text version of the board.

Example output:

0 0 0 0 0 0 0
0 0 0 0 0 0 0
0 0 0 0 0 0 0
0 0 0 0 0 0 0
X 0 0 0 0 0 0
X O 0 0 0 0 0
1 2 3 4 5 6 7 


- Each row of the board is printed from top to bottom.
- `'0'` represents an empty cell.
- A line of column numbers is printed at the bottom for easy reference.

---

## How to Use This Class

Here is a simple example of how you might use the `Board` class in a program:

```java
public class Main {
    public static void main(String[] args) {
        Board board = new Board();

        board.play(1);  // X moves
        board.play(1);  // O moves
        board.play(2);  // X moves again

        System.out.println(board.toString());
        System.out.println("Status: " + board.gameStatus());
    }
}

