<template>
	<body class="login-body">
		<div class="mobile-banner">
			<img src="assets/layout/images/logo-mobile.svg" alt="prestige-layout"/>
		</div>
		<div class="login-panel">
			<div class="logo">
				<img src="assets/layout/images/logo.svg" alt="prestige-layout"/>
			</div>
		</div>
		<div class="login-card">
			<div class="top-border"></div>
			<div class="login-content">
				<h1>Login</h1>
				<p>Welcome, please use the form to sign-in.</p>
				<div class="username-container">
					<label>Username</label>
					<div class="login-input">
						<InputText placeholder="Username"/>
					</div>
				</div>
				<div class="password-container">
					<label>Password</label>
					<div class="login-input">
							<InputText type="password" placeholder="Password"/>
					</div>
				</div>
				<div class="forgetpassword-container">
					<a href="#" class="forget-password">Forget Password?</a>
				</div>
				<div>
					<Button label="Sign In" @click="goDashboard"/>
				</div>
			</div>

		</div>
	</body>
</template>

<script>
	export default {
		data() {
			return {
				username: '',
				password: ''
			}
		},
		methods: {
			goDashboard(){
				window.location = "/#/"
			}
		}
	}
</script>

<style scoped>

</style>