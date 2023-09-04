<template>
  <div>
    <myheader />
    <b-container>
      <b-row>
        <b-col
          v-for="post in list"
          :key="post"
          sm="12"
          md="8"
          lg="6"
          class="my-2"
        >
          <b-card
            :img-src="post.image"
          >
            <b-card-title>
              {{ post.title }}
            </b-card-title>
            <b-card-text class="text-muted">
              {{ post.description }}
            </b-card-text>
            <b-button :to="'post/' + post.slug" class="card-link">記事を読む</b-button>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
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
