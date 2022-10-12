<template>
	<section class="default-section">
		<div class="container">
			<h1>Blog</h1>

			<div class="section-text">
				<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Obcaecati sunt et voluptates fugiat! Rerum atque nemo facilis commodi minus ipsa ut cum inventore labore delectus eum repellendus, eveniet, laboriosam hic.</p>
			</div>

			<div class="section-posts" v-if="posts.length">
				<h2>Posts</h2>
				<div class="post-card" v-for="(post, index) in posts" :key="post.id">
					<h3 class="card-title">
						<nuxt-link :to="'/blog/' + post.id">
							{{index + 1}}. {{ post.title }}
						</nuxt-link>
					</h3>
				</div>
			</div>

			<div class="section-posts" v-else>
				<h3>There is no posts</h3>
			</div>
		</div>
	</section>
</template>

<script>
export default {
	async fetch({store}){
		if (store.getters['posts/posts'].length === 0) {
			await store.dispatch('posts/fetchPosts')
		}
	},
	middleware: ['auth'],
	computed: {
		posts() {
			return this.$store.getters['posts/posts']
		}
	}
}
</script>

<style scoped>
	.section-posts{
		margin-top: 40px;
		display: grid;
		grid-gap: 30px;
	}
</style>