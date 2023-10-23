<template>
  <section class="section-player-b">
    <div class="section-total-and-bet-b">
      <div class="total-b">
        <h2>Player B</h2>
        <h3>Total</h3>
        <p :style="{ opacity: hide ? 0 : 1 }">{{ total }}</p>
      </div>
      <button
        class="bet-b"
        @click="betB"
        :style="{ visibility: gamestarted ? 'visible' : 'hidden' }"
      >
        Bet
      </button>
    </div>
    <div class="section-cards-b">
      <h1 :style="{ display: isHiddenB ? 'block' : 'none' }">Player B</h1>
      <div
        class="cards-pool-b"
        :style="{ display: isHiddenB ? 'none' : 'flex' }"
      >
        <div
          class="cards-b first-card"
          @click="hideBCard"
          :style="{ opacity: hide ? 0 : 1 }"
        >
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[0] ? 1 : 0 }"
          >
            {{ playerCardsB[0] }}
          </div>
        </div>
        <div class="cards-b">
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[1] ? 1 : 0 }"
          >
            {{ playerCardsB[1] }}
          </div>
        </div>
        <div class="cards-b">
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[2] ? 1 : 0 }"
          >
            {{ playerCardsB[2] }}
          </div>
        </div>
        <div class="cards-b">
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[3] ? 1 : 0 }"
          >
            {{ playerCardsB[3] }}
          </div>
        </div>
        <div class="cards-b">
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[4] ? 1 : 0 }"
          >
            {{ playerCardsB[4] }}
          </div>
        </div>
        <div class="cards-b">
          <div
            class="card-number-b"
            :style="{ opacity: playerCardsB[5] ? 1 : 0 }"
          >
            {{ playerCardsB[5] }}
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: [
    "total",
    "playerCardsB",
    "isHiddenB",
    "hideBFirstCard",
    "gamestarted",
  ],
  data() {
    return {
      id: "B",
      hide: this.hideBFirstCard,
    };
  },
  methods: {
    betB() {
      this.$emit("B-clicked");
    },
    hideBCard() {
      this.hide = true;
    },
    updateHide() {
      this.hide = this.hideBFirstCard;
    },
  },
};
</script>

<style>
.section-player-b {
  max-width: 150rem;
  height: 30rem;
  margin: 3rem auto;
  display: grid;
  grid-template-columns: 1fr 3fr;
}

.section-cards-b {
  font-size: 10rem;
  align-self: center;
  justify-self: center;
}

.cards-pool-b {
  display: flex;
  gap: 7rem;
  font-size: 2rem;
}

.cards-b {
  width: 6.3rem;
  height: 8.3rem;
  border: 2px solid black;
  border-radius: 5px;
  padding: 4rem 3rem;
  display: flex;
  justify-content: center;
  transition: opacity, 1s;
}

.card-number-b {
  opacity: 0;
  transition: opacity, 1s;
  font-size: 2.4rem;
}

.section-total-and-bet-b {
  font-size: 3rem;
  display: grid;
  grid-template-columns: 1fr;
  align-items: center;
  justify-items: center;
}

.total-b {
  display: grid;
  grid-template-columns: 1fr;
  justify-items: center;
  padding: 1rem 1rem;
  border: 3px solid black;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.bet-b {
  width: 30%;
  height: 30%;
  color: white;
  background-color: black;
  font-size: 2rem;
  border-radius: 5px;
  cursor: pointer;
}
</style>
