
# TicTacToe3D Lab Tutorial

## Required Concepts

### Inheritance
Inheritance establishes an "is-a" relationship between classes, allowing us to create new classes from existing ones. In this lab:

- **Base Class**: The existing `TicTacToe` class.
- **Derived Class**: The `TicTacToe3D` class, which inherits properties and methods from `TicTacToe`.

### Access Specifiers
These determine the accessibility of class members in inheritance:

- **Private**: Accessible only in the base class.
- **Public**: Accessible everywhere.
- **Protected**: Accessible in the base class and derived classes.

### Syntax of Derived Class
```cpp
class DerivedClassName : accessSpecifier BaseClassName { 
    member list 
}; 
```
If no access specifier is provided, inheritance defaults to private.

## Additional Notes

- **Overriding**: Redefining a base class's virtual function in a derived class. This allows the derived class to provide specific behavior while keeping the same function signature.
- **Overloading**: Creating multiple functions with the same name but different parameters in the same scope (not used for inheritance but useful for varied inputs).
- **Constructor in Derived Class**: A derived class must call a constructor of the base class. If not explicitly called, the default constructor of the base class is invoked by default.
- **Virtual Functions**: A virtual function in a base class enables dynamic binding, allowing derived classes to override this function. When a function is virtual in the base class, it remains virtual in derived classes without needing the `virtual` keyword again.

---

## Base Class: TicTacToe

Before updating for inheritance, `TicTacToe` might have all members private. To prepare it as a base class:

1. Change `currentPlayer` and `filledCells` to **protected** for access in `TicTacToe3D`.
2. Mark key functions as **virtual** to allow overriding.

### Updated TicTacToe Class

```cpp
class TicTacToe {
    char board[3][3];       // 3x3 game board (unused in 3D but kept for compatibility)
protected:
    char currentPlayer;     // 'X' or 'O'
    int emptyCells;        // Count of empty cells, decrements to zero

public:
    TicTacToe();            // Constructor to initialize the game
    virtual void displayBoard(); // Display the board
    virtual void playerMove();   // Handle player's move
    virtual void computerMove(); // Handle computer's move
    virtual bool checkWin();     // Check if a player has won
    bool isFull();               // Check if the board is full (draw)
    virtual bool makeMove(int row, int col); // Attempt to make a move
    void switchPlayer();         // Switch turns between 'X' and 'O'
    char getCurrentPlayer();     // Getter for currentPlayer
};
```
## Derived Class: TicTacToe3D

`TicTacToe3D` extends `TicTacToe` and overrides several functions. It includes a 3D board (3x3x3) and adds a scoring system for the number of completed rows, columns, and diagonals.

```cpp
class TicTacToe3D : public TicTacToe {
    char board3D[3][3][3];    // 3x3x3 game board for 3D Tic-Tac-Toe
    int scoreX, scoreO;        // Scores for players X and O
    
    int calculateScore(int x, int y, int z); // Calculate score based on completed rows
public:
    TicTacToe3D();             // Constructor to initialize the 3D game
    void displayBoard() override;     // Display the 3D board with ASCII art
    void playerMove() override;       // Handle player's move with 3D input
    void computerMove() override;     // Handle computer's move with 3D input
    bool makeMove(int x, int y, int z); // Attempt to make a move in 3D space
    bool checkWin() override;         // Override to announce the winner at the end
};
```
### Calculating Score

In `TicTacToe3D`, the `calculateScore` function checks completed rows by analyzing each 3-in-a-row in the 3D board. It includes:

- **Rows on each layer**: Checks rows within a single layer.
- **Columns on each layer**: Checks columns within a layer.
- **Vertical columns**: Checks vertical 3-in-a-row sequences.
- **3D diagonals**: Checks diagonal sequences that span across the entire cube.

This approach ensures the scoring system accurately tracks all possible ways to complete a line in 3D Tic-Tac-Toe.
## Class Inheritance Example

This example demonstrates how a derived class can inherit and utilize a method from its base class.

### Base Class: `base`

The `base` class defines a method to count uppercase letters in a single string.

```cpp
// base class definition
class base {
public:
    // This function counts the number of uppercase letters in the input string "s"
    int countUpper(string s) {
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            if (isupper(s[i])) count++;
        }
        return count;
    }
};
```
- `countUpper(string s)`: This function iterates over each character in the string `s`, counting uppercase letters using `isupper()`.

---

## Derived Class: `derived`

The `derived` class inherits from `base` and overrides the `countUpper` function to work with an array of strings.

```cpp
// derived class (inherits from base class) definition
class derived : public base {
public:
    string s[3];
    
    // This function counts the number of uppercase letters in all strings in the array "s".
    // It calls the base class function to count uppercase letters in each individual string.
    int countUpper() {
        int count = 0;
        for (int i = 0; i < 3; i++) {
            count += base::countUpper(s[i]); // Call the base class function
        }
        return count;
    }
};
```
### String Array `s`

The derived class has an array of strings `s[3]`.

### `countUpper()` in Derived Class

This method iterates through each string in the array `s`, calling `base::countUpper(s[i])` to count uppercase letters in each string.

- **`base::countUpper(s[i])`**: This syntax explicitly calls the `countUpper` function from the `base` class on each string in the array `s`.

### Key Points

- **Using `base::`**: In the derived class, `base::countUpper(s[i])` allows access to the `countUpper` method from the `base` class.
- **Inheritance**: The derived class inherits functionality from `base` and extends it to work with multiple strings by calling the inherited method on each element of `s`.

