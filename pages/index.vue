<template>
  <section class="index">
    <card
      v-for="(post,i) in posts"
      :key="i"
      :title="post.fields.title"
      :id="post.sys.id"
      :date="post.sys.updateAt"
    />
  </section>
</template>

<script>
import Card from '~/components/card.vue'
import { createClient } from '~/plugins/contentful.js'

const client = createClient()
export default {
  transition: 'slide-left',
  components: {
    Card
  },
  asyncData({ env, params }) {
    return client
      .getEntries(env.CTF_BLOG_POST_TYPE_ID)
      .then(entries => {
        return {
          posts: entries.items
        }
      })
      .catch(console.error)
  }
}
</script>