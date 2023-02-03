<template>
  <div :key="task.id" v-for="task in tasks">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script lang="ts">
import Task from "./Task.vue";
import type { task } from "../utils/types";

export default {
  name: "Tasks-C",
  props: {
    tasks: Array<task>,
  },
  components: {
    Task,
  },
  emits: ["delete-task", "toggle-reminder"],
  created() {
    console.log("Tasks is created", this.tasks);
  },
};
</script>
