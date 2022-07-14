<template>
  <div class="to-do-list">
    <HeaderComponent :ratio="ratio" @delete-tasks="deleteTasks" />
    <TaskComponent
      @add-task="addTask"
      @change-checked="changeChecked"
      :elements="elements"
    />
  </div>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent.vue";
import TaskComponent from "@/components/TaskComponent.vue";
import { computed, ref } from "vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    TaskComponent,
  },

  setup() {
    let elements = ref([]);

    const ratio = computed(() => {
      const checkedLength = elements.value.filter((el) => el.checked).length;
      return `${checkedLength}/${elements.value.length}`;
    });

    const addTask = (task) => {
      elements.value.push(task);
    };

    const changeChecked = (id) => {
      const index = elements.value.map((el) => el.id === id).indexOf(true);
      elements.value[index].checked = !elements.value[index].checked;
    };

    const deleteTasks = () => {
      elements.value = elements.value.filter((el) => !el.checked);
    };

    return {
      ratio,
      elements,
      addTask,
      changeChecked,
      deleteTasks,
    };
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.to-do-list {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 498px;
  height: 767px;
  background: #eeefff;
  border-radius: 12px;
  box-shadow: 0 7px 30px rgba(0, 0, 0, 0.3);
}
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400&display=swap");
body {
  min-height: 450px;
  height: 100vh;
  margin: 0;
  background: #fff;
  color: #fff;
  font-family: "Inter";
  font-weight: 400;
}
input,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
</style>
