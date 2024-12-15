<template>
  <div id="app" class="app-container">
    <!-- Основной заголовок приложения -->
    <h1 class="app-title">To-Do list Vue3</h1>
    <!-- Компонент списка задач с привязкой данных и событий -->
    <TodoList 
      :tasks="tasks" 
      @add-task="addTask" 
      @remove-task="removeTask" 
      @toggle-completion="toggleTaskCompletion"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: { TodoList },
  setup() {
    // Список задач - реактивная переменная
    const tasks = ref([]);

    // Метод добавления новой задачи
    const addTask = (newTask) => {
      tasks.value.push({
        id: Date.now(), // Уникальный идентификатор задачи
        text: newTask, // Текст задачи
        completed: false // Статус выполнения задачи
      });
    };

    // Метод удаления задачи по id
    const removeTask = (taskId) => {
      tasks.value = tasks.value.filter(task => task.id !== taskId);
    };

    // Метод переключения статуса выполнения задачи
    const toggleTaskCompletion = (task) => {
      task.completed = !task.completed;
    };

    // Возвращаем реактивные переменные и методы для использования в шаблоне
    return { tasks, addTask, removeTask, toggleTaskCompletion };
  }
};
</script>

<style scoped>
/* Стили для главного контейнера приложения */
.app-container {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin: 40px auto;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.app-title {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 20px;
}
</style>
