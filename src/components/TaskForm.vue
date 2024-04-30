<template>
  <form @submit.prevent="submitForm">
    <label for="task-title">New Task:</label>
    <input id="task-title" v-model="newTaskTitle" type="text" required>
    <label for="column-id">Column:</label>
    <select id="column-id" v-model="newTaskColumnId" required>
      <option v-for="column in columns" :key="column.id" :value="column.id">
        {{ column.title }}
      </option>
    </select>
    <button type="submit">Add Task</button>
  </form>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

// Пропы
const props = defineProps({
  columns: Array
});

// Данные для новой задачи
const newTaskTitle = ref('');
const newTaskColumnId = ref(props.columns[0].id);

// Определение событий
const emit = defineEmits(['submit']);

// Метод для отправки формы
const submitForm = () => {
  emit('submit', { title: newTaskTitle.value, columnId: newTaskColumnId.value });
  newTaskTitle.value = '';
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  height: 100vh;
  padding-top: 20px;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f5f5f5;
  padding: 10px;
  border-radius: 10px;
  width: 80%;
  max-width: 300px;
}

label {
  font-size: 14px;
  font-weight: bold;
  margin-top: 5px;
}

input, select {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-top: 5px;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  background-color: #4caf50;
  color: white;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  transition: filter 0.3s ease;
}

button:hover {
  filter: brightness(0.8);
}
</style>