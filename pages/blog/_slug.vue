<template>
  <article>
    <nuxt-content :document="article" />
     <div class="container my-12 mx-auto px-4 md:px-12">
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <div class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3" v-for="item in article" :key="item.slug">
                <article class="overflow-hidden rounded-lg shadow-lg">
                    <a href="#">
                        <img alt="Placeholder" class="block h-auto w-full" :src="item.image">
                    </a>

                    <header class="flex items-center justify-between leading-tight p-2 md:p-4">
                        <h1 class="text-lg">
                            <a class="no-underline hover:underline text-black" href="#">
                            {{ item.title }}
                            </a>
                        </h1>
                        <p class="text-grey-darker text-sm">
                        {{ formatDate(item.updatedAt) }}
                        </p>
                    </header>

                    <footer class="flex items-center justify-between leading-none p-2 md:p-4">
                        <a class="flex items-center no-underline hover:underline text-black" href="#">
                            <img alt="Placeholder" class="block rounded-full"  src="https://picsum.photos/32/32/?random">
                            <p class="ml-2 text-sm">
                                Author Name
                            </p>
                        </a>
                        <a class="no-underline text-grey-darker hover:text-red-dark" href="#">
                            <span class="hidden">Like</span>
                            <i class="fa fa-heart"></i>
                        </a>
                    </footer>

                </article>
            </div>
        </div>
    </div>
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