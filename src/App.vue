<template>
  <div class="container">
    <h1>Recipe Builder</h1>
    
    <!-- Pass recipe and methods as props to RecipeForm -->
    <RecipeForm 
      :recipe="recipe" 
      @update-recipe="updateRecipe"
      @clear-recipe="clearRecipe"
    />
    
    <!-- Display the recipe and cost using RecipeOutput -->
    <RecipeOutput :recipe="recipe" :totalCost="totalCost" />
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import RecipeForm from './components/RecipeForm.vue';
import RecipeOutput from './components/RecipeOutput.vue';

export default {
  components: {
    RecipeForm,
    RecipeOutput
  },
  setup() {
    const recipe = ref({
      ingredients: [],
      directions: [],
      costs: [] // To store the cost of each ingredient
    });

    const updateRecipe = (newRecipe) => {
      recipe.value = newRecipe;
    };

    const clearRecipe = () => {
      recipe.value = { ingredients: [], directions: [], costs: [] };
    };

    // Computed property to calculate the total cost
    const totalCost = computed(() => {
      return recipe.value.costs.reduce((sum, cost) => sum + parseFloat(cost), 0).toFixed(2);
    });

    return { recipe, updateRecipe, clearRecipe, totalCost };
  }
};
</script>

<style scoped>
/* Your existing styles */
</style>
