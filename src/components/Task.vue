<template>
  <div
    @click="$emit('fetch-task', task?.id)"
    @dblclick="$emit('toggle-reminder', task?.id)"
    :class="[task?.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task?.text }}
      <i @click="$emit('delete-task', task?.id)" class="fas fa-times" />
    </h3>
    <p>{{ task?.date }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";
import type { task as tTask } from "../utils/types";

export default defineComponent({
  name: "task-c",
  props: {
    task: Object as PropType<tTask>,
  },
});
</script>

<style>
.task {
  border-radius: 8px;
  background-color: rgb(231, 255, 244);
  margin: 0.2rem 0.5rem;
  padding: 0.5rem;
}

.task h3 {
  display: flex;
  justify-content: space-between;
  margin: 0.3rem 0;
}

.task .fa-times {
  color: darkred;
  margin: 0 1rem;
}

.reminder {
  border-left: 4px solid #1299ee;
}
</style>
