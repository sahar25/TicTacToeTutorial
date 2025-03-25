# Tic-Tac-Toe C++ Game Tutorial

## 1. Basic Concepts You Need to Know

Before writing the Tic-Tac-Toe game in C++, it’s important to understand some basic concepts of Object-Oriented Programming (OOP) that we will use in the program:

- **Classes and Objects**: A class is like a blueprint that defines the properties (variables) and behaviors (methods) of an object. An object is an instance of a class.
- **Encapsulation**: This refers to bundling the data (variables) and methods (functions) that operate on the data into a single unit or class. In C++, access specifiers like `public` and `private` control what is visible to the outside.
- **Constructors**: A constructor is a special method that gets called when an object is created. It is often used to initialize variables.
- **Member Functions**: These are functions that are defined inside a class and operate on the class’s variables.

---

## 2. Class Template, Variables, and Methods You Need to Have and Why

To build our Tic-Tac-Toe game in C++, we need to design a class that represents the game board and implements the game logic.

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using namespace std;
```

### Class Definition Template:

```cpp
class TicTacToe {
    char board[3][3];       // The 3x3 game board
    char currentPlayer;     // Tracks the current player ('X' or 'O')
public:
    TicTacToe();             // Constructor to initialize the game
    void displayBoard();     // Displays the current state of the game board
    void playerMove();       // Handles the player's move
    void computerMove();     // Handles the computer's move
    bool checkWin();         // Checks if a player has won the game
    bool isFull();           // Checks if the board is full (draw)
    void switchPlayer();     // Switches between players ('X' and 'O')
    char getCurrentPlayer(); // Get current player
};
```

## 3. `Constructor` Example

The constructor initializes the game by setting up the empty board and randomly deciding which player goes first.

```cpp
TicTacToe::TicTacToe() {
    // Initialize the board with empty spaces
    for (int i = 0; i < 3; ++i)
        for (int j = 0; j < 3; ++j)
            board[i][j] = ' ';

    // Randomly choose the first player
    srand(time(0));  // Seed the random number generator
    currentPlayer = (rand() % 2 == 0) ? 'X' : 'O';

    cout << "Player '" << currentPlayer << "' goes first!" << endl;
}
```

## 4. Example of a `Class` Used in `main`

```cpp
class Player {
    string name;
    int score;
public:
    Player(string playerName) {
        name = playerName;
        score = 0;
    }
    void increaseScore() {
        score++;
    }
    string getName() {
        return name;
    }
    int getScore() {
        return score;
    }
};
```
```cpp
int main() {
    // Create a TicTacToe game instance
    TicTacToe game;

    // Create a Player instance
    Player player1("Alice");
    cout << "Welcome, " << player1.getName() << "!\n";

    // Example gameplay loop (simplified)
    game.displayBoard();
    while (!game.checkWin() && !game.isFull()) {
        if (game.getCurrentPlayer() == 'X') {
            game.playerMove();
        } else {
            game.computerMove();
        }
        game.displayBoard();
         if (!game.checkWin()) {
            game.switchPlayer();
        }
    }

    if (game.checkWin()) {
        cout << "Player '" << game.getCurrentPlayer() << "' wins!\n";
        player1.increaseScore();
    } else {
        cout << "It's a draw!\n";
    }

    cout << player1.getName() << "'s final score: " << player1.getScore() << endl;
    return 0;
}
```


This file provides a comprehensive step-by-step tutorial that covers:

1. Basic concepts needed for the Tic-Tac-Toe game.
2. The class template with variables and methods, and why they are needed.
3. An example of how to define the constructor.
4. A small example of a different class (`Player`) and how to create an instance and use its methods and variables in `main()`.

