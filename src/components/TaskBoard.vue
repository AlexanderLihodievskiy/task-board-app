<template>
  <div class="task-board">
    <div class="task-board__top">
      <TaskBoardHeader />
    </div>
    <simplebar class="task-board__content">
      <div class="task-board__content-columns">
        <div
          v-for="(column, index) in columns"
          :key="column.id"
          :class="['task-board__content-item', { last: index === columns.length - 1 }]"
        >
          <TaskColumn
            :column="column"
            @remove="removeColumn"
            @add-task="() => openModal(column.id)"
            @remove-task="removeTask"
            @edit-task="editTask"
            @update:column="updateColumn"
          />
        </div>
      </div>
    </simplebar>

    <!-- <button class="add-column-button" @click="addColumn('New Column')">Add Column</button> -->
    <TaskModal :isOpen="isModalOpen" @closeModal="closeModal" @addTask="addTaskAndCloseModal" />
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import TaskColumn from './TaskColumn.vue'
import TaskModal from './TaskModal.vue'
import TaskBoardHeader from './TaskBoardHeader.vue'
import simplebar from 'simplebar-vue'

// Состояние
const columns = ref(JSON.parse(localStorage.getItem('columns')) || [
  { id: 1, title: 'Design', tasks: [] },
  { id: 2, title: 'Prototype', tasks: [] },
  { id: 3, title: 'Trello', tasks: [] },
  { id: 4, title: 'Test', tasks: [] },
  { id: 5, title: 'Final', tasks: [] }
]);

const isModalOpen = ref(false)
const currentColumnId = ref(null)

const updateColumn = (updatedColumn) => {
  const index = columns.value.findIndex(column => column.id === updatedColumn.id)
  if (index !== -1) {
    columns.value[index] = updatedColumn
  }
}

const addTask = ({ title, description, columnId }) => {
  const column = columns.value.find((column) => column.id === columnId)
  if (column) {
    const newTask = { id: Date.now(), title, description }
    column.tasks.push(newTask)
  }
}

// Следим за изменениями в состоянии и сохраняем их в localStorage
watch(
  columns,
  () => {
    localStorage.setItem('columns', JSON.stringify(columns.value))
  },
  { deep: true }
)

// Восстанавливаем состояние при монтировании компонента
onMounted(() => {
  const savedColumns = localStorage.getItem('columns');
  if (savedColumns) {
    columns.value = JSON.parse(savedColumns);
  }
});

const closeModal = () => {
  isModalOpen.value = false
}

const addTaskAndCloseModal = (task) => {
  addTask({ ...task, columnId: currentColumnId.value })
  closeModal()
}

const openModal = (columnId) => {
  currentColumnId.value = columnId
  isModalOpen.value = true
}

// Метод для редактирования задачи
const editTask = ({ columnId, taskId, newTaskData }) => {
  console.log('EDIT')
  const column = columns.value.find((column) => column.id === columnId)
  if (column) {
    const task = column.tasks.find((task) => task.id === taskId)
    if (task) {
      Object.assign(task, newTaskData)
    }
  }
}

// // Метод для добавления новой колонки
// const addColumn = (title) => {
//   const newColumn = { id: Date.now(), title, tasks: [] }
//   columns.value.push(newColumn)
// }

// Метод для удаления колонки
const removeColumn = (id) => {
  const index = columns.value.findIndex((column) => column.id === id)
  if (index !== -1) {
    columns.value.splice(index, 1)
  }
}

const removeTask = ({ columnId, taskId }) => {
  const column = columns.value.find((column) => column.id === columnId)
  if (column) {
    const taskIndex = column.tasks.findIndex((task) => task.id === taskId)
    if (taskIndex !== -1) {
      column.tasks.splice(taskIndex, 1)
    }
  }
}
</script>

<style lang="scss" scoped>
.task-board {
  &__top {
    margin-bottom: 15px;
  }

  &__content {
    padding: 20px 0;
    width: 100%;
    height: calc(100dvh - 60px - 40px - 15px - 89px);

    &-item {
      &.last {
        padding-right: 30px;
      }
    }

    &-columns {
      display: flex;
      gap: 30px;
      height: 100%;
      padding-left: 30px;
    }
  }
}
</style>
