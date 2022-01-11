<template>
  <div v-if="showAddTask">
    <AddTask @newTask="newTask" />
  </div>
  <Tasks v-bind:tasks="tasks" @delete-Task="deleteTask" @dbl-Click="dblClick" />
</template>

<script>
import AddTask from "../components/AddTask.vue";
import Tasks from "../components/tasks.vue";
import axios from "axios";

export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components: {
    AddTask,
    Tasks,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async newTask({ text, day, reminder }) {
      const res = await axios.post("api/tasks", { text, day, reminder });
      console.log(res);
      this.tasks = [...this.tasks, { text, day, reminder }];
    },
    async deleteTask(id) {
      if (confirm("Are u sureeeeee!!!!")) {
        const res = await axios.delete(`api/tasks/${id}`);

        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    dblClick(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },

    async fetchTasks() {
      const res = await axios.get("api/tasks");
      return res.data;
    },
    async fetchTask(id) {
      const res = await axios.get(`api/tasks/${id}`);
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
<style scoped></style>
