<template>
    <div class="tic-tac-toe-widget">
      <h2>Tic Tac Toe</h2>
      <div class="board">
        <div v-for="(cell, index) in board" :key="index" @click="handleClick(index)">
          {{ cell }}
        </div>
      </div>
      <button @click="resetGame">Reset</button>
      <p>{{ status }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        board: ['', '', '', '', '', '', '', '', ''],
        currentPlayer: 'X',
        isGameEnded: false,
      };
    },
    computed: {
      status() {
        if (this.isGameEnded) {
          return 'Game Over!';
        }
        return `Player ${this.currentPlayer}'s turn`;
      },
    },
    methods: {
      handleClick(index) {
        if (!this.isGameEnded && this.board[index] === '') {
          this.board[index] = this.currentPlayer;
          this.checkWinner();
          this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
        }
      },
      checkWinner() {
        const winningCombinations = [
          [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
          [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
          [0, 4, 8], [2, 4, 6], // Diagonals
        ];
  
        for (const combination of winningCombinations) {
          const [a, b, c] = combination;
          if (this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]) {
            this.isGameEnded = true;
            return;
          }
        }
      },
      resetGame() {
        this.board = ['', '', '', '', '', '', '', '', ''];
        this.currentPlayer = 'X';
        this.isGameEnded = false;
      },
    },
  };
  </script>
  
  <style scoped>
  .tic-tac-toe-widget {
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    max-width: 300px;
    margin: 0 auto;
    text-align: center;
    background-color: #f9f9f9;
    background-image: linear-gradient(to bottom right, #f9f9f9, #eaeaea);
  }
  
  .board {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
    margin-bottom: 10px;
  }
  
  .board div {
    border: 1px solid #ccc;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 24px;
    background-color: #f2f2f2;
    transition: background-color 0.3s ease-in-out;
  }
  
  .board div:hover {
    background-color: #e0e0e0;
  }
  
  button {
    margin-top: 10px;
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    background-color: #4caf50;
    color: #fff;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
  