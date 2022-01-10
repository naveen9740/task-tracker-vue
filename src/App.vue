<template>
  <div class="container">
    <Header
      @toggle-Click="toggleClick"
      :showAddTask="showAddTask"
      text="Hello"
    />
    <div v-if="showAddTask">
      <AddTask @newTask="newTask" />
    </div>
    <Tasks
      v-bind:tasks="tasks"
      @delete-Task="deleteTask"
      @dbl-Click="dblClick"
    />
    <!-- <button>hello</button> -->
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: true,
    };
  },
  methods: {
    newTask(newlyAddedTask) {
      this.tasks = [...this.tasks, newlyAddedTask];
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
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
  },
  created() {
    this.tasks = [
      { id: 1, text: "Brush Teeth", reminder: true, day: "March 1st 6.30pm" },
      { id: 2, text: "Dinner", reminder: false, day: "March 1st 2.30pm" },
      { id: 3, text: "Sleep", reminder: true, day: "March 1st 10.30pm" },
    ];
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
