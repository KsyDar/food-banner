<template>
<div class="flavour-item">
  <img alt="" :src="image">
</div>
</template>

<script setup lang="ts">
type PropType = {
  /** Изображение вкуса */
  image: string;
}

defineProps<PropType>();
</script>

<style scoped lang="scss">
.flavour-item {
  width: 115px;
  height: 115px;
  background: linear-gradient(186.15deg, #F7FABA 0.42%, #C5EB9D 63.56%);
  border: 0.1rem solid #FFFFFF;
  border-radius: 2.8rem;
  padding: 1.3rem;
  cursor: pointer;
  transition: .3s ease-in-out scale;

  &:hover {
    scale: 1.1;
  }
}
</style>