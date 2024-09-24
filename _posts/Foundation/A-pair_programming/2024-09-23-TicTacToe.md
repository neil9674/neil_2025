---
layout: post
title: Tic Tac Toe Coding Project - Neil C
type: issues
description: This is a Tic Tac Toe Coding Project where I collaborated with my partner to help me create it. We both added our own unique spin to this classic game.
comments: true
---

<style>
.game-board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    gap: 5px;
    justify-content: center;
    margin-top: 50px;
}
.cell {
    width: 100px;
    height: 100px;
    background-color: #f2f2f2;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2em;
    cursor: pointer;
    border: 2px solid #333;
}
.message {
    text-align: center;
    font-size: 1.5em;
    margin-top: 20px;
}
.color-selection {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-bottom: 20px;
}
select {
    font-size: 1em;
    padding: 5px;
}
</style>

<div class="color-selection">
    <div>
        <label for="x-color">Select X Color: </label>
        <select id="x-color">
            <option value="red">Red</option>
            <option value="blue">Blue</option>
            <option value="yellow">Yellow</option>
            <option value="green">Green</option>
        </select>
    </div>
    <div>
        <label for="o-color">Select O Color: </label>
        <select id="o-color">
            <option value="red">Red</option>
            <option value="blue">Blue</option>
            <option value="yellow">Yellow</option>
            <option value="green">Green</option>
        </select>
    </div>
</div>

<div class="game-board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
</div>

<div class="message"></div>

<script>
const cells = document.querySelectorAll('.cell');
const message = document.querySelector('.message');
let currentPlayer = 'X';
let board = Array(9).fill(null);
let isGameActive = true;

const xColorSelect = document.getElementById('x-color');
const oColorSelect = document.getElementById('o-color');
let xColor = xColorSelect.value;
let oColor = oColorSelect.value;

xColorSelect.addEventListener('change', () => {
    xColor = xColorSelect.value;
});

oColorSelect.addEventListener('change', () => {
    oColor = oColorSelect.value;
});

const winningConditions = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
];

function checkWinner() {
    for (const condition of winningConditions) {
        const [a, b, c] = condition;
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
            isGameActive = false;
            return board[a];
        }
    }
    if (!board.includes(null)) return 'Draw';
    return null;
}

function handleClick(e) {
    const index = e.target.dataset.index;
    if (!isGameActive || board[index]) return;

    board[index] = currentPlayer;
    e.target.textContent = currentPlayer;
    e.target.style.color = currentPlayer === 'X' ? xColor : oColor;

    const winner = checkWinner();
    if (winner) {
        message.textContent = winner === 'Draw' ? "It's a draw!" : `${winner} wins!`;
    } else {
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
}

cells.forEach(cell => cell.addEventListener('click', handleClick));
</script>
