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
import Card from "./Card.vue";

export default {
  components: { Card },
  props: {
    attempts: {
      type: Number,
      required: true,
    },
    cards: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
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
          this.$emit("success");
          this.clearSelected();
          this.verifyWin();
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
    verifyWin() {
      const win = this.cards.filter((card) => card.flipped);
      if (win.length === 30) return this.$emit("endGame");
    },
  },
};
</script>

<style scoped>
.cards {
  display: flex;
  width: 99%;
  height: 80%;
  flex-wrap: wrap;
  align-items: center;
  margin-top: 8%;
  justify-content: space-around;
}
</style>
