<template>
  <div id="app">
    <div class="todo-container">
      <h1>To Do List</h1>
      <div class="input-container">
        <input
          v-model="newTask"
          type="text"
          placeholder="Enter a new task"
          @keyup.enter="addTask"
        />
        <button @click="addTask">Add</button>
      </div>
      <div class="task-list">
        <div v-for="task in tasks" :key="task.id" class="task-item">
          <span class="task-text" :class="{ completed: task.completed }">{{ task.text }}</span>
          <button class="done-btn" @click="markAsDone(task.id)">
            {{ task.completed ? '✓' : 'Done' }}
          </button>
        </div>
        <div v-if="tasks.length === 0" class="empty-state">No tasks yet. Add your first task!</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: [],
    }
  },
  components: {
    // Register your components here
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({
          id: Date.now(),
          text: this.newTask,
          completed: false,
        })
        this.newTask = ''
      }
    },
    markAsDone(taskId) {
      const task = this.tasks.find((t) => t.id === taskId)
      if (task) {
        task.completed = !task.completed
      }
    },
  },
  computed: {
    // Your computed properties go here
  },
  mounted() {
    // Lifecycle hook when component is mounted
  },
}
</script>

<style lang="less">
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;

  .todo-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;

    h1 {
      text-align: center;
      color: #2c3e50;
      width: 100%;
      margin-bottom: 20px;
    }

    .input-container {
      display: grid;
      grid-template-columns: 1fr 80px;
      gap: 10px;
      margin-bottom: 20px;
      width: 100%;
      max-width: 500px;

      input {
        padding: 8px 12px;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 16px;
        width: 100%;

        &:focus {
          outline: none;
          border-color: #42b983;
        }
      }

      button {
        padding: 8px 16px;
        background-color: #42b983;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
        width: 80px;

        &:hover {
          opacity: 0.8;
        }
      }
    }

    .task-list {
      width: 100%;
      max-width: 500px;

      .task-item {
        display: grid;
        grid-template-columns: 1fr 80px;
        gap: 10px;
        margin-bottom: 8px;
        width: 100%;

        .task-text {
          font-size: 16px;
          color: white;
          padding: 8px 0;
          &.completed {
            text-decoration: line-through;
            opacity: 0.7;
          }
        }

        .done-btn {
          padding: 0;
          background-color: gray;
          color: white;
          border: none;
          border-radius: 4px;
          cursor: pointer;
          font-size: 10px;
          width: 80px;

          &:hover {
            opacity: 0.8;
          }
        }
      }

      .empty-state {
        text-align: center;
        color: #6c757d;
        padding: 20px;
        font-style: italic;
      }
    }
  }
}
</style>
