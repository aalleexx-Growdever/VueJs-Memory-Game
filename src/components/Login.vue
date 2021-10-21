<template>
  <div class="login">
    <h1>Selecione seu avatar:</h1>
    <div class="line">
      <div class="avatar">
        <img
          :src="romulojessica"
          width="100%"
          height="100%"
          key="romulojessica"
          :class="{
            selected: selected === romulojessica,
            shake: shake === 'avatar 1',
          }"
          @click="(selected = romulojessica), shaker('avatar 1')"
        />
      </div>
      <div class="avatar">
        <img
          :src="misamainara"
          width="100%"
          height="100%"
          key="misamainara"
          :class="{
            selected: selected === misamainara,
            shake: shake === 'avatar 2',
          }"
          @click="(selected = misamainara), shaker('avatar 2')"
        />
      </div>
      <div class="avatar alexbruna">
        <img
          :src="alexbruna"
          width="100%"
          height="100%"
          key="alexbruna"
          :class="{
            selected: selected === alexbruna,
            shake: shake === 'avatar 3',
          }"
          @click="(selected = alexbruna), shaker('avatar 3')"
        />
      </div>
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
import romulojessica from "../assets/card2.jpeg";
import misamainara from "../assets/card8.jpeg";
import alexbruna from "../assets/card12.jpeg";

export default {
  data() {
    return {
      username: "",
      selected: "",
      romulojessica,
      misamainara,
      alexbruna,
      shake: "",
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
    shaker(avatar) {
      this.shake = avatar;

      setTimeout(() => {
        this.shake = null;
      }, 500);
    },
  },
};
</script>

<style scoped>
.login {
  width: 80vw;
  height: 80vh;
  background-repeat: no-repeat;
  background-position: center bottom;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.login h1 {
  font-size: 5vh;
  color: black;
  padding: 0.5%;
  border-radius: 15%;
}

.line {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 40%;
  justify-content: space-evenly;
}

.avatar {
  width: 15%;
  height: 75%;
  opacity: 0.7;
}

.avatar img {
  border-radius: 50%;
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
}

.avatar img:hover {
  opacity: 1;
  cursor: pointer;
  border: 5px solid rgb(149, 149, 149);
}

.selected {
  border: 5px solid black;
  opacity: 1;
}

.inputName {
  width: 50%;
  font-size: 3.5vh;
  background-color: transparent;
  color: black;
  text-align: center;
  border-radius: 15px;
  outline: none;
}

.inputName::placeholder {
  color: black;
}

.btn {
  font-size: 3vh;
  border-radius: 10px;
  padding: 0.5% 2%;
  background-color: rgb(0, 0, 0);
  color: white;
}

.btn:hover {
  opacity: 0.7;
  cursor: pointer;
}

.shake {
  animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-2px, 0, 0);
  }
  20%,
  80% {
    transform: translate3d(3px, 0, 0);
  }
  30%,
  50%,
  70% {
    transform: translate3d(-5px, 0, 0);
  }
  40%,
  60% {
    transform: translate3d(5px, 0, 0);
  }
}
</style>
