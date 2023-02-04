<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="date"
        v-modal="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn" />
  </form>
</template>

<script lang="ts">
import type { task } from "../utils/types";

export default {
  name: "AddTask",
  data() {
    return {
      text: "Do something...",
      day: "",
      reminder: false,
    };
  },
  emits: ["add-task"],
  methods: {
    onSubmit(e: Event) {
      e.preventDefault();

      if (!this.text) {
        alert("Please enter task");
        return;
      }

      const newTask: task = {
        id: Math.floor(Math.random() * 99999999),
        text: this.text,
        reminder: this.reminder,
        date: this.day,
      };

      this.$emit("add-task", newTask);

      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
  max-width: 100%;
  padding: 0.5rem;
}
.form-control {
  margin: 20px 0;
  display: block;
  position: relative;
  padding: 6px;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  font-size: 16px;
  border-radius: 6px;
  border: 1px solid #ccc;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}

.btn {
  display: block;
  background-color: cadetblue;
  width: 100%;
  padding: 0.4rem;
  color: white;
  font-size: 1.2rem;
}

.btn:hover {
  transform: scale(1.01);
}

.btn:active {
  transform: scale(0.98);
}
</style>
