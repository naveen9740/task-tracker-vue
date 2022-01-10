<template>
  <div>
    <div v-for="task in tasks" :key="task.id">
      <!-- <li>{{ task?.id }}</li> -->
      <task
        :task="task"
        @dbl-Click="$emit('dbl-Click', task.id)"
        @delete-task="$emit('delete-Task', task.id)"
      />
    </div>
  </div>
</template>
<script>
import task from "./task.vue";
export default {
  components: { task },
  name: "Tasks",
  props: {
    tasks: Array,
  },
};
</script>
<style scoped></style>
