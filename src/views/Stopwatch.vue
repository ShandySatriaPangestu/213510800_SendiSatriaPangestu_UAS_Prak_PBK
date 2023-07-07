<template>
  <div class="stopwatch-widget">
    <h2>Stopwatch</h2>
    <div class="timer">
      <div class="timer-display">
        <span>{{ minutes }}</span>:<span>{{ seconds }}</span>:<span>{{ milliseconds }}</span>
      </div>
    </div>
    <div class="controls">
      <button @click="toggleStopwatch" :class="{ active: isRunning }">{{ isRunning ? 'Pause' : 'Start' }}</button>
      <button @click="resetStopwatch">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
    };
  },
  computed: {
    minutes() {
      return Math.floor(this.elapsedTime / 60000).toString().padStart(2, '0');
    },
    seconds() {
      return Math.floor((this.elapsedTime % 60000) / 1000).toString().padStart(2, '0');
    },
    milliseconds() {
      return (this.elapsedTime % 1000).toString().padStart(3, '0');
    },
  },
  methods: {
    toggleStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      } else {
        this.isRunning = true;
        this.startTime = Date.now() - this.elapsedTime;

        this.timerInterval = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      clearInterval(this.timerInterval);
      this.elapsedTime = 0;
    },
  },
};
</script>

<style scoped>
.stopwatch-widget {
  border: 2px solid #333;
  padding: 20px;
  margin-bottom: 20px;
  text-align: center;
  background-color: #f5f5f5;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stopwatch-widget h2 {
  color: #333;
  font-size: 24px;
  margin-bottom: 10px;
}

.timer {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.timer-display {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: #333;
}

.timer-display span {
  padding: 0 5px;
}

.controls {
  display: flex;
  justify-content: center;
}

.stopwatch-widget button {
  margin: 0 5px;
  padding: 10px 20px;
  background-color: #2980b9;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.stopwatch-widget button:hover {
  background-color: #2980b9;
}

.stopwatch-widget button:active {
  background-color: #398439;
}

.stopwatch-widget button.active {
  background-color: #f44336;
}

.stopwatch-widget button:disabled {
  background-color: #ccc;
  color: #999;
  cursor: not-allowed;
}
</style>
