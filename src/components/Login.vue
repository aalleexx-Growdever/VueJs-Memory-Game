<template>
  <div class="login">
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
  width: 60vw;
  height: 60vh;
  border-radius: 40px;
  padding: 5%;
  background-image: url("../assets/loginBackground.jpg");
  background-repeat: no-repeat;
  background-position: center bottom;
  border: 5px solid whitesmoke;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.line {
  display: flex;
  flex-direction: row;
  width: 100%;
  min-height: 250px;
  justify-content: space-around;
  margin-bottom: 5%;
  padding: 5%;
}

.avatar {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  background-position: center;
  background-size: cover;
  opacity: 0.8;
}

.avatar:hover {
  opacity: 1;
  width: 220px;
  height: 220px;
}

.daenerys {
  background-image: url("../assets/daenerys.jpg");
}

.johnSnow {
  background-image: url("../assets/john-snow.webp");
}

.selected {
  border: 2px solid rgba(0, 0, 0, 0.8);
  opacity: 1;
  width: 220px;
  height: 220px;
}

.inputName {
  width: 50%;
  font-size: larger;
  border: 1px solid white;
  border-radius: 5px;
  text-align: center;
  margin-bottom: 5%;
}

.btn {
  width: 100px;
  font-size: large;
  border-radius: 10px;
}

.btn:hover {
  opacity: 0.8;
  cursor: pointer;
}
</style>
