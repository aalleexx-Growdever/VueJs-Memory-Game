<template>
  <div class="cards">
    <div
      class="card"
      v-for="(card, i) in cards"
      :key="i"
      @click="select(card, i)"
    >
      <img
        src="../assets/backCard.jpg"
        :id="card.name + '-' + i"
        width="100%"
        height="100%"
      />
    </div>
  </div>
</template>

<script>
import cards from "../utils/cards";

export default {
  data() {
    return {
      cards,
      card1: null,
      index1: null,
      card2: null,
      index2: null,
      click: true,
    };
  },
  methods: {
    select(card, i) {
      if (card.flipped || !this.click) return;
      if (this.card1) {
        this.card2 = card;
        this.index2 = i;
        this.stopClick();
        this.flipCard(card, true, i);
        if (this.card1.name === this.card2.name) {
          this.$emit("success", [this.card1, this.card2]);
          this.clearSelected();
        } else {
          this.$emit("fail");
          this.flipCard(this.card1, false, this.index1);
          this.flipCard(this.card2, false, this.index2);
          this.clearSelected();
        }
      } else {
        this.card1 = card;
        this.index1 = i;
        this.flipCard(card, true, i);
      }
    },
    clearSelected() {
      this.card1 = null;
      this.card2 = null;
      this.index1 = null;
      this.index2 = null;
    },
    flipCard(flipped, to, i) {
      this.cards.map((card) => {
        if (card === flipped) {
          if (to === true) {
            card.flipped = to;
            document
              .getElementById(`${card.name}-${i}`)
              .setAttribute("src", card.front);
          } else {
            card.flipped = to;
            setTimeout(() => {
              document
                .getElementById(`${card.name}-${i}`)
                .setAttribute("src", card.back);
            }, 1500);
          }
        }
      });
    },
    stopClick() {
      this.click = false;
      setTimeout(() => {
        this.click = true;
      }, 2000);
    },
  },
};
</script>

<style scoped>
.cards {
  display: flex;
  width: 100%;
  height: 85%;
  flex-wrap: wrap;
  align-items: center;
  padding-top: 7.5%;
  justify-content: space-around;
}

.card {
  width: 9.8%;
  height: 33%;
  background-color: black;
  background-size: contain;
  background-position: center;
}

.card:hover {
  cursor: pointer;
  opacity: 0.6;
  box-shadow: 2px 2px white;
}
</style>
