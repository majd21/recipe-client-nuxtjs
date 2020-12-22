<template>
  <div class="container">
    <form>
      <h1>Add a new recipe</h1>
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
          <button class="btn btn-primary" @click="AddNewRecipe">Add recipe</button>
    </form>
    <nuxt-link class="btn btn-danger mt-2" to="/">Back to home</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      items: '',
      description: '',
      people: 0
    }
  },
  methods: {
    async AddNewRecipe() {
      try {
        let data = {
        title: this.title,
        people: this.people,
        description: this.description,
        items: this.items
      }
      let response = await this.$axios.$post('/api/recipes' , data)

      console.log(response)

      this.$router.push('/')
      } catch (error) {
        console.log(error);
      }
    }
  },
}
</script>
