<template>
  <div class="guess-number-widget">
    <h2 class="widget-title">Tebak Angka 1-10</h2>
    <div class="game">
      <div class="player">
        <h3>Player</h3>
        <input type="number" v-model.number="guess" placeholder="Tebak angka" :disabled="isGameOver">
        <button @click="checkGuess" :disabled="isGameOver">Tebak</button>
      </div>
      <div class="computer">
        <h3>Komputer</h3>
        <p v-if="isGameOver">Angka yang harus ditebak:</p>
        <h4 v-if="isGameOver" class="secret-number">{{ secretNumber }}</h4>
        <p v-if="isGameOver" class="game-result">{{ gameResult }}</p>
      </div>
    </div>
    <div class="result" v-if="isGameOver">
      <button @click="resetGame">Main Lagi</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      secretNumber: null,
      guess: null,
      isGameOver: false,
      gameResult: ''
    };
  },
  methods: {
    checkGuess() {
      if (!this.guess) {
        alert("Silakan masukkan angka tebakan!");
        return;
      }

      if (this.guess === this.secretNumber) {
        this.gameResult = "Selamat! Anda berhasil menebak angka dengan benar.";
      } else if (this.guess < this.secretNumber) {
        this.gameResult = "Angka terlalu kecil! Coba lagi.";
      } else {
        this.gameResult = "Angka terlalu besar! Coba lagi.";
      }

      this.isGameOver = true;
    },
    resetGame() {
      this.secretNumber = null;
      this.guess = null;
      this.isGameOver = false;
      this.gameResult = '';
      this.generateSecretNumber();
    },
    generateSecretNumber() {
      this.secretNumber = Math.floor(Math.random() * 10) + 1;
    }
  },
  mounted() {
    this.generateSecretNumber();
  }
};
</script>

<style scoped>
.guess-number-widget {
  border: 2px solid #3498db;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f0f6fc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.widget-title {
  margin-top: 0;
  color: #3498db;
  font-size: 24px;
  font-weight: bold;
  text-transform: uppercase;
}

.game {
  display: flex;
  justify-content: space-around;
  margin: 50px 0;
}

.player,
.computer {
  flex-basis: 30%;
}

input[type="number"] {
  padding: 10px;
  font-size: 16px;
  width: 100px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  margin: 5px;
  padding: 10px 20px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.player button:disabled {
  background-color: #9e9e9e;
  cursor: not-allowed;
}

.computer .secret-number {
  font-size: 40px;
  color: #ff5722;
  margin: 0;
}

.computer .game-result {
  margin-top: 10px;
  color: #666;
}

.result {
  margin-top: 30px;
}

.result button {
  padding: 10px 20px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

@media only screen and (max-width: 600px) {
  .guess-number-widget {
    padding: 10px;
  }

  .widget-title {
    font-size: 20px;
  }

  .game {
    flex-direction: column;
  }

  .player,
  .computer {
    flex-basis: auto;
  }

  input[type="number"] {
    width: 80px;
    font-size: 14px;
  }

  button {
    padding: 8px 16px;
    font-size: 14px;
  }

  .result button {
    padding: 8px 16px;
    font-size: 14px;
  }
}
</style>
