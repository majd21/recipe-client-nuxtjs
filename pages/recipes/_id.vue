<template>
  <div class="container mt-4">
    <div style="width: 18rem;">

    <div class="card-body">
    <h2 class="card-title">{{recipe.title}}</h2>
    <small>{{recipe.time}}</small>
    <p>{{recipe.items}}</p>
    <p>{{recipe.people}}</p>
    <p class="card-text">{{recipe.description}}</p>
    </div>
    </div>

        <form method="post">
          <div class="form-group">
        <label for="title">Title</label>
        <input class="form-control" type="text" v-model="title" placeholder="enter new title...">
      </div>
      <div class="form-group">
        <label for="items">Items</label>
          <input class="form-control" type="text" v-model="items" placeholder="enter new items...">
      </div>
      <div class="form-group">
        <label for="people">People</label>
          <input class="form-control" type="number" v-model="people" placeholder="enter new people...">
      </div>
      <div class="form-group">
       <label for="description">Description</label>
        <textarea class="form-control" type="text" v-model="description" placeholder="enter new description..."></textarea>
      </div>
          <button class="btn btn-primary" @click="UpdateRecipe">Edit recipe</button>
        </form>
        <br>
        <a class="btn btn-warning" @click="DeleteRecipe">Delete Recipe</a>
        <br>
        <nuxt-link class="btn btn-danger mt-2" to="/">Back to home</nuxt-link>
  </div>
</template>

<script>
export default {
  async asyncData({$axios , params , next}) {
    try {
      let id = params.id
      let recipeResponse = await $axios.$get(`/api/recipes/${id}`)
      console.log(recipeResponse);
      return {
        recipe: recipeResponse.recipe[0]
      }
    } catch (error) {
      console.log(error);
      next(error)
    }
  },
  data() {
    return {
      title: '',
      items: '',
      description: '',
      people: 0
    }
  },
  methods: {
    async UpdateRecipe() {
      let data = {
        title: this.title,
        items: this.items,
        description: this.description,
        people: this.people
      }

      let response = await this.$axios.$put(`/api/recipes/${this.$route.params.id}` , data)

      console.log(response);

      this.$router.push(`/recipe/${params.id}`)
    },
    async DeleteRecipe() {
      let response = await this.$axios.$delete(`/api/recipes/${this.$route.params.id}`)

      console.log(response);

      this.$router.push('/')
    }
  },
}
</script>
