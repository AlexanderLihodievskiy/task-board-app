<template>
  <section class="task-board-header">
    <h1 class="task-board-header__title">Brackets</h1>
    <div class="task-board-header__right">
      <div class="task-board-header__actions">
        <button class="task-board-header__actions-button">
          <SvgIconLikes />
        </button>
        <span class="task-board-header__actions-divider"></span>
        <button class="task-board-header__actions-button">
          <SvgIconGlobe />
          <span>Public</span>
        </button>
        <span class="task-board-header__actions-divider"></span>
        <button class="task-board-header__actions-button">
          <SvgIconHard />
        </button>
      </div>
      <div class="task-board-header__users">
        <img :src="usersImg" alt="Users" />
      </div>
      <p class="task-board-header__menu">Menu</p>
    </div>
  </section>
</template>

<script setup>
import SvgIconLikes from '../../../assets/svg/i-likes.svg?component'
import SvgIconGlobe from '../../../assets/svg/i-globe.svg?component'
import SvgIconHard from '../../../assets/svg/i-hard.svg?component'
import usersImg from '../../../assets/img/users.png'
</script>

<style lang="scss" scoped>
.task-board-header {
  display: flex;
  padding: 0 30px;
  flex-direction: column;

  @media screen and (min-width: 992px) {
    align-items: center;
    flex-direction: row;
  }

  &__title {
    font-size: 16px;
    line-height: 24px;
    font-weight: 500;

    @media screen and (min-width: 992px) {
      font-size: 26px;
      line-height: 39px;
    }
  }

  &__right {
    display: flex;
    align-items: center;
    margin-left: auto;
    width: 100%;
  }

  &__actions {
    display: flex;
    align-items: center;
    height: 35px;
    gap: 5px;

    @media screen and (min-width: 992px) {
      gap: 10px;
      margin-left: 90px;
    }

    &-divider {
      height: 100%;
      width: 1px;
      background-color: #000;
      opacity: 0.1;
    }

    &-button {
      background: transparent;
      border: initial;
      padding: 0;
      display: flex;
      align-items: center;
      font-size: 16px;
      line-height: 24px;
      gap: 4px;

      @media screen and (min-width: 992px) {
        font-size: 18px;
        line-height: 27px;
      }

      svg {
        width: 20px;
        height: 20px;
      }

      span {
        opacity: 0.1;
      }
    }
  }

  &__users {
    height: 30px;
    margin-left: auto;

    @media screen and (min-width: 992px) {
      height: 40px;
    }

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
    }
  }

  &__menu {
    font-size: 16px;
    line-height: 24px;
    margin-left: 10px;

    @media screen and (min-width: 992px) {
      font-size: 20px;
      line-height: 30px;
      margin-left: 100px;
    }
  }
}
</style>
