<template>
  <div class="flavours">
    <h1 class="title flavours__title">try different flavours</h1>
    <p class="flavours__subtitle">you have <span>3 attempts</span></p>
    <ul class="flavours__list">
      <li class="flavours__list-item" v-for="flavour in flavoursList" :key="flavour.id" ref="list">
        <FlavoursItem :image="flavour.image"/>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import FlavoursItem from "./FlavoursItem.vue";
import {Flavour} from "../../types/items";
import {v4} from "uuid";
import {onMounted, ref} from "vue";
import { spring, timeline} from "motion";
import {TimelineDefinition} from "@motionone/dom/types/timeline/types";


type EmitType = {
  /** Событие окончания демонстрации компонента*/
  (e: 'live-end'): void
}

const emits = defineEmits<EmitType>()
/** Элементы дерева списка вкусов */
const list = ref<HTMLElement[]>()
/** Задержка перед сменой баннера */
const delayBeforeChange = 4000

onMounted(async () => {
  /** Последовательность анимаций элементов дизайна */
  const sequence: TimelineDefinition = [
    [".flavours__title", {opacity: [0, 1]}, {duration: .5}],
    [".flavours__subtitle", {opacity: [0, 1]}, {duration: .4, at: 0.3}],
  ]
  if (list.value) {
    let debounce = 0
    for (const [index, listItem] of list.value?.entries()) {
      if (index % 2 === 0) debounce += 0.5
      sequence.push([listItem,
        {scale: [0.3, 1], opacity: [0, 1],},
        {
          at: debounce,
          easing: spring({
            restSpeed: 0.3,
            restDistance: 0.1,
            damping: 8,
            stiffness: 200
          })
        }])
    }
  }
  await timeline(sequence).finished
  setTimeout(async () => {
    await timeline(sequence, { direction: "reverse"}).finished
    emits('live-end')
  }, delayBeforeChange)
})

/** Список вкусов */
const flavoursList: Flavour[] = [
  {
    id: v4(),
    image: "/assets/images/honeyImage.png",
  },
  {
    id: v4(),
    image: "/assets/images/mintImage.png",
  },
  {
    id: v4(),
    image: "/assets/images/lemonImage.png",
  },
  {
    id: v4(),
    image: "/assets/images/honeyImage.png",
  },
  {
    id: v4(),
    image: "../../assets/images/lemonImage.png",
  },
  {
    id: v4(),
    image: "../../assets/images/mintImage.png",
  },
]
</script>

<style scoped lang="scss">
@use "@styles/variables" as *;

.flavours {
  padding: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;

  &__title {
    margin-top: 1rem;
  }

  &__list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 1.5rem;
    margin-top: 3rem;
  }

  &__subtitle {
    font-weight: 400;
    font-size: 1.6rem;
    line-height: 1.9rem;
    text-align: center;
    margin-top: 1rem;

    & > span {
      font-weight: bold;
    }
  }
}

</style>