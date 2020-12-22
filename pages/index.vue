<template>
  <div class="container">
    <nuxt-link class="btn btn-success mt-4" to="/recipes">Add a new Recipe</nuxt-link>
    <div class="mt-4">
    <div v-for="recipe in recipes" :key="recipe._id" class="card col-sm-4" style="width: 18rem;">

    <div class="card-body">
    <a class="btn btn-default" :href="`recipes/${recipe._id}`"><h2 class="card-title">{{recipe.title}}</h2></a>
    <p class="card-text">{{recipe.description}}</p>
    </div>
    </div>

</div>
  </div>
</template>

<script>
export default {
  async asyncData({$axios , next}) {
    try {
      let response = await $axios.$get('/api/recipes')
      console.log(response);
      return {
        recipes: response.recipe
      }
    } catch (error) {
      console.log(error);
      next(error)
    }
  },
}
</script>

<style>

</style>
