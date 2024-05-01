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
import TaskBoard from './views/TaskBoard/TaskBoard.vue'
import PageHeader from './views/TaskBoard/components/PageHeader.vue'

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
    height: calc(100dvh - 69px);
    overflow: hidden;
  }
}
</style>
