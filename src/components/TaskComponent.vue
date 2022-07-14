<script setup>
import { ref, defineEmits, defineProps } from "vue";

defineProps({
  elements: {
    type: Array,
    default: () => [],
  },
});

let id = ref(0);

const emit = defineEmits(["change-ratio", "add-task", "change-checked"]);

const taskValue = ref("");

const btnHandler = () => {
  emit("add-task", {
    id: `content__todo-${id.value}`,
    text: taskValue.value,
    checked: false,
  });
  taskValue.value = "";
  id.value += 1;
};

const checkboxHandler = (id) => {
  emit("change-checked", id);
};
</script>

<template>
  <div class="content">
    <form class="content__add">
      <input
        type="textbox"
        name="content__add"
        placeholder="Введите текст"
        v-model="taskValue"
      />
      <button type="button" class="content__add-button" @click="btnHandler" />
    </form>
    <ul class="content__todos-list">
      <li v-for="el in elements" :key="el.id">
        <input type="checkbox" :id="el.id" @click="checkboxHandler(el.id)" />
        <label :for="el.id">
          <span class="content__check"></span>
          {{ el.text }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style>
.content {
  padding-left: 23px;
  padding-top: 56px;
  padding-right: 17px;
}
.content form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  font-size: 20px;
}
.content__add > * {
  background: #fff;
  border: none;
  height: 67px;
  width: 390px;
  padding-left: 14px;
  padding-top: 22px;
  padding-bottom: 21px;
}
.content__add-button {
  background-color: #a0ffa4;
  width: 61px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 20px;
  background-image: url("@/assets/arrow.svg");
  background-repeat: no-repeat;
  background-position: center;
  cursor: pointer;
}
.content__todos-list {
  max-height: 390px;
  overflow-x: auto;
}
.content ul .content__todos-list {
  letter-spacing: none;
  height: 220px;
  overflow: auto;
  cursor: pointer;
}
.content li {
  user-select: none;
  margin-bottom: 10px;
  display: flex;
}
.content input[type="checkbox"] {
  display: none;
}
.content input[type="checkbox"] + label {
  color: #000000;
  font-weight: 400;
  font-size: 20px;
  line-height: 24px;
  cursor: pointer;
  position: relative;
  display: inline-block;
  padding: 22px 58px 21px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  width: 100%;
}
.content input[type="checkbox"] + label:hover {
  color: #fff;
  background-color: #f5b461;
}
.content input[type="checkbox"] + label span.content__check {
  left: 10px;
  top: 50%;
  position: absolute;
  transform: translatey(-50%);
  width: 28px;
  height: 28px;
  display: block;
  background: #fff;
  border-radius: 50%;
  border: 1px solid #d9d9d9;
}
.content input[type="checkbox"]:checked + label {
  color: rgba(0, 0, 0, 0.6);
  text-decoration: line-through;
}
.content input[type="checkbox"] + label span.content__check::after {
  width: 100%;
  height: 100%;
  content: "";
  display: block;
  position: absolute;
  background-image: url("@/assets/checked.svg");
  /* background-size: 13px 13px; */
  background-size: 65%;
  /* background-image: url(data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTkuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iTGF5ZXJfMSIgeD0iMHB4IiB5PSIwcHgiIHZpZXdCb3g9IjAgMCA0MjYuNjY3IDQyNi42NjciIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDQyNi42NjcgNDI2LjY2NzsiIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSI1MTJweCIgaGVpZ2h0PSI1MTJweCI+CjxwYXRoIHN0eWxlPSJmaWxsOiM2QUMyNTk7IiBkPSJNMjEzLjMzMywwQzk1LjUxOCwwLDAsOTUuNTE0LDAsMjEzLjMzM3M5NS41MTgsMjEzLjMzMywyMTMuMzMzLDIxMy4zMzMgIGMxMTcuODI4LDAsMjEzLjMzMy05NS41MTQsMjEzLjMzMy0yMTMuMzMzUzMzMS4xNTcsMCwyMTMuMzMzLDB6IE0xNzQuMTk5LDMyMi45MThsLTkzLjkzNS05My45MzFsMzEuMzA5LTMxLjMwOWw2Mi42MjYsNjIuNjIyICBsMTQwLjg5NC0xNDAuODk4bDMxLjMwOSwzMS4zMDlMMTc0LjE5OSwzMjIuOTE4eiIvPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8Zz4KPC9nPgo8L3N2Zz4K); */
  border-radius: 50%;
  border: 1px solid #a0ffa4;
  background-repeat: no-repeat;
  background-position: center;
  transform: scale(0);
  transition: transform 300ms cubic-bezier(0.3, 0, 0, 1.5);
}
.content input[type="checkbox"]:checked + label span.content__check::after {
  transform: scale(1);
}
.content input[type="checkbox"] + label span.content__check::before {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: block;
  content: "";
  position: absolute;
  border-radius: 50%;
  transform: scale(0);
}
</style>
