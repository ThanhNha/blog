<style>
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
  }
</style>

<template>
  <article>
    <nuxt-content :document="article" />
    
        <article v-for="item in article">
          <h1>{{ item.title }}</h1>
            <p>{{ item.description }}</p>
            <img :src="item.image" :alt="item.alt" />
        </article>
    
        <!-- <p>Article last updated: {{ formatDate(article.updatedAt) }}</p> -->
  </article>
  
  
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('blogs', params.slug).fetch()
      console.log(article);
      return { article }
    },
    methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
 }
    
  }
  
</script>