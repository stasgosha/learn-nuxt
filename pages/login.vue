<template>
	<div class="auth-form">
		<h1>Login</h1>
		<form @submit.prevent="onSubmit">
			<div class="form-inner">
				<div class="form-fields">
					<div class="form-field">
						<p v-if="$route.query.message === 'login'" style="color: red">Access denied. Login first</p>
						<p>user: admin, pass: qweqwe</p>
					</div>
					<div class="form-field">
						<input type="text" v-model="username" placeholder="Username" class="input-field">
					</div>
					<div class="form-field">
						<input type="password" v-model="password" placeholder="Password" class="input-field">
					</div>
				</div>
				<div class="form-submit">
					<button class="btn">Log In</button>
				</div>
			</div>
		</form>
	</div>
</template>

<script>
export default {
	layout: 'auth',
	data: () => ({
		username: null,
		password: null
	}),
	methods: {
		onSubmit(){
			if (this.username === 'admin' && this.password === 'qweqwe') {
				this.$store.dispatch('login')
				this.$router.push('/')
			} else{
				alert('Wrong username or password')
			}
		}
	}
}
</script>

<style scoped>
	.auth-form{
		width: 360px;
		margin-left: auto;
		margin-right: auto;
		padding: 24px;
		background: #fff;
		border-radius: 10px;
	}

	.form-fields{
		display: grid;
		grid-gap: 20px;
	}

	.form-submit{
		margin-top: 20px;
	}

	.form-submit .btn{
		width: 100%;
	}

	.input-field{
		width: 100%;
		height: 44px;
		padding: 0 16px;
		border-radius: 4px;
	}

	.btn{
		height: 44px;
		border-radius: 4px;
		cursor: pointer;
	}
</style>