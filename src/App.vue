<template>
  <div class="container">
    <HeaderC title="Task Tracker" />
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
import type { task } from "./utils/types";

export default {
  name: "App",
  components: { HeaderC, TasksC },
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
  },
};
</script>

<style scoped>
.container {
  display: flex;
  align-content: center;
  justify-content: center;
  border: 1px solid #ccc;
  padding: 1rem;
  margin: 0 auto;
  flex-direction: column;
  max-width: 420px;
}
</style>
