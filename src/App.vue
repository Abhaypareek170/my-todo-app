<template>
  <div id="app">
    <h1>To-Do List</h1>
    <div class="folder-input">
      <input
        v-model="newFolderName"
        type="text"
        placeholder="Enter folder name"
      />
      <button @click="addFolder">Create Folder</button>
    </div>

    <div
      v-for="(folder, folderIndex) in folders"
      :key="folderIndex"
      class="folder"
    >
      <h2>{{ folder.name }}</h2>
      <div class="task-input">
        <input
          v-model="folder.newTask"
          type="text"
          placeholder="Add a new task"
        />
        <button @click="addTask(folderIndex)">Add Task</button>
      </div>

      <div
        v-for="(task, taskIndex) in folder.tasks"
        :key="taskIndex"
        class="task"
      >
        <label>
          <input type="checkbox" v-model="task.completed" />
          <span :class="{ completed: task.completed }">{{ task.text }}</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newFolderName: "",
      folders: [],
    };
  },
  methods: {
    addFolder() {
      if (this.newFolderName !== "") {
        this.folders.push({
          name: this.newFolderName,
          newTask: "",
          tasks: [],
        });
        this.newFolderName = "";
      }
    },
    addTask(folderIndex) {
      if (this.folders[folderIndex].newTask !== "") {
        this.folders[folderIndex].tasks.push({
          text: this.folders[folderIndex].newTask,
          completed: false,
        });
        this.folders[folderIndex].newTask = "";
      }
    },
  },
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
}

.folder-input {
  margin-bottom: 10px;
}

.folder {
  margin-bottom: 20px;
}

.task-input {
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.completed {
  text-decoration: line-through;
}
</style>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
