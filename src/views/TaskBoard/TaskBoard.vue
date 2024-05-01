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

    <TaskModal
      v-if="isModalOpen"
      :task="taskToEdit"
      :isOpen="isModalOpen"
      @closeModal="closeModal"
      @addTask="addOrUpdateTaskAndCloseModal"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import TaskColumn from './components/TaskColumn.vue'
import TaskModal from './components/TaskModal.vue'
import TaskBoardHeader from './components/TaskBoardHeader.vue'
import simplebar from 'simplebar-vue'

let initialColumns = [
  { id: 1, title: 'Design', tasks: [] },
  { id: 2, title: 'Prototype', tasks: [] },
  { id: 3, title: 'Trello', tasks: [] },
  { id: 4, title: 'Test', tasks: [] },
  { id: 5, title: 'Final', tasks: [] }
]

try {
  const savedColumns = localStorage.getItem('columns')
  if (savedColumns) {
    initialColumns = JSON.parse(savedColumns)
  }
} catch (error) {
  console.error('Failed to parse columns from localStorage', error)
}

const columns = ref(initialColumns)

const isModalOpen = ref(false)
const currentColumnId = ref(null)
const taskToEdit = ref(null)

const updateColumn = (updatedColumn) => {
  const index = columns.value.findIndex((column) => column.id === updatedColumn.id)
  if (index !== -1) {
    columns.value[index] = updatedColumn
  }
}

const addOrUpdateTaskAndCloseModal = (task) => {
  if (task.id) {
    const column = columns.value.find((column) => column.tasks.find((t) => t.id === task.id))
    const taskToUpdate = column.tasks.find((t) => t.id === task.id)
    taskToUpdate.title = task.title
    taskToUpdate.description = task.description
  } else {
    const id =
      Math.max(...columns.value.flatMap((column) => column.tasks.map((task) => task.id)), 0) + 1
    task.id = id
    const column = columns.value.find((column) => column.id === currentColumnId.value)
    column.tasks.push(task)
  }

  closeModal()
}

watch(
  columns,
  () => {
    localStorage.setItem('columns', JSON.stringify(columns.value))
  },
  { deep: true }
)

onMounted(() => {
  try {
    const savedColumns = localStorage.getItem('columns')
    if (savedColumns) {
      columns.value = JSON.parse(savedColumns)
    }
  } catch (error) {
    console.error('Failed to parse columns from localStorage', error)
  }
})

const closeModal = () => {
  isModalOpen.value = false
  taskToEdit.value = null
}

const openModal = (columnId) => {
  currentColumnId.value = columnId
  isModalOpen.value = true
}

const editTask = ({ columnId, taskId }) => {
  const column = columns.value.find((column) => column.id === columnId)
  if (column) {
    const task = column.tasks.find((task) => task.id === taskId)
    if (task) {
      taskToEdit.value = task
      isModalOpen.value = true
    }
  }
}


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
