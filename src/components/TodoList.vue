<script setup>
// Importing the 'ref' function from Vue to create reactive data variables
import { ref } from "vue";

// 'newTask' holds the current value of the input field for a new task.
// 'ref' makes it reactive so the UI updates automatically when its value changes.
const newTask = ref("");

// 'tasks' is a reactive array that stores all added tasks.
const tasks = ref([]);

// Function to add a new task to the 'tasks' array.
// It checks if the input is not just empty spaces before adding.
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value); // Add the task to the list
    newTask.value = ""; // Clear the input field after adding
  }
};

// Function to remove a task based on its index in the 'tasks' array.
const removeTask = (index) => {
  tasks.value.splice(index, 1); // Remove one task at the given index
};
</script>

<template>
  <div class="container">
    <!-- Main heading of the Todo List component -->
    <h1>Todo List</h1>
    <div class="input-container">
      <!--
        Input field for new task.
        - v-model binds the input to 'newTask'
      -->
      <input v-model="newTask" placeholder="Add a new task" @keyup.enter="addTask" />
      <!--
        Button to add a task.
        When clicked, it triggers the addTask function.
      -->
      <button @click="addTask">Add To Do</button>
    </div>
    <!-- Unordered list rendering each task as a list item. -->
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <!-- Display the task text -->
        {{ task }}
        <!-- Button to remove the specific task. -->
        <button @click="removeTask(index)" class="remove-button">Remove</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.input-container {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.input-container input {
  flex: 1;
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

.input-container input::placeholder {
  color: #999;
}

.input-container button {
  padding: 0.5rem 1rem;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Remove default list styling */
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem;
  background: #f8f8f8;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}

.remove-button {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}
</style>
