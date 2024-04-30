<template>
  <button class="add-task-button" type="button" @click="$emit('click')">
      + Add new card
  </button>
</template>

<script setup>

</script>

<style lang="scss" scoped>
  .add-task-button {
    width: 100%;
    height: 160px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px dashed rgba($color: #000000, $alpha: 0.2);
    background: transparent;
    font-size: 16px;
    line-height: 24px;
    cursor: pointer;
  }
</style>