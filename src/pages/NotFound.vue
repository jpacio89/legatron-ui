<template>
	<div class="exception-body notfound">
	<div class="mobile-banner">
		<img src="assets/layout/images/logo-mobile.svg" alt="prestige-layout"/>
	</div>
	<div class="exception-panel">
		<div class="logo">
			<img src="assets/layout/images/logo.svg" alt="prestige-layout"/>
		</div>
	</div>
	<div class="exception-card">
		<div class="top-border"></div>
		<div class="exception-content">
			<h1>Page Not Found</h1>
			<p>Requested resource is not available.</p>
			<Button label="Go To Dashboard" @click="goDashboard" />
		</div>
	</div>
	</div>
</template>

<script>
	export default {
		methods: {
			goDashboard(){
				window.location = "/#/"
			}
		}
	}
</script>

<style scoped>

</style>