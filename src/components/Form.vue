<template>
  <div id="app">
    <form @submit.prevent="createPost">
      <input placeholder="name" v-model="post.name">
      <input placeholder="title" v-model="post.title">
      <br>
      <button type="submit">Create</button>
    </form>
    {{data}}
  </div>
</template>
<script>
export default {
  name: "#app",
  data() {
    return {
      post: {
        name: "",
        title: ""
      },
      data: {}
    };
  },
  methods: {
      utf8_to_b64( str ) {
        return window.btoa(unescape(encodeURIComponent( str )))
      },
    async createPost() {
      let headers = new Headers()
      headers.set('Authorization', 'Basic ' + this.utf8_to_b64("pierre" + ":" + "azerty"))
      const request = new Request(
          "http://localhost/vuewp/wp-json/wp/v2/posts",
          {
            method: "POST",
            mode: "cors",
            cache: "default",
            headers: headers,
            body: JSON.stringify(this.post)
          }
      );
      const res = await fetch(request);
      const data = await res.json();
      this.data = data;
    }
  }
};
</script>

<style>

</style>