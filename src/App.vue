<template>
  <div class="container">
    <HeaderC
      @toggle-show-add-task="toggleShowAddTask"
      :showAddTask="showAddTask"
      title="Task Tracker"
    />

    <section v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </section>

    <section>
      <TasksC
        @delete-task="deleteTask"
        @toggle-reminder="toggleTaskReminder"
        @fetch-task="fetchTask"
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
      showAddTask: false,
    };
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
  methods: {
    async deleteTask(id: number) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
    toggleShowAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async toggleTaskReminder(id: number) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });

      const data = await res.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async addTask(formData: any) {
      // console.log("🚀 ~ file: App.vue:55 ~ addTask ~ formData", formData);
      const res = await fetch("http://localhost:5000/tasks", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(formData),
      });
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async fetchTasks() {
      const res = await fetch("http://localhost:5000/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id: number) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`);
      const data = await res.json();
      return data;
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
