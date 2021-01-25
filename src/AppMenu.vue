<template>
	<AppSubmenu class="layout-menu clearfix" :items="model" :layoutMode="layoutMode" :menuActive="active"
                :root="true" :parentMenuItemActive="true"/>
</template>

<script>
import AppSubmenu from './AppSubmenu';

export default {
	props: {
		layoutMode: String,
		active: Boolean
    },
    data() {
        return {
            model : [
								{ label: 'Overview', icon: 'pi pi-fw pi-home', to:'/' },
								{ label: 'Brains', icon: 'pi pi-fw pi-cloud', to:'/brains' },
								{
									label: 'Chess Brain', icon: 'pi pi-fw pi-cloud',
									items: [
										{ label: 'Information', icon: 'pi pi-fw pi-id-card', to: '/formlayout' },
										{ label: 'Transformers', icon: 'pi pi-fw pi-id-card', to: '/formlayout' },
									]
								},
								/*{
									label: 'UI Kit', icon: 'pi pi-fw pi-star',
									items: [
										{label: 'Form Layout', icon: 'pi pi-fw pi-id-card', to: '/formlayout'},
										{label: 'Input', icon: 'pi pi-fw pi-check-square', to: '/input'},
										{label: 'Float Label', icon: 'pi pi-fw pi-bookmark', to: '/floatlabel'},
										{label: 'Button', icon: 'pi pi-fw pi-mobile', to: '/button', class: 'rotated-icon'},
										{label: 'Table', icon: 'pi pi-fw pi-table', to: '/table'},
										{label: 'List', icon: 'pi pi-fw pi-list', to: '/list'},
										{label: 'Tree', icon: 'pi pi-fw pi-share-alt', to: '/tree'},
										{label: 'Panel', icon: 'pi pi-fw pi-tablet', to: '/panel'},
										{label: 'Overlay', icon: 'pi pi-fw pi-clone', to: '/overlay'},
										{label: "Media", icon: "pi pi-fw pi-image", to: "/media"},
										{label: 'Menu', icon: 'pi pi-fw pi-bars', to: '/menu'},
										{label: 'Message', icon: 'pi pi-fw pi-comment', to: '/messages'},
										{label: 'File', icon: 'pi pi-fw pi-file', to: '/file'},
										{label: 'Chart', icon: 'pi pi-fw pi-chart-bar', to: '/chart'},
										{label: 'Misc', icon: 'pi pi-fw pi-circle-off', to: '/misc'},
										{label: 'Display', icon:'pi pi-fw pi-desktop', to:'/display'},
										{label: 'Elevation', icon:'pi pi-fw pi-external-link', to:'/elevation'},
										{label: 'Flexbox', icon:'pi pi-fw pi-directions', to:'/flexbox'},
										{label: 'Icons', icon:'pi pi-fw pi-search', to:'/icons'},
										{label: 'Widgets', icon:'pi pi-fw pi-star-o', to:'/widgets'},
										{label: 'Grid System', icon:'pi pi-fw pi-th-large', to:'/grid'},
										{label: 'Spacing', icon:'pi pi-fw pi-arrow-right', to:'/spacing'},
										{label: 'Typography', icon:'pi pi-fw pi-align-center', to:'/typography'},
										{label: 'Text', icon:'pi pi-fw pi-pencil', to:'/text'},
										{label: 'Crud', icon: 'pi pi-fw pi-pencil', to: '/crud'},
										{label: 'Calendar', icon: 'pi pi-fw pi-calendar-plus', to: '/calendar'},
										{label: 'Landing', icon: 'pi pi-fw pi-globe', url: 'assets/pages/landing.html', target: '_blank'},
										{label: 'Login', icon: 'pi pi-fw pi-sign-in', to: '/login'},
										{label: 'Invoice', icon: 'pi pi-fw pi-dollar', to: '/invoice'},
										{label: 'Help', icon: 'pi pi-fw pi-question-circle', to: '/help'},
										{label: 'Error', icon: 'pi pi-fw pi-times-circle', to: '/error'},
										{label: 'Not Found', icon: 'pi pi-fw pi-exclamation-circle', to: '/notfound'},
										{label: 'Access Denied', icon: 'pi pi-fw pi-lock', to: '/access'},
										{label: 'Empty', icon: 'pi pi-fw pi-circle-off', to: '/empty'},
										{
											label: 'Submenu 1', icon: 'pi pi-fw pi-align-left',
											items: [
												{
													label: 'Submenu 1.1', icon: 'pi pi-fw pi-align-left',
													items: [
														{label: 'Submenu 1.1.1', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 1.1.2', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 1.1.3', icon: 'pi pi-fw pi-align-left'},
													]
												},
												{
													label: 'Submenu 1.2', icon: 'pi pi-fw pi-align-left',
													items: [
														{label: 'Submenu 1.2.1', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 1.2.2', icon: 'pi pi-fw pi-align-left'}
													]
												},
											]
										},
										{
											label: 'Submenu 2', icon: 'pi pi-fw pi-align-left',
											items: [
												{
													label: 'Submenu 2.1', icon: 'pi pi-fw pi-align-left',
													items: [
														{label: 'Submenu 2.1.1', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 2.1.2', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 2.1.3', icon: 'pi pi-fw pi-align-left'},
													]
												},
												{
													label: 'Submenu 2.2', icon: 'pi pi-fw pi-align-left',
													items: [
														{label: 'Submenu 2.2.1', icon: 'pi pi-fw pi-align-left'},
														{label: 'Submenu 2.2.2', icon: 'pi pi-fw pi-align-left'}
													]
												},
											]
										}
									]
								},*/
								{	label: 'Documentation', icon: 'pi pi-fw pi-info-circle', to: '/documentation' },
						]
        }
    },
	components: {
		'AppSubmenu': AppSubmenu
	}
}
</script>

<style scoped>

</style>
