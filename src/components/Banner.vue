<template>
  <div class="banner">
    <slot></slot>
  </div>
</template>

<style scoped lang="scss">
@use "@styles/variables" as *;

.banner {
  width: 300px;
  height: 600px;
  background-image: url("src/assets/images/bannerBg_1.png");
  font-family: $main-font-family;
  font-style: italic;
  color: $main-font-color;
  overflow: hidden;
}
</style>