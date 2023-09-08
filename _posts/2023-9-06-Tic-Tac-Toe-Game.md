---
comments: True
layout: post
title: Tic Tac Toe Game
description: creation of a tic tac toe game
type: hacks
courses: {'csp': {'week': 3}}
---

<style>
    /* Add your CSS styles for the Tic Tac Toe game here */
    .container {
        text-align: center;
    }
    .cell {
        width: 100px;
        height: 100px;
        display: inline-block;
        font-size: 36px;
        text-align: center;
        line-height: 100px;
        border: 1px solid #ccc;
        cursor: pointer;
    }

    #gameover {
        display: none;
        font-size: 24px;
    }
</style>

<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <h1 class="fs-4">Tic Tac Toe</h1>
    </header>
    <div id="board">
        <!-- The game board will be created here -->
    </div>
    <div id="gameover">
        <p id="gameover_message"></p>
        <button id="new_game" onclick="resetGame()">New Game</button>
    </div>
</div>

<script>
    // JavaScript code for the Tic Tac Toe game
    const board = document.getElementById("board");
    const gameoverMessage = document.getElementById("gameover_message");

    let currentPlayer = "X";
    let boardState = ["", "", "", "", "", "", "", "", ""];
    let gameActive = true;

    // Create the Tic Tac Toe grid
    for (let i = 0; i < 3; i++) {
        const row = document.createElement("div");

        for (let j = 0; j < 3; j++) {
            const cell = document.createElement("div");
            cell.classList.add("cell");
            cell.addEventListener("click", () => handleMove(cell, i * 3 + j));
            row.appendChild(cell);
        }

        board.appendChild(row);
    }

    // Function to handle a player's move
    function handleMove(cell, index) {
        if (boardState[index] === "" && gameActive) {
            cell.textContent = currentPlayer;
            boardState[index] = currentPlayer;

            if (checkWin()) {
                gameActive = false;
                gameoverMessage.textContent = `${currentPlayer} wins!`;
                document.getElementById("new_game").style.display = "block";
            } else if (!boardState.includes("")) {
                gameActive = false;
                gameoverMessage.textContent = "It's a draw!";
                document.getElementById("new_game").style.display = "block";
            } else {
                currentPlayer = currentPlayer === "X" ? "O" : "X";
            }
        }
    }

    // Function to check if a player has won
    function checkWin() {
        const winCombinations = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
            [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
            [0, 4, 8], [2, 4, 6] // Diagonals
        ];

        for (const combination of winCombinations) {
            const [a, b, c] = combination;
            if (boardState[a] && boardState[a] === boardState[b] && boardState[a] === boardState[c]) {
                return true;
            }
        }

        return false;
    }

    // Function to reset the game
    function resetGame() {
        currentPlayer = "X";
        boardState = ["", "", "", "", "", "", "", "", ""];
        gameActive = true;
        gameoverMessage.textContent = "";
        document.getElementById("new_game").style.display = "none";

        // Clear the board
        const cells = document.querySelectorAll(".cell");
        cells.forEach(cell => cell.textContent = "");
    }
</script>
