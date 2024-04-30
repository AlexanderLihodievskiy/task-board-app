<template>
  <header class="page-header">
    <div class="page-header__left">
      <a href="#" class="page-header__logo">
        <SvgLogo />
      </a>
      <span class="page-header__divider"></span>
      <div class="page-header__boards">
        <SvgBoards />
        <span>Boards</span>
      </div>
      <span class="page-header__divider"></span>
      <div class="page-header__search desktop">
        <SearchField />
      </div>
      <div class="page-header__search mobile">
        <button type="button">
          <SvgSearch />
        </button>
      </div>
    </div>
    <div class="page-header__right">
      <div class="page-header__actions">
        <button class="page-header__actions-button">
          <SvgPlus />
        </button>
        <button class="page-header__actions-button">
          <SvgAlert />
        </button>
        <button class="page-header__actions-button">
          <SvgBell />
        </button>
      </div>
      <div class="page-header__avatar">
        <img :src="imgAvatar" alt="Avatar" />
      </div>
    </div>
  </header>
</template>

<script setup>
import SvgLogo from '../assets/svg/logo.svg?component'
import SvgBoards from '../assets/svg/i-boards.svg?component'
import SearchField from './SearchField.vue'
import SvgPlus from '../assets/svg/i-plus.svg?component'
import SvgAlert from '../assets/svg/i-alert.svg?component'
import SvgBell from '../assets/svg/i-bell.svg?component'
import SvgSearch from '../assets/svg/i-search.svg?component'
import imgAvatar from '../assets/img/avatar.png'
</script>

<style lang="scss" scoped>
.page-header {
  display: flex;
  align-items: center;
  padding: 14px 30px;
  width: 100%;
  border-bottom: 1px solid rgba($color: #000000, $alpha: 0.2);

  &__logo {
    display: none;

    @media screen and (min-width: 992px) {
      height: 30px;
      display: block;
    }

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }

  &__left {
    display: flex;
    align-items: center;
    gap: 20px;
    height: 32px;
    width: 100%;
    max-width: 760px;
  }

  &__boards {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 16px;
    line-height: 24px;

    span {
      display: none;

      @media screen and (min-width: 992px) {
        display: block;
      }
    }

    svg {
      width: 30px;
      height: 30px;
      background: #f4f4f4;

      @media screen and (min-width: 992px) {
        width: 24px;
        height: 24px;
      }
    }
  }

  &__divider {
    display: none;

    @media screen and (min-width: 992px) {
      height: 100%;
      width: 1px;
      background-color: #000;
      opacity: 0.2;
      flex-shrink: 0;
      display: block;
    }
  }

  &__search {
    &.desktop {
      display: none;

      @media screen and (min-width: 992px) {
        width: 100%;
        max-width: 300px;
        display: block;
      }

      @media screen and (min-width: 1024px) {
        max-width: none;
      }
    }

    &.mobile {
      display: block;

      @media screen and (min-width: 992px) {
        display: none;
      }

      button {
        width: 20px;
        height: 20px;
        border: initial;
        background: transparent;
        padding: 0;
        cursor: pointer;
        opacity: 0.2;

        svg {
          width: 100%;
          height: 100%;
        }
      }
    }
  }

  &__right {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-left: auto;

    @media screen and (min-width: 992px) {
      gap: 30px;
    }
  }

  &__actions {
    display: flex;
    align-items: center;
    gap: 10px;

    @media screen and (min-width: 992px) {
      gap: 30px;
    }

    &-button {
      width: 20px;
      height: 20px;
      border: initial;
      background: transparent;
      padding: 0;
      cursor: pointer;

      svg {
        width: 100%;
        height: 100%;
      }
    }
  }

  &__avatar {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    overflow: hidden;

    @media screen and (min-width: 992px) {
      width: 40px;
      height: 40px;
    }

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}
</style>