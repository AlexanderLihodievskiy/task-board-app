<template>
  <div class="app">
    <div class="desk">
      <PageHeader />
      <div class="desk__board">
        <TaskBoard class="task-board" :columns="columns" />
      </div>
    </div>
  </div>
</template>

<script setup>
import TaskBoard from './components/TaskBoard.vue'
import PageHeader from './components/PageHeader.vue'

const columns = [
  {
    id: 1,
    title: 'Колонка 1',
    tasks: [
      { id: 1, title: 'Задача 1', description: 'Описание задачи 1' },
      { id: 2, title: 'Задача 2', description: 'Описание задачи 2' }
    ]
  },
  {
    id: 2,
    title: 'Колонка 2',
    tasks: [
      { id: 3, title: 'Задача 3', description: 'Описание задачи 3' },
      { id: 4, title: 'Задача 4', description: 'Описание задачи 4' }
    ]
  }
]
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

html,
body {
  font-family: 'Poppins', sans-serif;
}

.app {
  background-color: #fff;
  color: #000;
  height: 100dvh;
  font-family: 'Poppins', sans-serif;
}

.desk {
  &__board {
    padding: 30px 0;
    height: calc(100dvh - 60px);
    overflow: hidden;
  }
}
</style>
