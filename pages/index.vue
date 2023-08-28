<template>
  <b-container>
    <myheader />
    <b-card v-for="post in list" :key="post" class="my-2">
      <b-card-title>
        {{post.title}}
      </b-card-title>
      <b-card-text class="text-muted">
        {{post.description}}
      </b-card-text>
      <b-link :to="'post/' + post.slug" class="card-link">記事を読む</b-link>
    </b-card>
  </b-container>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const list = await $content('post').fetch()
    list.sort((a, b) => {
      return (a.path < b.path) ? -1 : 1
    })
    return {
      list
    }
  }
}
</script>
