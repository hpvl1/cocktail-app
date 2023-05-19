<script setup>
import { defineProps } from 'vue';
import { RouterLink } from 'vue-router';

const props = defineProps({
  cocktail: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="cocktail">
    <RouterLink :to="`/cocktails/${cocktail.idDrink}`">
      <div
        :style="`background-image: url(${cocktail.strDrinkThumb})`"
        class="cocktail__picture"
      ></div>
    </RouterLink>
    <div class="cocktail__title">{{ cocktail.strDrink }}</div>
  </div>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

.cocktail
    width: calc((100% - 76px) / 3)
    padding-right: 38px
    padding-bottom: 20px

    &:nth-child(3n + 3)
        padding-right: 0
    &__picture
        width: 120px
        height: 120px
        margin: 0 auto
        background-repeat: no-repeat
        background-position: 50% 50%
        background-size: 100%
    &__title
        padding-top: 15px
        letter-spacing: 0.1em
</style>
