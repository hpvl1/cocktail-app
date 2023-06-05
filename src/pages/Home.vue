<script setup>
import { useRootStore } from '../stores/root';
import { storeToRefs } from 'pinia';

import AppLayout from '../components/AppLayout.vue';
import CocktailItem from '../components/CocktailItem.vue';

const rootStore = useRootStore();
rootStore.getIngredients();

const { ingredients, ingredient, cocktails } = storeToRefs(rootStore);

function getCocktails() {
  rootStore.getCocktails(rootStore.ingredient);
}

function removeIngredient() {
  rootStore.setIngredient(null);
}
</script>

<template>
  <AppLayout imgUrl="../assets/img/bg-1.jpg" :back-func="removeIngredient" :is-back-button-visible="!!ingredient">
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <div class="title">Choose your drink</div>
        <div class="line"></div>
        <div class="select-wrapper">
          <el-select
            v-model="rootStore.ingredient"
            class="select"
            filterable
            allow-create
            placeholder="Choose main ingredient"
            size="large"
            @change="getCocktails"
          >
            <el-option
              v-for="item in ingredients"
              :key="item.strIngredient1"
              :label="item.strIngredient1"
              :value="item.strIngredient1"
            />
          </el-select>
        </div>
        <div class="text">
          Try our delicious cocktail recipes for every occasion. Find delicious cocktail recipes by
          ingredient through our cocktail generator.
        </div>
        <img src="../assets/img/cocktails.png" alt="Cocktails" class="img" />
      </div>
      <div v-else class="info">
        <div class="title">COCKTAILS WITH {{ ingredient }}</div>
        <div class="line"></div>
        <div class="cocktails">
          <CocktailItem
            v-for="cocktail in cocktails"
            :key="cocktail.idDrink"
            :cocktail="cocktail"
          />
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
.select-wrapper
    padding-top: 50px

.select
    width: 220px
.text
    margin: 0 auto
    max-width: 516px
    padding-top: 50px
    line-height: 36px
    letter-spacing: 0.1em
    color: $textMuted
.img
    margin-top: 60px

.cocktails
    display: flex
    flex-wrap: wrap
    align-items: center
    margin-top: 60px
    max-height: 400px
    overflow-y: auto
</style>
