<template>
  <section class="section-player-a" :key="id">
    <div class="section-cards-a">
      <h1 :style="{ display: isHiddenA ? 'block' : 'none' }">Player A</h1>
      <div
        class="cards-pool-a"
        :style="{ display: isHiddenA ? 'none' : 'flex' }"
      >
        <div
          class="cards-a first-card"
          @click="hideACard"
          :style="{ opacity: hide ? 0 : 1 }"
        >
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[0] ? 1 : 0 }"
          >
            {{ playerCardsA[0] }}
          </div>
        </div>
        <div class="cards-a">
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[1] ? 1 : 0 }"
          >
            {{ playerCardsA[1] }}
          </div>
        </div>
        <div class="cards-a">
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[2] ? 1 : 0 }"
          >
            {{ playerCardsA[2] }}
          </div>
        </div>
        <div class="cards-a">
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[3] ? 1 : 0 }"
          >
            {{ playerCardsA[3] }}
          </div>
        </div>
        <div class="cards-a">
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[4] ? 1 : 0 }"
          >
            {{ playerCardsA[4] }}
          </div>
        </div>
        <div class="cards-a">
          <div
            class="card-number-a"
            :style="{ opacity: playerCardsA[5] ? 1 : 0 }"
          >
            {{ playerCardsA[5] }}
          </div>
        </div>
      </div>
    </div>
    <div class="section-total-and-bet-a">
      <div class="total-a fixed-total">
        <h2>Player A</h2>
        <h3>Total</h3>
        <p :style="{ opacity: hide ? 0 : 1 }">{{ total }}</p>
      </div>
      <button
        class="bet-a"
        @click="betA"
        :style="{ visibility: gamestarted ? 'visible' : 'hidden' }"
      >
        Bet
      </button>
    </div>
  </section>
</template>

<script>
export default {
  props: [
    "total",
    "playerCardsA",
    "isHiddenA",
    "hideAFirstCard",
    "gamestarted",
  ],
  data() {
    return {
      id: "A",
      hide: this.hideAFirstCard,
    };
  },
  methods: {
    betA() {
      this.$emit("A-clicked");
    },
    hideACard() {
      this.hide = true;
    },
    updateHide() {
      this.hide = this.hideAFirstCard;
    },
  },
};
</script>

<style>
.section-player-a {
  max-width: 150rem;
  height: 30rem;
  margin: 3rem auto;
  display: grid;
  grid-template-columns: 3fr 1fr;
}

.section-cards-a {
  font-size: 10rem;
  align-self: center;
  justify-self: center;
}

.cards-pool-a {
  display: flex;
  gap: 7rem;
  font-size: 2rem;
}

.cards-a {
  width: 6.3rem;
  height: 8.3rem;
  border: 2px solid black;
  border-radius: 5px;
  padding: 4rem 3rem;
  display: flex;
  justify-content: center;
  transition: opacity, 1s;
}

.card-number-a {
  opacity: 0;
  transition: opacity, 1s;
  font-size: 2.4rem;
}

.section-total-and-bet-a {
  font-size: 3rem;
  display: grid;
  grid-template-columns: 1fr;
  align-items: center;
  justify-items: center;
}

.total-a {
  display: grid;
  grid-template-columns: 1fr;
  justify-items: center;
  padding: 1rem 1rem;
  border: 3px solid black;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.bet-a {
  width: 30%;
  height: 30%;
  color: white;
  background-color: black;
  font-size: 2rem;
  border-radius: 5px;
  cursor: pointer;
}
</style>
