<template>
  <div class="card" @click="emitEvent">
    <transition name="flip">
      <img :src="image" width="100%" height="100%" :key="card.flipped" />
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    card: {
      type: Object,
      required: true,
    },
  },
  computed: {
    image: function () {
      return this.card.flipped ? this.card.front : this.card.back;
    },
  },
  methods: {
    emitEvent() {
      this.$emit("select", this.card);
    },
  },
};
</script>

<style scoped>
.card {
  width: 9.2%;
  height: 30%;
  border-radius: 10px;
}

.card img {
  object-fit: cover;
  border-radius: 10px;
}

.card:hover {
  cursor: pointer;
  opacity: 0.8;
  box-shadow: 4px 4px rgb(0, 0, 0);
}

.flip-enter-active {
  transition: all 0.8s ease-in-out;
}

.flip-leave-active {
  transition: all 0.8s ease-in-out;
}

.flip-enter,
.flip-leave {
  transform: rotateY(180deg);
  opacity: 0;
}
</style>
