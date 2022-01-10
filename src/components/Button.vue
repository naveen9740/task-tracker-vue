<template>
  <button
    v-bind:style="{ background: color }"
    v-on:click="onClick()"
    @toggleClick="$emit('toggleClick')"
  >
    {{ btnText }} Task
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    btnText: {
      type: String,
      default: "Button",
    },

    color: String,
  },
  methods: {
    onClick() {
      this.$emit("toggleClick");
    },
  },
};
</script>

<style scoped></style>
