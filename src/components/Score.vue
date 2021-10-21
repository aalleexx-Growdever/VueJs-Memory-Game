<template>
  <div class="score">
    <div class="box">
      <div class="avatar">
        <img :src="user.avatar" width="100%" height="100%" />
      </div>
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
  position: absolute;
  top: 0;
  border-bottom: 2px solid black;
}

.box {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  padding-left: 1%;
}

.box h3 {
  color: black;
  font-size: 3vh;
}

.avatar {
  width: 8%;
  height: 95%;
  margin-right: 1%;
}

.avatar img {
  border-radius: 50%;
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;
}

.scorePoints {
  position: absolute;
  right: 15%;
  color: rgb(48, 149, 48);
  font-size: 6vh;
}

.attempts {
  position: absolute;
  right: 5%;
  color: red;
  font-size: 6vh;
}
</style>
