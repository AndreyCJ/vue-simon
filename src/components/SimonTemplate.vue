<template>
  <div class="simon">
    <SimonWheel
      @boxClick="boxClick"
      :isBoxOneActive="isBoxOneActive"
      :isBoxTwoActive="isBoxTwoActive"
      :isBoxThreeActive="isBoxThreeActive"
      :isBoxFourActive="isBoxFourActive"
      :userTurn="userTurn"
    />
    <SimonControls
      @changeGameState="changeGameState"
      :childDiff.sync="difficulty"
      :score="score"
      :state="state"
    />
    <SimonMessage 
      :message="message"
    />
  </div>
</template>

<script>
import SimonWheel from '@/components/SimonWheel.vue';
import SimonControls from '@/components/SimonControls';
import SimonMessage from '@/components/SimonMessage';

import a1 from '@/assets/sounds/1.mp3';
import a2 from '@/assets/sounds/2.mp3';
import a3 from '@/assets/sounds/3.mp3';
import a4 from '@/assets/sounds/4.mp3';

const audio1 = new Audio(a1);
const audio2 = new Audio(a2);
const audio3 = new Audio(a3);
const audio4 = new Audio(a4);

export default {
  data() {
    return {
      userTurn: false,
      difficulty: 'easy',
      score: 0,
      state: 'off',
      pattern: [],
      index: 0,
      isBoxOneActive: false,
      isBoxTwoActive: false,
      isBoxThreeActive: false,
      isBoxFourActive: false,
      message: '',
      isDisabled: false,
    }
  },
  components: {
    SimonWheel,
    SimonControls,
    SimonMessage
  },
  methods: {
    changeGameState() {
      if (this.state === 'off') {
        this.message = '';
        this.state = 'on';
        this.isPlaying = true;
        this.computerTurn();
      } else {
        this.resetGame();
      }
    },
    computerTurn() {
      this.index = 0;
      const randomNum = this.getRandomNum();
      this.pattern.push(randomNum);
      this.lightUp();
    },
    getDelay(diff) {
      let delay = 1500;
      switch (diff){
        case 'easy':
          delay = 1500;
          break;
        case 'medium':
          delay = 1000;
          break;
        case 'hard':
          delay = 400;
          break;
      }
      return delay;
    },
    allowInput() {
      this.userTurn = true;
    },
    lightUp() {
      let delay = this.getDelay(this.difficulty);
      let i = 0;
      let timer = setInterval(() => {
        if (i >= this.pattern.length) {
          clearInterval(timer);
        } else {
          this.clickEffect(this.pattern[i])
          i++;
        }
      }, delay);
      
      this.userTurn = true;
    },
    boxClick(boxNum) {
      if (this.state === 'off') {
        return;
      }
      if (this.userTurn) {
        this.clickEffect(boxNum);

        let isCorrect = this.isInputCorrect(boxNum);
        if (!isCorrect) {
          this.gameOver();
        } else {
          if (this.index === this.pattern.length - 1) {
            this.score++;
            setTimeout(() => {
              this.userTurn = false;
              this.computerTurn();
            }, 1000);
          } else {
            this.index++;
          }
        }
      } else {
        return;
      }
    },
    clickEffect(boxNum) {
      switch (boxNum) {
        case 1:
          this.isBoxOneActive = true;
          audio1.play();
          setTimeout(() => {
            this.isBoxOneActive = false;
            audio1.pause();
            audio1.currentTime = 0;
          }, 300);
          break;
        case 2:
          this.isBoxTwoActive = true;
          audio2.play();
          setTimeout(() => {
            this.isBoxTwoActive = false;
            audio2.pause();
            audio2.currentTime = 0;
          }, 300);
          break;
        case 3:
          this.isBoxThreeActive = true;
          audio3.play();
          setTimeout(() => {
            this.isBoxThreeActive = false;
            audio3.pause();
            audio3.currentTime = 0;
          }, 300);
          break;
        case 4:
          this.isBoxFourActive = true;
          audio4.play();
          setTimeout(() => {
            this.isBoxFourActive = false;
            audio4.pause();
            audio4.currentTime = 0;
          }, 300);
          break;
      }
    },
    getRandomNum() {
      return Math.floor(Math.random() * 4 + 1);
    },
    isInputCorrect(boxNum) {
      return (this.pattern[this.index] === boxNum);
    },
    gameOver(){ 
      this.message = `Игра закончена со счетом - ${this.score}` 
      this.resetGame();
    },
    resetGame() {
      this.userTurn = false;
      this.state = 'off';
      this.score = 0;
      this.isPlaying = false;
      this.pattern = [];
      this.index = 0;
    },
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
  font-weight: 900;
  font-family: sans-serif;
  color: #323232;
}

a {
  text-decoration: none;
  color: #3F72AF;
}

.--hidden {
  visibility: hidden;
}

.simon {
  width: 100%;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.flex--center {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>