# Tic Tac Toe Game

A fun and interactive Tic Tac Toe game built using **HTML**, **CSS**, and **JavaScript**. This game supports two players (Player X and Player O) and includes features like a reset button and winner detection.

---

## Table of Contents

- [HTML Structure](#html-structure)
- [CSS Styling](#css-styling)
- [JavaScript Logic](#javascript-logic)
  - [Selecting DOM Elements](#selecting-dom-elements)
  - [Player Turns](#player-turns)
  - [Winning Logic](#winning-logic)
  - [Resetting the Game](#resetting-the-game)

---

## HTML Structure

The HTML structure defines the layout of the game, including the game board and control buttons.

### Why this structure?
- **Semantic Elements**: Using `<main>` and `<button>` ensures the structure is clear and accessible.
- **Dynamic Elements**: Buttons are used for each game cell, enabling interaction.
- **Message Container**: Displays the winner and options for starting a new game.

### Code

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tic-Tac-Toe Game</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="msg-container hide">
      <p id="msg">Winner</p>
      <button id="new-btn">New Game</button>
    </div>
    <main>
      <h1>Tic Tac Toe</h1>
      <div class="container">
        <div class="game">
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
        </div>
      </div>
      <button id="reset-btn">Reset Game</button>
    </main>
    <script src="tic_tac.js"></script>
  </body>
</html>
```

---

## CSS Styling

CSS is used to style the game layout, making it visually appealing and responsive.

### Why this styling?
- **Flexbox**: Ensures that elements are centered and responsive.
- **Box Styling**: Each game cell has a shadow and rounded corners for better aesthetics.
- **Colors**: Distinct background and font colors for contrast and clarity.

### Code

```css
* {
    margin: 0;
    padding: 0;
  }
  
  body {
    background-color: #548687;
    text-align: center;
  }
  
  .container {
    height: 70vh;
    display: flex;
  
    justify-content: center;
    align-items: center;
  }
  
  .game {
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1.5vmin;
  }
  
  .box {
    height: 18vmin;
    width: 18vmin;
    border-radius: 1rem;
    border: none;
    box-shadow: 0 0 1rem rgba(0, 0, 0, 0.3);
    font-size: 8vmin;
    color: #b0413e;
    background-color: #ffffc7;
  }
  
  #reset-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color: #fff;
    border-radius: 1rem;
    border: none;
  }
  
  #new-btn {
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color: #fff;
    border-radius: 1rem;
    border: none;
  }
  
  #msg {
    color: #ffffc7;
    font-size: 5vmin;
  }
  
  .msg-container {
    height: 100vmin;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 4rem;
  }
  
  .hide {
    display: none;
  }
  
```

---

## JavaScript Logic

JavaScript handles the game logic, including player turns, winner detection, and resetting the game.

### Selecting DOM Elements
- **Why?** To interact with the HTML elements and update the game dynamically.

```javascript
let boxes = document.querySelectorAll(".box");
let resetBtn = document.querySelector("#reset-btn");
let newGameBtn = document.querySelector("#new-btn");
let msgContainer = document.querySelector(".msg-container");
let msg = document.querySelector("#msg");
```

### Player Turns
- **Why?** Alternates turns between Player X and Player O.

```javascript
let turnO = true; // Player X, player O

boxes.forEach((box) => {
    box.addEventListener("click", () => {
        if (turnO) {
            box.innerText = "O";
            turnO = false;
        } else {
            box.innerText = "X";
            turnO = true;
        }
        box.disabled = true;
        checkWinner();
    });
});
```

### Winning Logic
- **Why?** Checks all winning patterns to determine the winner.

```javascript
let winPatterns = [
    [0, 1, 2],
    [0, 3, 6],
    [0, 4, 8],
    [1, 4, 7],
    [2, 5, 8],
    [2, 4, 6],
    [3, 4, 5],
    [6, 7, 8],
];

const checkWinner = () => {
    for (let pattern of winPatterns) {
        let pos1val = boxes[pattern[0]].innerText;
        let pos2val = boxes[pattern[1]].innerText;
        let pos3val = boxes[pattern[2]].innerText;

        if (pos1val !== "" && pos2val !== "" && pos3val !== "") {
            if (pos1val === pos2val && pos2val === pos3val) {
                showWinner(pos1val);
            }
        }
    }
};

const showWinner = (winner) => {
    msg.innerText = `Congratulations, Winner is ${winner}`;
    msgContainer.classList.remove("hide");
    disableBoxes();
};
```

### Resetting the Game
- **Why?** Clears the board and starts a new game.

```javascript
const disableBoxes = () => {
    for (let box of boxes) {
        box.disabled = true;
    }
};

const enableBoxes = () => {
    for (let box of boxes) {
        box.disabled = false;
        box.innerText = "";
    }
};

const restGame = () => {
    turnO = true;
    enableBoxes();
    msgContainer.classList.add("hide");
};

resetBtn.addEventListener("click", restGame);
newGameBtn.addEventListener("click", restGame);
```
