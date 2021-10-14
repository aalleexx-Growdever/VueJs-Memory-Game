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
  width: 100%;
  height: 15%;
  display: flex;
  background-image: url("../assets/header.jpg");
  position: fixed;
  top: 0;
  justify-content: left;
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
}

.avatar {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  background-position: center;
  background-size: cover;
  margin-right: 3%;
}

.daenerys {
  background-image: url("../assets/daenerys.jpg");
}

.johnSnow {
  background-image: url("../assets/john-snow.webp");
}
.scorePoints {
  position: fixed;
  left: 300px;
  color: goldenrod;
  margin-left: 40%;
}

.attempts {
  position: fixed;
  left: 400px;
  color: red;
  margin-left: 40%;
}
</style>
