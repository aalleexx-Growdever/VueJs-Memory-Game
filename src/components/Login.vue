<template>
  <div class="login">
    <h1>Selecione seu avatar:</h1>
    <div class="line">
      <div
        class="avatar daenerys"
        :class="{ selected: selected === 'Daenerys' }"
        @click="selected = 'Daenerys'"
      ></div>
      <div
        class="avatar johnSnow"
        :class="{ selected: selected === 'John Snow' }"
        @click="selected = 'John Snow'"
      ></div>
    </div>
    <input
      class="inputName"
      type="text"
      placeholder="Digite seu nome ..."
      v-model="username"
      @keypress.enter="play"
    />
    <button @click="play" class="btn">Jogar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      selected: "",
    };
  },
  methods: {
    play() {
      const user = {
        name: this.username,
        avatar: this.selected,
      };

      this.$emit("play", user);
    },
  },
};
</script>

<style scoped>
.login {
  width: 80vw;
  height: 80vh;
  border-radius: 40px;
  background-image: url("../assets/loginBackground.jpg");
  background-repeat: no-repeat;
  background-position: center bottom;
  border: 5px solid indigo;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.login h1 {
  font-size: 5vh;
  color: white;
  background-color: indigo;
  padding: 0.5%;
  border-radius: 15%;
}

.line {
  display: flex;
  flex-direction: row;
  width: 100%;
  min-height: 35%;
  justify-content: space-evenly;
}

.avatar {
  width: 15%;
  height: 90%;
  border-radius: 50%;
  background-position: center;
  background-size: cover;
  opacity: 0.7;
}

.avatar:hover {
  opacity: 1;
  width: 18%;
  height: 100%;
}

.daenerys {
  background-image: url("../assets/daenerys.jpg");
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
  background-color: white;
}

.johnSnow {
  background-image: url("../assets/john-snow.webp");
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
  background-color: white;
}

.selected {
  border: 5px solid indigo;
  opacity: 1;
  width: 18%;
  height: 100%;
}

.inputName {
  width: 50%;
  font-size: 3.5vh;
  background-color: indigo;
  color: white;
  border-radius: 5px;
  text-align: center;
}

.btn {
  font-size: 3vh;
  border-radius: 10px;
  padding: 0.5% 2%;
  background-color: indigo;
  color: white;
}

.btn:hover {
  opacity: 0.8;
  cursor: pointer;
}
</style>
