<template>
  <div class="container">
    <h1>Yapılacaklar Listesi</h1>
    
    <!-- Yeni görev ekleme formu -->
    <div class="add-todo">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        placeholder="Yeni görev ekle..."
        type="text"
      >
      <button @click="addTodo">Ekle</button>
    </div>

    <!-- Görev listesi -->
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="index" :class="{ completed: todo.completed }">
        <input 
          type="checkbox" 
          v-model="todo.completed"
        >
        <span>{{ todo.text }}</span>
        <button @click="removeTodo(index)" class="delete-btn">Sil</button>
      </li>
    </ul>

    <!-- İstatistikler -->
    <div class="stats">
      <p>Toplam görev: {{ totalTodos }}</p>
      <p>Tamamlanan: {{ completedTodos }}</p>
      <p>Kalan: {{ remainingTodos }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  computed: {
    totalTodos() {
      return this.todos.length
    },
    completedTodos() {
      return this.todos.filter(todo => todo.completed).length
    },
    remainingTodos() {
      return this.totalTodos - this.completedTodos
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          text: this.newTodo,
          completed: false
        })
        this.newTodo = ''
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  font-size: 16px;
  cursor: pointer;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
}

button:hover {
  background-color: #45a049;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-list li {
  display: flex;
  align-items: center;
  padding: 10px;
  margin-bottom: 5px;
  background-color: #f9f9f9;
  border-radius: 4px;
  gap: 10px;
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: #888;
}

.delete-btn {
  background-color: #ff4444;
  margin-left: auto;
}

.delete-btn:hover {
  background-color: #cc0000;
}

.stats {
  margin-top: 20px;
  padding: 15px;
  background-color: #f0f0f0;
  border-radius: 4px;
}

.stats p {
  margin: 5px 0;
}
</style> 