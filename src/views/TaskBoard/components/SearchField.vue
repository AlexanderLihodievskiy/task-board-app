<template>
  <div class="search-field">
    <input type="text" class="search-field__input" placeholder="Search" />
    <button class="search-field__button">
      <SvgSearch />
    </button>
  </div>
</template>

<script setup>
import SvgSearch from '../../../assets/svg/i-search.svg?component'
</script>

<style lang="scss" scoped>
.search-field {
  display: flex;
  align-items: center;
  background: #f4f4f4;
  border-radius: 25px;
  overflow: hidden;
  padding: 0 15px;
  height: 30px;

  &__input {
    border: none;
    background: none;
    width: 100%;
    height: 100%;
    font-size: 13px;
    outline: none;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
  }

  &__button {
    width: 16px;
    height: 16px;
    padding: 0;
    background: transparent;
    border: initial;
    cursor: pointer;

    svg {
      width: 100%;
      height: 100%;
    }
  }
}
</style>
