<template>
  <div class="todo-list">
    <h1>To Do List</h1>
    <input type="text"
           placeholder="Add a task..."
           v-model="newTaskForList"
           @keyup.enter="addTask()"/>
    <button
        type="button"
        @click="addTask()"
    >Add
    </button>
    <ol>
      <li v-for="(task, index) in tasksList" :key="index">
        <input class="check-box" type="checkbox" v-model="task.completed" />
        <span :class="{completed: task.completed}">{{ task.text }}</span>
        <button class="delete-button" @click="deleteTask(index)">Delete</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',
  data() {
    return {
      tasksList: [],
      newTaskForList: '',
    }
  },
  methods: {
    addTask() {
      if (this.newTaskForList !== '') {
        this.tasksList.push({text: this.newTaskForList, completed: false})
        this.newTaskForList = '';
      }
    },
    deleteTask(index) {
      this.tasksList.splice(index, 1)
    }
  },
}
</script>

<style scoped>
body {
  background: hsl(0, 0%, 31%);
}

button {
  margin: 10px;
  align-items: center;
  font-size: 1rem;
  font-weight: bold;
  border: none;
  padding: 10px;
  background-color: aquamarine;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.5s;
}

input[type="text"] {
  font-size: 1.2rem;
  padding: 10px;
  border: 2px solid hsla(0, 0%, 80%, 0.5);
  border-radius: 5px;
  color: black;
}

.check-box {
  height: 20px;
  width: 20px;
}

.check-box:checked {
  accent-color: aquamarine;
}

.delete-button {
  background: #a00;
  color: #fff;
  padding: 4px 10px;
  border-radius: 3px;
  margin-left: 10px;
}

ol {
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  gap: 16px;
  justify-content: space-between;
  list-style: none;
  font-size: 1.5rem;
  font-weight: bold;
  background: hsl(0, 0%, 95%);
  margin-bottom: 10px;
  border: 2px solid hsla(0, 0%, 85%, 0.75);
  border-radius: 5px;
}

li span {
  flex: 1;
  word-break: break-word;
}

.completed {
  text-decoration: line-through;
  color: #aaa;
  opacity: 0.7;
}
</style>
