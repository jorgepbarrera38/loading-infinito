<template>
  <div class="container">
    <div class="row">
      <div class="col-md-4 offset-md-4">

        <div class="card margin-top" v-for="(post, index) in posts" :key="index">
          <div class="card-header">
            {{ post.title }}
          </div>
            <div class="card-body">
              {{ post.body }}
            </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  mounted () {
    this.getPosts()
  },
  data () {
    return {
      posts: []
    }
  },
  methods: {
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts?_page=2').then( response => {
        this.posts = response.data
      })
    }
  }
}
</script>
<style scoped>
.margin-top {
  margin-top:20px
}
</style>