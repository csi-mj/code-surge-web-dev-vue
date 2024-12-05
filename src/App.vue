<template>
  <div>
    <h1>Task Manager</h1>
    <div class="task-input">
      <input v-model="newTaskTitle" type="text" placeholder="Enter new task" />
      <button class="add-task-button" @click="addTask">Add Task</button>
    </div>

    <div class="task-lists">
      <TaskList
        v-for="state in taskStates"
        :key="state"
        :tasks="filterTasksByState(state)"
        :state="state"
        @delete-task="deleteTask"
        @switch-task="switchTask"
      />
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import TaskList from "./components/TaskList.vue";

const newTaskTitle = ref("");
const taskStates = ref(["TODO", "INPROG", "COMPLETED"]);

const taskData = ref([
  { taskTitle: "Clean bed", state: "TODO" },
  { taskTitle: "Have Breakfast", state: "INPROG" },
  { taskTitle: "Sleep", state: "COMPLETED" },
  { taskTitle: "Gym", state: "TODO" },
]);

const filterTasksByState = (state) => {
  return taskData.value.filter((task) => task.state === state);
};

const deleteTask = (taskTitle) => {
  taskData.value = taskData.value.filter(
    (task) => task.taskTitle !== taskTitle
  );
};

const switchTask = (taskTitle) => {
  const task = taskData.value.find((task) => task.taskTitle === taskTitle);
  if (task) {
    const currentIndex = taskStates.value.indexOf(task.state);
    task.state = taskStates.value[(currentIndex + 1) % taskStates.value.length];
  }
};

const addTask = () => {
  taskData.value.push({ taskTitle: newTaskTitle.value, state: "TODO" });
  newTaskTitle.value = "";
};
</script>

<style scoped>
input {
  width: 500px;
  height: 40px;
  border-radius: 8px;
  border: 1px solid black;
  margin-right: 10px;
  padding: 2px 8px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.add-task-button {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background-color: #256cc8;
  color: white;
  border: 1px solid #a7a7a785;
  border-radius: 8px;
  min-width: 200px;
  padding: 6px 18px;
  margin-left: 10px;
  cursor: pointer;
  font-size: 16px;
}

.task-lists {
  margin-top: 40px;
}
</style>
