<template>
  <div class="cards">
    <Card
      v-for="(card, i) in cards"
      :key="i"
      :card="card"
      @select="select($event)"
    />
  </div>
</template>

<script>
import cards from "../utils/cards";
import Card from "./Card.vue";

export default {
  components: { Card },
  data() {
    return {
      cards,
      card1: null,
      card2: null,
      click: true,
    };
  },
  methods: {
    select(card) {
      if (card.flipped || !this.click) return;
      if (this.card1) {
        this.card2 = card;
        this.flipCard(card, true);
        if (this.card1.name === this.card2.name) {
          this.$emit("success", [this.card1, this.card2]);
          this.clearSelected();
        } else {
          this.stopClick();
          this.$emit("fail");
          this.flipCard(this.card1, false);
          this.flipCard(this.card2, false);
          this.clearSelected();
        }
      } else {
        this.card1 = card;
        this.flipCard(card, true);
      }
    },
    clearSelected() {
      this.card1 = null;
      this.card2 = null;
    },
    flipCard(flipped, to) {
      this.cards.map((card) => {
        if (card === flipped) {
          if (to === true) {
            card.flipped = to;
          } else {
            setTimeout(() => {
              card.flipped = to;
            }, 1500);
          }
        }
      });
    },
    stopClick() {
      this.click = false;
      setTimeout(() => {
        this.click = true;
      }, 1500);
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
</style>
