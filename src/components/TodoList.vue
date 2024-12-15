<template>
    <div class="todo-list-container">
      <!-- Форма для добавления новой задачи -->
      <form @submit.prevent="addNewTask" class="todo-form">
        <input v-model="newTaskInput" placeholder="Введите новую задачу" class="todo-input" />
        <button type="submit" class="todo-button">Добавить</button>
      </form>
      <!-- Список задач -->
      <ul class="todo-list">
        <TodoItem 
          v-for="task in tasks" 
          :key="task.id" 
          :task="task"
          @remove-task="$emit('remove-task', $event)"
          @toggle-completion="$emit('toggle-completion', $event)"
        />
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import TodoItem from './TodoItem.vue';
  
  export default {
    name: 'TodoList',
    components: { TodoItem },
    props: ['tasks'], // Получение списка задач от родительского компонента
    emits: ['add-task', 'remove-task', 'toggle-completion'], // Объявление событий
    setup(_, { emit }) {
      // Поле ввода новой задачи
      const newTaskInput = ref('');
  
      // Метод добавления новой задачи
      const addNewTask = () => {
        if (newTaskInput.value.trim() !== '') {
          emit('add-task', newTaskInput.value);
          newTaskInput.value = ''; // Очистка поля ввода
        }
      };
  
      return { newTaskInput, addNewTask };
    }
  };
  </script>
  
  <style scoped>
  /* Контейнер для списка задач */
  .todo-list-container {
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  /* Форма для добавления задач */
  .todo-form {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
  }
  
  .todo-input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  .todo-button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .todo-button:hover {
    background-color: #45a049;
  }
  
  /* Список задач */
  .todo-list {
    list-style: none;
    padding: 0;
  }
  </style>