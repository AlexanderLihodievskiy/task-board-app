<template>
  <div class="task-card">
    <div class="task-card__actions">
      <button class="task-card__actions-button" @click="editTask">Edit</button>
      <button class="task-card__actions-button" @click="removeTask">Remove</button>
    </div>
    <div class="task-card__labels">
      <span class="task-card__labels-item" v-for="n in 4" :key="n"></span>
    </div>
    <h3 class="task-card__title">{{ task.title }}</h3>
    <p class="task-card__desc">{{ task.description }}</p>
    <div class="task-card__info">
      <button type="button" class="task-card__info-add">
        <SvgIconAdd />
      </button>
      <div class="task-card__info-actions">
        <button type="button" class="task-card__info-button">
          <span class="task-card__info-number">15</span>
          <SvgIconComments class="task-card__info-icon" />
        </button>
        <button type="button" class="task-card__info-button">
          <span class="task-card__info-number">456</span>
          <SvgIconLikes class="task-card__info-icon" />
        </button>
        <button type="button" class="task-card__info-button">
          <span class="task-card__info-number">4</span>
          <SvgIconFile class="task-card__info-icon" />
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
import SvgIconAdd from '../assets/svg/i-add.svg?component'
import SvgIconComments from '../assets/svg/i-comments.svg?component'
import SvgIconLikes from '../assets/svg/i-likes.svg?component'
import SvgIconFile from '../assets/svg/i-file.svg?component'

// Пропы
const props = defineProps({
  task: Object
})

// Определение событий
const emit = defineEmits(['edit-task', 'remove-task'])

// Метод для редактирования задачи
const editTask = () => {
  emit('edit-task', props.task.id)
}

// Метод для удаления задачи
const removeTask = () => {
  emit('remove-task', props.task.id)
}
</script>

<style lang="scss">
.task-card {
  background-color: #f4f4f4;
  border-radius: 10px;
  padding: 20px;

  &__actions {
    display: flex;
    align-items: center;
    gap: 5px;
    justify-content: space-between;

    &-button {
      background: transparent;
      border: initial;
      padding: 0;
      font-size: 14px;
      line-height: 18px;
      cursor: pointer;

      &:hover {
        text-decoration: underline;
      }
    }
  }

  &__labels {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-top: 10px;

    &-item {
      width: 100%;
      max-width: 60px;
      height: 8px;
      border-radius: 4px;

      &:nth-of-type(1) {
        background-color: #1ad698;
      }
      &:nth-of-type(2) {
        background-color: #ff3838;
      }
      &:nth-of-type(3) {
        background-color: #891be8;
      }
      &:nth-of-type(4) {
        background-color: #4339f2;
      }
    }
  }
  &__title {
    font-size: 16px;
    margin-top: 11px;
    line-height: 24px;
  }

  &__desc {
    font-size: 13px;
    line-height: 19px;
    font-weight: 300;
    margin-top: 2px;
    opacity: 0.4;
  }

  &__info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 5px;
    margin-top: 26px;

    &-add {
      background: transparent;
      padding: 0;
      border: initial;
      cursor: pointer;
      
      svg {
        width: 30px;
        height: 30px
      }
    }

    &-actions {
      display: flex;
      align-items: center;
      gap: 18px;
    }

    &-button {
      display: flex;
      align-items: center;
      gap: 2px;
      background: transparent;
      border: initial;
      padding: 0;
      cursor: pointer;
    }

    &-number {
      font-size: 14px;
      line-height: 21px;
      opacity: 0.2;
    }

    &-icon {
      flex-shrink: 0;
      width: 20px;
      height: 20px;
    }
  }
}
</style>
