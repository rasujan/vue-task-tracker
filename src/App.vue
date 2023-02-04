<template>
  <div class="container">
    <HeaderC title="Task Tracker" />

    <section>
      <AddTask @add-task="addTask" />
    </section>

    <section>
      <TasksC
        @delete-task="deleteTask"
        @toggle-reminder="toggleTask"
        :tasks="tasks"
      />
    </section>
  </div>
</template>

<script lang="ts">
import HeaderC from "./components/Header.vue";
import TasksC from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import type { task } from "./utils/types";

export default {
  name: "App",
  components: { HeaderC, TasksC, AddTask },
  data() {
    return {
      tasks: [] as task[],
    };
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Wash the clothes",
        reminder: true,
        date: "2023-01-03",
      },
      {
        id: 2,
        text: "Do the dishes",
        reminder: false,
        date: "2023-02-10",
      },
      {
        id: 3,
        text: "Clean the room",
        reminder: true,
        date: "2023-02-03",
      },
    ];
  },
  methods: {
    deleteTask(id: number) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    toggleTask(id: number) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
    addTask(formData: task) {
      console.log("🚀 ~ file: App.vue:65 ~ addTask ~ formData", formData);
      this.tasks = [...this.tasks, formData];
    },
  },
};
</script>

<style scoped>
.container {
  display: block;
  border: 1px solid #ccc;
  margin: 0 auto;
  min-width: 420px;
  max-width: max-content;
}
</style>
