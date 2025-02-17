<template>
    <form @submit.prevent="submitRecipe">
      <label for="ingredients">Ingredients (separate by comma):</label>
      <textarea 
        id="ingredients" 
        v-model="ingredients" 
        required
      ></textarea>
  
      <label for="ingredient-costs">Costs (separate by comma, e.g., 2.5, 3.0):</label>
      <textarea 
        id="ingredient-costs" 
        v-model="ingredientCosts" 
        required
      ></textarea>
  
      <label for="directions">Directions (each step on a new line):</label>
      <textarea 
        id="directions" 
        v-model="directions" 
        required
      ></textarea>
  
      <div class="button-group">
        <button type="submit">Generate Full Recipe</button>
        <button type="button" @click="clearRecipe">Clear</button>
      </div>
    </form>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    props: {
      recipe: Object
    },
    emits: ['update-recipe', 'clear-recipe'],
    setup(props, { emit }) {
      const ingredients = ref('');
      const ingredientCosts = ref(''); // To hold the costs for each ingredient
      const directions = ref('');
  
      const submitRecipe = () => {
        const ingredientsList = ingredients.value.split(',').map(i => i.trim());
        const costList = ingredientCosts.value.split(',').map(c => c.trim());
  
        const newRecipe = {
          ingredients: ingredientsList,
          directions: directions.value.split('\n').map(d => d.trim()),
          costs: costList
        };
  
        emit('update-recipe', newRecipe);
      };
  
      const clearRecipe = () => {
        ingredients.value = '';
        ingredientCosts.value = '';
        directions.value = '';
        emit('clear-recipe');
      };
  
      return { ingredients, ingredientCosts, directions, submitRecipe, clearRecipe };
    }
  };
  </script>