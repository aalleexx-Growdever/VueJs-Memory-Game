<template>
  <div class="endGame">
    <div class="text">
      <p v-if="!winner">Não foi desta vez {{ user.name }} :{</p>
      <p v-if="!winner">Você fez {{ points }} pontos.</p>
      <p v-if="!winner">Mas não desanime! Vamos tentar novamente?</p>
      <p v-if="winner">Parabéns {{ user.name }}, você conseguiu!!!</p>
      <p v-if="winner">
        Você fez {{ points }} pontos e ainda sobrou {{ attempts }} tentativas.
      </p>
      <p v-if="winner">Que tal tentar bater teus pontos em um novo jogo?</p>
    </div>
    <div class="btnBox">
      <button class="btn" @click="playAgain">Bora jogar!!!</button>
      <button class="btn" @click="newGame">Começar do zero</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    points: {
      type: Number,
      required: true,
    },
    attempts: {
      type: Number,
      required: true,
    },
    user: {
      type: Object,
      required: true,
    },
  },
  methods: {
    newGame() {
      this.$emit("newGame");
    },
    playAgain() {
      this.$emit("playAgain");
    },
  },
  computed: {
    winner() {
      console.log(this.attempts);
      return this.attempts === 0 ? false : true;
    },
  },
};
</script>

<style scoped>
.endGame {
  width: 100%;
  height: 100%;
  margin-top: 7%;
  background-size: cover;
  display: flex;
  flex-direction: column;
  justify-content: left;
}

.text {
  width: 40%;
  height: 70%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.text p {
  font-size: 5vh;
  color: black;
}

.btnBox {
  width: 40%;
  height: 20%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.btn {
  font-size: 3vh;
  border-radius: 10px;
  padding: 0.5% 2%;
  background-color: black;
  color: white;
}

.btn:hover {
  opacity: 0.8;
  cursor: pointer;
}
</style>
