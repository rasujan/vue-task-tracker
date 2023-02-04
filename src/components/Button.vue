<template>
  <button @click="onClick()" :style="{ background: color }">
    {{ label }}
  </button>
</template>

<script lang="ts">
export default {
  name: "Button-C",
  props: {
    label: {
      type: String,
    },
    color: {
      type: String,
      default: "#A5D8FF",
    },
    action: {
      type: Function,
    },
  },
  methods: {
    onClick() {
      this.$emit("btn-action");
    },
  },
};
</script>

<style scoped>
button {
  border: 1px solid;
  border-radius: 6px;
  background: #fefefe;
  min-width: 5rem;
  padding: 4px;
  cursor: pointer;
}
</style>
