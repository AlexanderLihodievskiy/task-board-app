<template>
  <transition name="modal">
    <div class="modal-overlay" v-show="isOpen" @click="closeModal">
      <div class="modal-content" @click.stop>
        <div class="input-group" :class="{ error: titleError }">
          <label for="task-title">Title:</label>
          <input id="task-title" v-model="title" type="text" @input="titleError = false" />
          <p class="error-message" v-if="titleError">
            Необходимо ввести данные перед добавлением задачи
          </p>
        </div>
        <div class="input-group" :class="{ error: descriptionError }">
          <label for="task-description">Description:</label>
          <textarea id="task-description" v-model="description" @input="descriptionError = false"></textarea>
          <p class="error-message" v-if="descriptionError">
            Необходимо ввести данные перед добавлением задачи
          </p>
        </div>
        <div class="button-group">
          <button class="button save" @click="saveTask">Save</button>
          <button class="button cancel" @click="closeModal">Cancel</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, defineProps, defineEmits, toRefs } from 'vue'

const props = defineProps({
  isOpen: Boolean
})

const emit = defineEmits(['closeModal', 'addTask'])

const { isOpen } = toRefs(props)
const title = ref('')
const description = ref('')
const titleError = ref(false)
const descriptionError = ref(false)

const saveTask = () => {
  titleError.value = !title.value
  descriptionError.value = !description.value

  if (titleError.value || descriptionError.value) {
    return
  }

  emit('addTask', { title: title.value, description: description.value })
  closeModal()
}

const closeModal = () => {
  title.value = ''
  description.value = ''
  titleError.value = false
  descriptionError.value = false
  emit('closeModal')
}
</script>

<style lang="scss" scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  width: 80%;
  max-width: 500px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.input-group {
  display: flex;
  flex-direction: column;
}

.input-group label {
  color: #000;
}

.input-group input,
.input-group textarea {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-top: 5px;
}

.input-group textarea {
  resize: vertical;
}

.button-group {
  display: flex;
  justify-content: space-between;
}

.button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  transition: filter 0.3s ease;
}

.button:hover {
  filter: brightness(0.8);
}

.button.save {
  background-color: #4caf50;
  color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.26);
}

.button.cancel {
  background-color: #f44336;
  color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.26);
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.1s;
}

.error {
  border-color: red;
}

.error-message {
  color: red;
}
</style>
