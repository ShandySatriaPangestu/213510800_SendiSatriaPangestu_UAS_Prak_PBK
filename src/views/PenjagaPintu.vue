<template>
    <div class="door-guard-game">
      <h2 class="game-title">Penjaga Pintu</h2>
      <p class="game-description">
        Pilihlah satu pintu dan temukan hadiah mobil yang tersembunyi di balik pintu tersebut. Berhati-hatilah, ada kambing yang tersembunyi di pintu lainnya!
      </p>
      <div class="game">
        <div class="door" v-for="(door, index) in doors" :key="index">
          <button @click="openDoor(door, index)" :disabled="isGameOver || door.isOpened">
            <img :src="door.isOpened ? door.image : require('@/assets/pintu.png')" :alt="door.isOpened ? door.prize : 'Pilih'">
          </button>
        </div>
      </div>
      <div class="result" v-if="isGameOver">
        <p v-if="isWin" class="result-text">Anda menang! Hadiahnya: {{ prize }}</p>
        <p v-else class="result-text">Anda kalah! Coba lagi.</p>
        <button @click="resetGame" class="play-again-btn">Main Lagi</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        doors: [],
        selectedDoorIndex: null,
        isGameOver: false,
        isWin: false,
        prize: ''
      };
    },
    created() {
      this.startGame();
    },
    methods: {
      startGame() {
        const initialDoors = [
          { prize: 'Kambing', isOpened: false, image: require('@/assets/kambing.png') },
          { prize: 'Kambing', isOpened: false, image: require('@/assets/kambing.png') },
          { prize: 'Mobil', isOpened: false, image: require('@/assets/mobil.png') }
        ];
        this.doors = this.shuffleArray([...initialDoors]);
      },
      openDoor(door, index) {
        if (this.isGameOver || door.isOpened) {
          return;
        }
  
        this.selectedDoorIndex = index;
        door.isOpened = true;
  
        if (door.prize === 'Mobil') {
          this.isWin = true;
          this.prize = 'Mobil';
        } else {
          this.isWin = false;
          this.prize = 'Kambing';
        }
  
        this.isGameOver = true;
      },
      resetGame() {
        const initialDoors = [
          { prize: 'Kambing', isOpened: false, image: require('@/assets/kambing.png') },
          { prize: 'Kambing', isOpened: false, image: require('@/assets/kambing.png') },
          { prize: 'Mobil', isOpened: false, image: require('@/assets/mobil.png') }
        ];
        this.doors = this.shuffleArray([...initialDoors]);
        this.selectedDoorIndex = null;
        this.isGameOver = false;
        this.isWin = false;
        this.prize = '';
      },
      shuffleArray(array) {
        for (let i = array.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [array[i], array[j]] = [array[j], array[i]];
        }
        return array;
      }
    }
  };
  </script>
  
  <style scoped>
  .door-guard-game {
    text-align: center;
    background-color: #f0f6fc;
    padding: 20px;
    border: 2px solid #3498db;
    border-radius: 8px;
  }
  
  .game-title {
    color: #3498db;
    font-size: 24px;
    margin-bottom: 10px;
  }
  
  .game-description {
    color: #333;
    font-size: 16px;
    margin-bottom: 20px;
  }
  
  .game {
    display: flex;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .door {
    margin: 0 10px;
  }
  
  button {
    margin: 5px;
    padding: 0;
    background-color: transparent;
    border: none;
    cursor: pointer;
    transition: opacity 0.3s ease;
  }
  
  button:disabled {
    cursor: not-allowed;
    opacity: 0.5;
  }
  
  .result {
    margin-top: 30px;
  }
  
  .result button {
    background-color: #f44336;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .result button:hover {
    background-color: #d32f2f;
  }
  
  .result-text {
    margin-bottom: 10px;
    font-weight: bold;
    font-size: 20px;
  }
  
  .play-again-btn {
    background-color: #3498db;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .play-again-btn:hover {
    background-color: #2979b8;
  }
  
  img {
    width: 100px;
    height: 100px;
  }
  </style>
  