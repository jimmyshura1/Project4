<template>
    <div v-if="recipe.ingredients.length" class="recipe-output">
      <h2>Ingredients</h2>
      <ul>
        <li v-for="(ingredient, index) in recipe.ingredients" :key="index">
          {{ ingredient }} - ${{ recipe.costs[index] }}
        </li>
      </ul>
  
      <h2>Directions</h2>
      <ul>
        <li v-for="(direction, index) in recipe.directions" :key="index">{{ direction }}</li>
      </ul>
  
      
      <h2>Total Cost: ${{ totalCost }}</h2>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      recipe: Object,
      totalCost: String
    }
  };
  </script>