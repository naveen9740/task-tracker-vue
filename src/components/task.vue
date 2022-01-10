<template>
  <div
    @dblclick="$emit('dbl-Click', task.id)"
    :class="[task.reminder ? 'task reminder' : 'task']"
  >
    <h3>
      {{ task.text }}
      <span @click="onDelete(task.id)" class="fas">X</span>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>
<script>
export default {
  name: "task",
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      this.$emit("delete-Task", id);
    },
  },
  emits: ["delete-Task"],
};
</script>
<style>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
