<template>
  <header>
    <h2>Hello {{ text }}</h2>
    <Button
      @toggleClick="$emit('toggle-Click')"
      class="btn"
      :btnText="showAddTask ? 'Close' : 'Add'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";

export default {
  name: "Header",
  props: {
    text: {
      type: String,
    },
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
