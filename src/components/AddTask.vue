<template>
  <form class="add-form">
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
export default {
  name: "AddTask",
  data: () => ({
    text: "Do something...",
    day: new Date(),
    reminder: false,
  }),
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
