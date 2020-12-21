<template>
  <div class="container">
    <nuxt-link class="btn btn-success mt-4" to="/recipes">Add a new Recipe</nuxt-link>
    <ul>
      <li v-for="recipe in recipes" :key="recipe._id">
        <a :href="`recipes/${recipe._id}`"><h1>{{recipe.title}}</h1></a>
        <p>{{recipe.items}}</p>
        <p>{{recipe.people}}</p>
        <p>{{recipe.description}}</p>
      </li>
    </ul>
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
