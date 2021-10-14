<template>
  <div id="app">
    <transition name="fade">
      <Login show v-if="login" @play="startGame($event)" />
    </transition>
    <transition name="fade">
      <Score :user="user" v-if="score" :attempts="attempts" :points="points" />
    </transition>
    <transition name="fade">
      <CardList v-if="cards" @success="success($event)" @fail="fail" />
    </transition>
  </div>
</template>

<script>
import Login from "./components/Login.vue";
import Score from "./components/Score.vue";
import CardList from "./components/CardList.vue";

export default {
  name: "App",
  components: { Login, Score, CardList },
  data() {
    return {
      user: {},
      login: false,
      score: false,
      cards: false,
      attempts: 10,
      points: 0,
    };
  },
  methods: {
    startGame(user) {
      this.user = user;
      this.closeLogin();
    },
    closeLogin() {
      this.login = false;
      setTimeout(() => {
        this.score = true;
        this.cards = true;
      }, 3000);
    },
    success() {
      this.points += 10;
    },
    fail() {
      this.attempts -= 1;
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
  background: radial-gradient(
    circle,
    rgba(0, 0, 0, 1) 0%,
    rgba(122, 100, 100, 1) 50%,
    rgba(0, 0, 0, 1) 100%
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
  transition: opacity 3s;
}
</style>
