<template>
<Banner>
  <FlavoursList @live-end="needChange = true" v-if="!needChange"/>
  <DrinkTeaBanner v-else/>
</Banner>
</template>

<script setup lang="ts">
import FlavoursList from "./components/flavours-banner/FlavoursList.vue";
import DrinkTeaBanner from "./components/drink-tea-banner/DrinkTeaBanner.vue";
import Banner from "./components/Banner.vue";
import {ref} from "vue";
const needChange = ref(false)

</script>

<style scoped lang="scss">

</style>
