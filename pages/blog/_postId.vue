<template>
	<section class="default-section">
		<div class="container">
			<nuxt-link to="/blog">Go back</nuxt-link>
			<br><br>
			<h1>{{ post.title }}</h1>
			<p class="author">{{ author.name }}</p>

			<div class="section-text">
				{{ post.body }}
			</div>
		</div>
	</section>
</template>

<script>
  export default {
	middleware: ['auth'],
    async asyncData({ params, $axios }) {
      const post = await $axios.$get('https://jsonplaceholder.typicode.com/posts/' + params.postId)
	  const author = await $axios.$get('https://jsonplaceholder.typicode.com/users/' + post.userId)

	  return {post, author}
    },
	validate({params}){
		return /^\d+$/.test(params.postId)
	},
	data(){
		return {
			post: [],
			author: ''
		}
	}
  }
</script>

<style scoped>
	.author{
		margin-bottom: 30px;
	}
</style>