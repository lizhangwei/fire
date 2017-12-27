<template>
  <div class="hello">
    <input type="text" v-model="newPost.title" name="">
    <button v-on:click="submit()" >提交</button>
    <ul>
      <li v-for="post in posts">
        {{post.title}}
      </li>
    </ul>
  </div>
</template>

<script>
import fire from '@/fire.js'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      posts: [],
      newPost: {
        title: '',
        ctime: fire.database.ServerValue.TIMESTAMP
      }
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {
      fire.database().ref('posts').on('value', (data) => {
        this.posts = data.val()
      })
    },
    submit () {
      fire.database().ref('posts').push(this.newPost).then(data => {
        // alert()
      })
    }
  }
}
</script>

