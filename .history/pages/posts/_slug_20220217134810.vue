<template>
  <div>
    <v-row>
      <v-btn class="nav-button" :to="`/posts/${id - 1}`" nuxt>
        Previous
      </v-btn>
      <v-spacer />
      <v-btn class="nav-button" :to="`/posts/${id + 1}`" nuxt>
        Next
      </v-btn>
    </v-row>
    <br>
    <h1 class="title-text">{{ title }}</h1>
    <h4 class="body-text">{{ body }}</h4>
    <br>
    <h2 class="comment-title">Commentaires : </h2>
    <ul>
      <li v-for="comment in comments" :key="comment.id">
        <v-row class="comment-upper-part">
          <h3 class="body-text">{{ comment.name }}</h3>
          <v-spacer />
          <h3 class="body-text">{{ comment.email }}</h3>
        </v-row>
        <h4 class="body-text"><i>{{ comment.body }}</i></h4>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData ({ params, $axios }) {
    const slug = params.slug
    const { data } = await $axios.get(
      `https://jsonplaceholder.typicode.com/posts/${slug}`
    )
    const comments = await $axios.$get(`https://jsonplaceholder.typicode.com/posts/${slug}/comments`)
    const { title, body, id } = data
    return { title, body, id, comments }
  }
}
</script>