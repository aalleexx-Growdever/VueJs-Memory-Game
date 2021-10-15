<template>
  <div class="score">
    <div class="box">
      <div
        class="avatar"
        :class="{
          daenerys: user.avatar === 'Daenerys',
          johnSnow: user.avatar === 'John Snow',
        }"
      ></div>
      <h3>{{ user.name }}</h3>
      <h1 class="scorePoints">{{ points }}</h1>
      <h1 class="attempts">{{ attempts }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    user: {
      type: Object,
      required: true,
    },
    attempts: {
      type: Number,
      required: true,
    },
    points: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.score {
  width: 100vw;
  height: 15vh;
  display: flex;
  background-image: url("../assets/header.jpg");
  background-size: cover;
  position: absolute;
  top: 0;
}

.box {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  padding-left: 1%;
}

.box h3 {
  color: white;
  font-size: 3vh;
}

.avatar {
  width: 6%;
  height: 80%;
  border-radius: 50%;
  margin-right: 3%;
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
  background-color: white;
}

.daenerys {
  background-image: url("../assets/daenerys.jpg");
}

.johnSnow {
  background-image: url("../assets/john-snow.webp");
}
.scorePoints {
  position: absolute;
  right: 37%;
  color: goldenrod;
  font-size: 6vh;
}

.attempts {
  position: absolute;
  right: 30%;
  color: red;
  font-size: 6vh;
}
</style>
