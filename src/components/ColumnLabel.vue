<template>
  <div class="column-label">
    <h2 class="column-label__title">
      <slot></slot>
    </h2>
    <div class="column-label__actions">
      <button class="column-label__context">
        <SvgImage />
      </button>
      <button class="column-label__remove" @click="$emit('remove')">
        <SvgRemoveColumn />
      </button>
    </div>
  </div>
</template>

<script setup>
import SvgImage from '../assets/svg/i-dots.svg?component'
import SvgRemoveColumn from '../assets/svg/i-close.svg?component'
</script>

<style lang="scss" scoped>
.column-label {
  background-color: #f4f4f4;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 5px;
  padding: 14px 15px;

  &__title {
    color: #000000;
    font-size: 16px;
    font-weight: 500;
  }

  &__actions {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  &__context {
    display: flex;
    align-items: center;
    justify-content: center;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    flex-shrink: 0;
    width: 24px;
    height: 6px;

    svg {
      width: 100%;
      height: 100%;
    }
  }

  &__remove {
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    width: 18px;
    height: 18px;
    color: rgba($color: #000000, $alpha: 0.2);

    svg {
      width: 100%;
      height: 100%;
    }
  }
}
</style>
