<template>
	<nav class="top-nav">
		<ul>
			<li v-for="item in navItems" :key="item.text">
				<nuxt-link :to="item.to" :exact="item.isExact" active-class="current">
					{{ item.text }}
				</nuxt-link>
			</li>
			<li v-if="!hasToken">
				<nuxt-link to="/login" active-class="current">Login</nuxt-link>
			</li>
			<li v-else>
				<a href="#" @click.prevent="logout">Logout</a>
			</li>
		</ul>
	</nav>
</template>

<script>
export default {
	data() {
		return {
			navItems: [
				{
					text: 'Home',
					to: '/',
					isExact: true
				},
				{
					text: 'About',
					to: '/about',
					isExact: false
				},
				{
					text: 'Blog',
					to: '/blog',
					isExact: false
				}
			]
		}
	},
	computed: {
		hasToken(){
			return this.$store.getters.hasToken
		}
	},
	methods: {
		logout(){
			this.$store.dispatch('logout')
			this.$router.push('/login')
		}
	}
}
</script>