<template>
  <div class="container">
    <Header
      @toggle-Click="toggleClick"
      :showAddTask="showAddTask"
      text="Task Tracker"
    />
    <div v-if="showAddTask">
      <AddTask @newTask="newTask" />
    </div>
    <Tasks
      v-bind:tasks="tasks"
      @delete-Task="deleteTask"
      @dbl-Click="dblClick"
    />
    <router-view></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/tasks.vue";
import AddTask from "./components/AddTask.vue";
import Footer from "./components/Footer.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
    Footer,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
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
    toggleClick() {
      this.showAddTask = !this.showAddTask;
      console.log(this.showAddTask);
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

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
