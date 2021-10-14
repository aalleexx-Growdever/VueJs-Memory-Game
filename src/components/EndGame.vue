<template>
  <div class="endGame"></div>
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
  },
};
</script>

<style scoped>
.endGame {
  width: 100%;
}
</style>
