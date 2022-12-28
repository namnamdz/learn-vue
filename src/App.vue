<template>
  <div class="app">
    <TaskLevel />
  </div>
</template>

<script>
import TaskLevel from "./views/TaskLevel.vue";
export default {
  name: "App",
  components: {
    TaskLevel,
  },
};
</script>

<style scoped>
.app {
  margin: 0 auto;
}
</style>
