<template>
  <div class="task-column">
    <!-- <h2>{{ column.title }}</h2> -->
    <ColumnLabel @remove="remove">{{ column.title }}</ColumnLabel>
    <VueDraggableNext
      class="task-column__tasks"
      :list="column.tasks"
      :group="{ name: 'tasks' }"
      @end="onEnd"
    >
      <TaskCard
        v-for="task in column.tasks"
        :key="task.id"
        :task="task"
        @remove-task="removeTask"
        @edit-task="editTask"
      />
    </VueDraggableNext>
    <AddTaskButton @click="addTask('New Task')">Add Task</AddTaskButton>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
import TaskCard from './TaskCard.vue'
import ColumnLabel from './ColumnLabel.vue'
import AddTaskButton from './AddTaskButton.vue'
import { VueDraggableNext } from 'vue-draggable-next'

// Пропы
const props = defineProps({
  column: Object
})

// Определение событий
const emit = defineEmits(['add-task', 'remove-task', 'remove', 'edit-task', 'update:column'])

// Метод для добавления новой задачи
const addTask = (title) => {
  const newTask = { id: Date.now(), title }
  emit('add-task', { columnId: props.column.id, task: newTask })
}

// Метод для обработки окончания перетаскивания
const onEnd = () => {
  emit('update:column', props.column)
}

// Метод для удаления задачи
const removeTask = (id) => {
  emit('remove-task', { columnId: props.column.id, taskId: id })
}

// Метод для удаления колонки
const remove = () => {
  emit('remove', props.column.id)
}

// Метод для редактирования задачи
const editTask = (taskId, newTaskData) => {
  emit('edit-task', { columnId: props.column.id, taskId, newTaskData })
}
</script>

<style lang="scss" scoped>
.task-column {
  display: flex;
  flex-direction: column;
  gap: 10px;
  min-width: calc(100vw - 60px);

  @media screen and (min-width: 512px) {
    min-width: 362px;
  }

  &__tasks {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
}
</style>
