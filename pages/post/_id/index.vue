<template>
  <div class="main-content">
    <div class="container">
      <h2 class="title is-2">{{ post.title }}</h2>
      <div v-html="post.content"></div>
      <br>
      <h4 class="title is-5 is-marginless">by <strong>{{ post.author }}</strong> at <strong>{{ post.published }}</strong></h4>
    </div>
  </div>
</template>

<script>
import posts from '~/dummy_posts.json'

export default {
  validate ({ params }) {
    return /^\d+$/.test(params.id)
  },
  asyncData ({ params }, callback) {
    const post = posts.find(post => post.id === parseInt(params.id))
    if (post) {
      callback(null, { post })
    } else {
      callback(null, { statusCode: 404, message: 'Post not found' })
    }
  },
  head () {
    return {
      title: this.post.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.post.summary
        }
      ]
    }
  }
}
</script>
