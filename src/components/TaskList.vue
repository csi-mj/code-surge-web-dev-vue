<template>
  <div class="task-list">
    <h2>{{ state }}</h2>
    <ul v-if="tasks.length">
      <li v-for="task in tasks" :key="task.taskTitle">
        <span @click="emitSwitchTask(task.taskTitle)">{{
          task.taskTitle
        }}</span>
        <button @click="emitDeleteTask(task.taskTitle)">Delete</button>
      </li>
    </ul>
    <p v-else>No tasks in this state.</p>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  tasks: {
    type: Array,
  },
  state: {
    type: String,
  },
});

const emit = defineEmits(["delete-task", "switch-task"]);

const emitDeleteTask = (taskTitle) => {
  emit("delete-task", taskTitle);
};
const emitSwitchTask = (taskTitle) => {
  emit("switch-task", taskTitle);
};
</script>

<style>
.task-lists {
  display: flex;
  width: 100%;
  justify-content: space-evenly;
}
.task-list {
  width: 100%;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.task-list ul {
  list-style: none;
  padding: 0;
}
.task-list li {
  margin: 5px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}
.task-list button {
  margin-left: 10px;
  padding: 5px 10px;
  background-color: red;
  color: white;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
.task-list button:hover {
  background-color: darkred;
}
</style>
