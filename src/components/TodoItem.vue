<template>
    <li :class="{ completed: task.completed }" class="todo-item">
      <!-- Текст задачи с возможностью переключения статуса -->
      <span @click="$emit('toggle-completion', task)" class="task-text">
        {{ task.text }}
      </span>
      <!-- Кнопка удаления задачи -->
      <button @click="$emit('remove-task', task.id)" class="remove-button">Удалить</button>
    </li>
  </template>
  
  <script>
  export default {
    name: 'TodoItem',
    props: ['task'], // Получение данных задачи
    emits: ['toggle-completion', 'remove-task'] // Объявление событий для родителя
  };
  </script>
  
  <style scoped>
  /* Контейнер для элемента списка задач */
  .todo-item {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  /* Стили для завершенной задачи */
  .completed .task-text {
    text-decoration: line-through;
    color: #aaa;
  }
  
  .task-text {
    cursor: pointer;
    flex: 1;
  }
  
  /* Кнопка удаления задачи */
  .remove-button {
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 5px 10px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .remove-button:hover {
    background-color: #e53935;
  }
  </style>
  