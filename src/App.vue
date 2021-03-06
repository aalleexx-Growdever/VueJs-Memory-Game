<template>
  <div id="app">
    <transition name="fade">
      <Login show v-if="login" @play="startGame($event)" />
    </transition>
    <transition name="fade">
      <Score :user="user" v-if="score" :attempts="attempts" :points="points" />
    </transition>
    <transition name="fade">
      <CardList
        v-if="cards"
        :attempts="attempts"
        :cards="list"
        @success="success($event)"
        @fail="fail"
        @endGame="setEndGame"
      />
    </transition>
    <transition name="fade">
      <EndGame
        v-if="endGame"
        @newGame="newGame"
        @playAgain="play"
        :user="user"
        :points="points"
        :attempts="attempts"
      />
    </transition>
  </div>
</template>

<script>
import cardArray from "./utils/cards";

import Login from "./components/Login.vue";
import Score from "./components/Score.vue";
import CardList from "./components/CardList.vue";
import EndGame from "./components/EndGame.vue";

export default {
  name: "App",
  components: { Login, Score, CardList, EndGame },
  data() {
    return {
      user: {},
      list: null,
      login: false,
      score: false,
      cards: false,
      endGame: false,
      attempts: 10,
      points: 0,
    };
  },
  methods: {
    startGame(user) {
      this.user = user;
      this.play();
    },
    success(sequence) {
      this.attempts += sequence;
      this.points += 10 * sequence;
    },
    fail() {
      this.attempts -= 1;
      if (this.attempts === 0) return this.setEndGame;
    },
    setEndGame() {
      setTimeout(() => {
        this.unflipCards(cardArray);
      }, 1000);
      setTimeout(() => {
        this.cards = false;
      }, 2000);
      setTimeout(() => {
        this.endGame = true;
      }, 4000);
    },
    shuffleArray(arr) {
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    },
    unflipCards(arr) {
      arr.forEach((card) => {
        card.flipped = false;
      });
    },
    play() {
      this.login = false;
      this.endGame = false;
      this.score = false;
      this.list = this.shuffleArray(cardArray);
      setTimeout(() => {
        this.points = 0;
        this.attempts = 10;
        this.score = true;
        this.cards = true;
      }, 2000);
    },
    newGame() {
      this.endGame = false;
      this.score = false;
      this.list = this.shuffleArray(cardArray);
      setTimeout(() => {
        this.points = 0;
        this.attempts = 10;
        this.login = true;
      }, 2000);
    },
  },
  watch: {
    attempts() {
      if (this.attempts === 0) return this.setEndGame();
    },
  },
  created() {
    setTimeout(() => {
      this.login = true;
    }, 1000);
  },
};
</script>

<style>
html,
body {
  margin: 0 auto;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
  background: linear-gradient(
    0deg,
    rgba(125, 59, 59, 1) 0%,
    rgba(218, 191, 132, 1) 100%
  );
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 2s;
}
</style>
