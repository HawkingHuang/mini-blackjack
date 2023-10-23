<!-- Port: 8085 -->
<template>
  <transition-group name="whole" tag="div" appear>
    <div class="home" :key="id">
      <PlayerASection
        :isHiddenA="isHiddenA"
        @A-clicked="handleAClick"
        :total="totalA"
        :playerCardsA="playerCardsA"
        :hideAFirstCard="hideAFirstCard"
        ref="playerA"
        :gamestarted="gamestarted"
      />
      <div class="setting">
        <button class="setting-btn" @click="start">Start</button>
        <button class="setting-btn" @click="end">End</button>
        <button class="setting-btn" @click="reset">Reset</button>
      </div>
      <transition name="fade">
        <div class="result" v-show="showEnd">
          <h3>{{ result }}</h3>
          <button @click="closeResult" class="close-button">
            <ion-icon name="close-outline" class="button-x"></ion-icon>
          </button>
        </div>
      </transition>
      <PlayerBSection
        :isHiddenB="isHiddenB"
        @B-clicked="handleBClick"
        :total="totalB"
        :playerCardsB="playerCardsB"
        :hideBFirstCard="hideBFirstCard"
        ref="playerB"
        :gamestarted="gamestarted"
      />
    </div>
  </transition-group>
</template>

<script>
import PlayerASection from "./components/PlayerASection.vue";
import PlayerBSection from "./components/PlayerBSection.vue";
export default {
  name: "App",
  components: {
    PlayerASection,
    PlayerBSection,
  },
  data() {
    return {
      id: "blackjack",
      cardsPool: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11],
      isHiddenA: true,
      isHiddenB: true,
      showEnd: false,
      playerCardsA: [],
      playerCardsB: [],
      totalA: 0,
      totalB: 0,
      result: "",
      hideAFirstCard: false,
      hideBFirstCard: false,
      gamestarted: false,
    };
  },
  methods: {
    start() {
      this.gamestarted = true;
      this.isHiddenA = false;
      this.isHiddenB = false;
    },
    handleAClick() {
      const randomIndex = Math.floor(Math.random() * this.cardsPool.length);
      const cardValue = this.cardsPool.splice(randomIndex, 1)[0];
      this.totalA += cardValue;

      this.playerCardsA.push(cardValue);
    },
    handleBClick() {
      const randomIndex = Math.floor(Math.random() * this.cardsPool.length);
      const cardValue = this.cardsPool.splice(randomIndex, 1)[0];
      this.totalB += cardValue;

      this.playerCardsB.push(cardValue);
    },
    end() {
      if (this.totalA > this.totalB && this.totalA <= 21 && this.totalB <= 21) {
        this.result = `A(${this.totalA}):B(${this.totalB}), Player A wins!`;
      } else if (
        this.totalA < this.totalB &&
        this.totalA <= 21 &&
        this.totalB <= 21
      ) {
        this.result = `A(${this.totalA}):B(${this.totalB}), Player B wins!`;
      } else if (this.totalA > 21 && this.totalB <= 21) {
        this.result = `A(${this.totalA}):B(${this.totalB}), Player B wins!`;
      } else if (this.totalB > 21 && this.totalA <= 21) {
        this.result = `A(${this.totalA}):B(${this.totalB}), Player A wins!`;
      } else {
        this.result = `A(${this.totalA}):B(${this.totalB}), It's a draw!`;
      }
      this.showEnd = true;
      this.$refs.playerA.updateHide();
      this.$refs.playerB.updateHide();
    },
    closeResult() {
      this.showEnd = false;
    },
    reset() {
      this.cardsPool = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];
      this.isHiddenA = true;
      this.isHiddenB = true;
      this.playerCardsA = [];
      this.playerCardsB = [];
      this.totalA = 0;
      this.totalB = 0;
      this.result = "";
      this.hideAFirstCard = false;
      this.hideBFirstCard = false;
      this.$refs.playerA.updateHide();
      this.$refs.playerB.updateHide();
      this.gamestarted = false;
    },
  },
};
</script>

<style>
* {
  font-family: Pixelify Sans;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
  background: #e9ecef;
}

.home {
  position: relative;
}

.setting {
  max-width: 150rem;
  margin: 1rem auto;
  display: flex;
  justify-content: center;
  font-size: 3rem;
  gap: 1rem;
  position: relative;
}

.setting-btn {
  width: 10%;
  height: 30%;
  color: white;
  background-color: black;
  font-size: 2rem;
  border-radius: 5px;
  cursor: pointer;
}

.result {
  width: 50rem;
  height: 10rem;
  border: 1px solid black;
  border-radius: 8px;
  margin: 0 auto;
  position: absolute;
  z-index: 1;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: black;
  text-align: center;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3rem;
}

.first-card {
  cursor: pointer;
}

.result button.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  width: 2rem;
  height: 2rem;
  border-radius: 6px;
  cursor: pointer;
  background: white;
}

ion-icon {
  --ionicon-stroke-width: 80px;
}

.whole-enter-from,
.whole-leave-to {
  opacity: 0;
}

.whole-enter-active,
.whole-leave-active {
  transition: opacity 5s ease;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
