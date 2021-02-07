<template>
	<div class="layout-topbar">
		<div class="layout-topbar-logo" @click="$router.push({path: '/'})">
			<img class="logo" src="assets/layout/images/logo.png" alt="">
        </div>

        <a class="layout-menu-button" href="#" @click="onMenuButtonClick">
            <i class="pi pi-bars"></i>
        </a>

		<ul class="layout-topbar-menu">
			
		</ul>

	</div>
</template>

<script>
	export default {
		emits: ['topbar-item-click', 'menubutton-click', 'topbar-menubutton-click'],
		props: {
			topbarMenuActive: Boolean,
			horizontal: Boolean,
			activeTopbarItem: String
		},
		methods: {
			onMenuButtonClick(event) {
				this.$emit('menubutton-click', event);
			},
			onTopbarMenuButtonClick(event) {
				this.$emit('topbar-menubutton-click', event);
			}
		},
		computed: {

		}
	}
</script>
