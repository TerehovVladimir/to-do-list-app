<script setup>
import { defineEmits, defineProps, computed } from "vue";

defineProps({
  ratio: {
    type: String,
    default: "0/0",
  },
});

const date = computed(() => {
  return new Date()
    .toLocaleTimeString("ru", {
      year: "numeric",
      month: "numeric",
      day: "numeric",
      timeZone: "UTC",
    })
    .slice(0, 10);
});

const weekDay = computed(() => {
  let days = ["ВС", "ПН", "ВТ", "СР", "ЧТ", "ПТ", "СБ"];
  const date = new Date();

  return days[date.getDay()];
});

const emit = defineEmits(["delete-tasks"]);

const deleteTasks = () => {
  emit("delete-tasks");
};
</script>

<template>
  <div class="header-inner">
    <p class="header-inner__current-date">{{ date }}</p>
    <p class="header-inner__current-weekday">{{ weekDay }}</p>
    <button
      class="header-inner__delete-button"
      type="button"
      @click="deleteTasks"
    >
      +
    </button>
    <div class="header-inner__tasks-info">
      <span>Tasks</span>
      <span class="header-inner__tasks-count">{{ ratio }}</span>
    </div>
  </div>
</template>

<style>
.header-inner {
  display: flex;
  height: 226px;
  display: flex;
  flex-direction: column;
  background: #b1b7ff;
  content: "";
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
.header-inner__current-date {
  padding-left: 20px;
  padding-top: 20px;
  font-size: 24px;
  color: black;
}
.header-inner__current-weekday {
  padding-left: 20px;
  font-size: 24px;
  color: black;
}
.header-inner__tasks-info {
  display: flex;
  position: relative;
  flex-direction: column;
  font-size: 50px;
  padding-left: 342px;
  bottom: 10px;
}
span.header-inner__tasks-count {
  text-align: right;
  padding-right: 20px;
}
.header-inner__delete-button {
  position: absolute;
  width: 70px;
  height: 70px;
  background-color: #fc7b7b;
  border-radius: 50%;
  top: 25%;
  border: none;
  color: white;
  font-size: 40px;
  right: 17px;
  text-align: center;
  vertical-align: middle;
  transform: rotate(45deg);
  cursor: pointer;
}
</style>
