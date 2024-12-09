<template>
  <div class="todo-app">
    <h1>Liste de tâches</h1>

    <!-- Task input section -->
    <div class="input-section">
      <input
        type="text"
        v-model="newTask"
        placeholder="Entrez une tâche"
        @keyup.enter="addTask"
      />
      <button @click="addTask">Ajouter une tâche</button>
    </div>

    <!-- Task list -->
    <ul class="task-list">
      <li
        v-for="(task, index) in tasks"
        :key="index"
        :class="{ completed: task.completed }"
      >
        <label>
          <!-- Task number and checkbox -->
          <input type="checkbox" v-model="task.completed" />
          {{ index + 1 }}. <span>{{ task.text }}</span>
        </label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "", // Text of the new task
      tasks: [], // List of tasks
    };
  },
  methods: {
    // Add a new task
    addTask() {
      if (this.newTask.trim() === "") {
        return; // Do not add an empty task
      }
      this.tasks.push({ text: this.newTask, completed: false });
      this.newTask = ""; // Clear the input field
    },
  },
};
</script>

<style scoped>
.todo-app {
  max-width: 400px;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  text-align: center;
}

h1 {
  color: #4caf50;
}

.input-section {
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 8px;
  width: 70%;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 12px;
  margin-left: 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-list li {
  padding: 10px;
  font-size: 18px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ddd;
}

.task-list li.completed span {
  text-decoration: line-through;
  color: gray;
}

.task-list li label {
  cursor: pointer;
  display: flex;
  align-items: center;
}

.task-list li input[type="checkbox"] {
  margin-right: 10px;
}
</style>
