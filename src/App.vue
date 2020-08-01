<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 offset-md-3">

        <div class="card margin-top" v-for="(post, index) in posts" :key="index">
          <div class="card-header">
            {{ post.title }}
          </div>
            <div class="card-body">
              {{ post.body }}
            </div>
        </div>
        <infinite-loading @infinite="getPosts"></infinite-loading>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import InfiniteLoading from 'vue-infinite-loading';
export default {
  components: {
    InfiniteLoading
  },
  data () {
    return {
      page: 1,
      posts: []
    }
  },
  methods: {
    getPosts($state) {
      axios.get('https://jsonplaceholder.typicode.com/posts?&_page=' + this.page).then( response => {
        if (response.data.length) {
          this.page += 1
          this.posts.push(...response.data)
          $state.loaded()
        } else {
           $state.complete();
        }
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