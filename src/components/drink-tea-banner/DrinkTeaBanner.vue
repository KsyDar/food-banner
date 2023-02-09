<template>
  <div class="drink-tea">
    <h1 class="title drink-tea__title">Try refreshing</h1>
    <p class="title drink-tea__subtitle">ready-to-drink tea</p>
    <button
        class="drink-tea__button"
        @mouseenter="buttonHover"
        @mouseleave="buttonLeave"
        @click="goToGoogle"
    >
      Buy
    </button>
    <div class="drink-tea__images">
      <div class="drink-tea__images-item drink-tea__images-item--waves">
        <img alt="" src="../../assets/images/wavesImage.png">
      </div>
      <div class="drink-tea__images-item drink-tea__images-item--honey">
        <img alt="" src="../../assets/images/cutHoneyImage.png">
      </div>
      <div class="drink-tea__images-item drink-tea__images-item--mint">
        <img alt="" src="../../assets/images/plusMintImage.png">
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import {animate, AnimationControls, spring, timeline} from "motion";
import {onMounted} from "vue";
import {TimelineDefinition} from "@motionone/dom/types/timeline/types";

/** Контрол анимации кнопки */
let buttonAnimation: AnimationControls | null = null;

onMounted(() => {
  /** Бесконечная анимация кнопки */
  buttonAnimation = animate(".drink-tea__button",
      {scale: [ 0.9, 1.1, 0.9]},
      {
        repeat: Infinity,
        duration: 1,
        easing: "ease-in-out",
      }
  )
  /**
   * Последовательность анимаций элементов дизайна
   */
  const sequence: TimelineDefinition = [
    [".drink-tea__title", {opacity: [0, 1], translate: [-100, 0]}, {duration: 1}],
    [".drink-tea__subtitle", {opacity: [0, 1], translate: [100, 0]}, {duration: 1, at: 0.3}],
    [".drink-tea__images-item--mint", {opacity: [0, 1], translate: [100, 0], rotate: [180, 0]}, {
      at: 0.5,
      easing: spring({
        damping: 7,
      })
    }],
    [".drink-tea__images-item--waves",
      {
        opacity: [0, 1],
        x: [-50, -2],
        y: [50, 2]
      }, {
      at: 0.5,
      easing: spring({
        damping: 11,
        stiffness: 70
      })
    }],
    [".drink-tea__images-item--honey", {opacity: [0, 1], translate: [100, 0], rotate: [180, 0]}, {
      at: 0.9,
      easing: spring({
        damping: 7,
      })
    }],
    [".drink-tea__button", {opacity: [0, 1]}, {duration: 0.5, at: 1.7}],
  ]

  timeline(sequence)

})

/** Функция для остановки анимации кнопки, срабатывает при наведении курсора на кнопку */
const buttonHover = () => {
  if (buttonAnimation) {
    buttonAnimation.pause()
  }
}

/** Функция для возобновления анимации кнопки, срабатывает при отведении курсора с кнопки */
const buttonLeave = () => {
  if (buttonAnimation) {
    buttonAnimation.play()
  }
}

/** Переход по ссылке */
const goToGoogle = () => {
  window.open("https://www.google.com", "_blank")
}

</script>

<style scoped lang="scss">
@use "@styles/variables" as *;

.drink-tea {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 100%;
  position: relative;

  &__title {
    font-size: 3.5rem;
    margin: 4rem 2rem 0 2rem;

  }

  &__subtitle {
    font-size: 2.7rem;
    margin: 0 2rem 1.6rem 2rem;
  }

  &__button {
    color: $main-font-color;
    text-transform: uppercase;
    font-family: $main-font-family;
    font-style: italic;
    font-weight: 700;
    font-size: 2.6rem;
    line-height: 3.1rem;
    display: flex;
    align-items: center;
    text-align: center;
    padding: 0.5rem 5.1rem;
    background: linear-gradient(180deg, #F1F9B7 0%, #C6EC9E 100%);
    border: 0.1rem solid #FFFFFF;
    border-radius: 3.3rem;

    &[style*="opacity: 1"] {
      cursor: pointer;
    }
  }

  &__images {
    width: 100%;
    height: 100%;

    &-item {
      position: absolute;

      &--waves {
        bottom: -3px;
        z-index: 1000;
      }

      &--honey {
        width: 150px;
        bottom: -3px;
        left: 46%;
      }

      &--mint {
        width: 110px;
        right: 0;
        top: 35%;
      }
    }
  }
}
</style>