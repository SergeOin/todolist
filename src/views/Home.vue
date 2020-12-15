<template>
    <Form />
</template>

<script>
// @ is an alias to /src
import Form from '@/components/Form'
import {ref} from "@vue/reactivity";
export default {
  name: 'App',
  components: {
    Form,
  },
  setup() {
    let postits = ref([])
    const savePost = function (data) {
      console.log("App | savePost() | data", data)
      postits.value = [...postits.value, { postit: data, id: Date.now()}]
      console.log("App | savePost() | postits.value", postits.value)
    }
    const editPost = function(post) {
      postits.value = postits.value.map(p => p.id !== post.id ? p : post)
    }
    const deletePost = function(post){
      console.log("App | deletePost() | post", post)
      postits.value = postits.value.filter(p => p.id !== post.id)
    }
    return{
      savePost,
      deletePost,
      editPost,
      postits,
    }
  }
}
</script>
