<template>
	<div :class="containerClass" @click="onDocumentClick">
        <div class="layout-content-wrapper">
            <AppTopBar :topbarMenuActive="topbarMenuActive" :horizontal="layoutMode === 'horizontal'" :activeTopbarItem="activeTopbarItem"
                @menubutton-click="onMenuButtonClick" @topbar-menubutton-click="onTopbarMenuButtonClick" @topbar-item-click="onTopbarItemClick"></AppTopBar>

                <div class="layout-menu-container" @click="onMenuClick">
                    <div class="overlay-menu-button" @click="onMenuButtonClick">
                        <div class="overlay-menu-button-bars">
						<span></span>
						<span></span>
						<span></span>
					</div>
					<div class="overlay-menu-button-times">
						<span></span>
						<span></span>
					</div>
				</div>

				<div class="layout-menu-wrapper fadeInDown">
					<AppMenu :layoutMode="layoutMode" :active="menuActive"
						@menuitem-click="onMenuItemClick" @root-menuitem-click="onRootMenuItemClick"></AppMenu>
				</div>
			</div>

			<AppActionBar />

			<div class="layout-content">
				<router-view />
			</div>

			<AppConfig :theme="theme" :layout="layout" @theme-change="onThemeChange" @layout-change="onLayoutChange" :layoutMode="layoutMode" :wrapperMode="wrapperMode" @layout-mode-change="onLayoutModeChange" @wrapper-mode-change="onWrapperModeChange"></AppConfig>

			<AppFooter />

			<div class="layout-mask"></div>
		</div>
	</div>
</template>

<script>
import AppTopBar from './AppTopbar.vue';
import AppConfig from './AppConfig.vue';
import AppMenu from './AppMenu.vue';
import AppActionBar from './AppActionBar';
import AppFooter from './AppFooter.vue';
import EventBus from './event-bus';

export default {
	props: {
		theme: String,
		layout: String
	},
    data() {
        return {
			layoutMode: 'horizontal',
			wrapperMode: false,
			overlayMenuActive: false,
			mobileMenuActive: false,
			topbarMenuActive: false,
			activeTopbarItem: null,
            menuActive: false
        }
    },
    watch: {
        $route() {
            this.menuActive = false;
            this.$toast.removeAllGroups();
        }
    },
    methods: {
		onDocumentClick() {
			if (!this.topbarItemClick) {
				this.activeTopbarItem = null;
				this.topbarMenuActive = false;
			}

			if (!this.menuClick) {
				if(this.isHorizontal()) {
					this.menuActive = false;
					EventBus.emit('reset-active-index');
				}

				this.hideOverlayMenu();
			}

			this.topbarItemClick = false;
			this.menuClick = false;
		},
		onProfileClick(event) {
			this.profileExpanded = !this.profileExpanded;
			if (this.isHorizontal()) {
				EventBus.emit('reset-active-index');
			}

			event.preventDefault();
		},
		onMenuClick() {
			this.menuClick = true;
		},
		onMenuItemClick(event) {
			if (!event.item.items) {
				EventBus.emit('reset-active-index');
                this.hideOverlayMenu();

                if (this.isHorizontal()) {
                    this.menuActive = false;
                }
            }
		},
		onRootMenuItemClick() {
			this.menuActive = !this.menuActive;
		},
		onMenuButtonClick(event) {
			this.menuClick = true;

			this.topbarMenuActive = false;
			if (this.isDesktop()) {
				if(this.layoutMode === 'overlay') {
					this.overlayMenuActive = !this.overlayMenuActive;
				}
			}
			else {
				this.mobileMenuActive = !this.mobileMenuActive;
			}

			event.preventDefault();
		},
		onTopbarMenuButtonClick(event) {
			this.topbarItemClick = true;
			this.topbarMenuActive = !this.topbarMenuActive;
			this.hideOverlayMenu();
			event.preventDefault();
		},
		onTopbarItemClick(event) {
			this.topbarItemClick = true;

			if(this.activeTopbarItem === event.item)
				this.activeTopbarItem = null;
			else
				this.activeTopbarItem = event.item;

			event.originalEvent.preventDefault();
		},
		hideOverlayMenu() {
			this.overlayMenuActive = false;
			this.mobileMenuActive = false;
		},
		isDesktop() {
			return window.innerWidth > 1024;
		},
		isHorizontal() {
			return this.layoutMode === 'horizontal';
		},
		onLayoutModeChange(layoutMode) {
			this.layoutMode = layoutMode;
			this.staticMenuDesktopInactive = false;
			this.overlayMenuActive = false;
		},
		onWrapperModeChange(wrapperMode) {
			this.wrapperMode = wrapperMode;
		},
		onThemeChange(theme) {
			this.$emit('theme-change', theme);
		},
		onLayoutChange(layout) {
			this.$emit('layout-change', layout);
		}
    },
    computed: {
        containerClass() {
            return ['layout-wrapper', {
				'layout-menu-overlay': this.layoutMode === 'overlay',
				'layout-menu-overlay-active': this.overlayMenuActive,
				'layout-mobile-active': this.mobileMenuActive,
				'layout-menu-horizontal': this.layoutMode === 'horizontal',
				'p-input-filled': this.$appState.inputStyle === 'filled',
				'p-ripple-disabled': this.$primevue.ripple === false
			},
			{
				'layout-fullwidth': this.wrapperMode
			}];
        }
    },
    components: {
        'AppTopBar': AppTopBar,
        'AppConfig': AppConfig,
        'AppMenu': AppMenu,
		'AppFooter': AppFooter,
		'AppActionBar': AppActionBar
    }
}
</script>

<style lang="scss">
@import './App.scss';
</style>
