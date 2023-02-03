<template>
  <header>
    <h1>{{ title }}</h1>
    <ButtonC label="Add" color="#96F2D7" />
  </header>
</template>

<script lang="ts">
import ButtonC from "./Button.vue";

export default {
  name: "Header-C",
  props: {
    title: {
      type: String,
      default: "hello world",
    },
  },
  components: {
    ButtonC,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

h1 {
  margin: 0.5rem;
  font-size: 1.5rem;
}
</style>
