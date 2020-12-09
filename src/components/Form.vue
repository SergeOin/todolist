<template>
  <div id="app">
    <form class="mb-3">
      <label>Créer un Post It</label>
      <div class="d-flex justify-content-center">
        <input class="form-control mr-2" style="width: 35%;" type="text" name="postit" v-model="newPost">
        <input class="btn btn-outline-success" type="submit" value="Créer" @click="addPost">
      </div>
    </form>
    <div class="card-columns w-75 mt-3 mx-auto">
      <div v-for="post in postits" :key="post" class="card" style="width: 18rem;">
        <div class="card-header bg-transparent border-0">
          <h5 class="card-title">{{ post }}</h5>
        </div>
        <div class="card-footer bg-transparent border-0">
          <a class="btn btn-outline-danger mr-2" @click="deletePost(post)">Supprimer</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default  {
  el: '#app',
  data() {
    return {
      postits: [],
      newPost: null
    }
  },
  mounted() {
    if (localStorage.getItem('postits')) {
      try {
        this.postits = JSON.parse(localStorage.getItem('postits'));
      } catch (e) {
        localStorage.removeItem('postits');
      }
    }
  },
  methods: {
    addPost() {
      // s'assurer que l'utilisateur a entré quelque chose
      if (!this.newPost) {
        return;
      }

      this.postits.push(this.newPost);
      this.newPost = '';
      this.savePosts();
    },
    deletePost(post) {
      this.postits.splice(post, 1);
      this.savePosts();
    },
    savePosts() {
      const parsed = JSON.stringify(this.postits);
      localStorage.setItem('postits', parsed);
    }
  }
}
</script>

<style>

</style>