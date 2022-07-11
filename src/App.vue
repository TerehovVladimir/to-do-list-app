<template>
  <HeaderComponent />
  <TaskComponent />
  <TaskListComponent />
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent.vue";
import TaskComponent from "@/components/TaskComponent.vue";
import TaskListComponent from "@/components/TaskListComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    TaskComponent,
    TaskListComponent,
  },
};
</script>

<style>
#app {
}
</style>
