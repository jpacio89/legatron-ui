<template>
    <div id="layout-config" :class="containerClass">
        <div class="layout-config-content">
            <a class="layout-config-button" id="layout-config-button" @click="toggleConfigurator">
                <i class="pi pi-save"></i>
            </a>
            <a tabindex="0" class="layout-config-close" @click="hideConfigurator">
                <i class="pi pi-times"></i>
            </a>
            <TabView>
                <TabPanel header="Metrics"></TabPanel>
                <TabPanel header="Data">
                  <DataTable :paginator="true" class="p-datatable-customers" :rows="10" dataKey="id" :rowHover="true">
                    <template #empty>
                      No data available.
                    </template>
                    <template #loading>
                      Loading transformed data. Please wait.
                    </template>
                    <Column field="name" header="Name">
                      <template>
                        <span class="p-column-title">Name</span>
                      </template>
                    </Column>
                    <Column field="date" header="Date">
                      <template>
                        <span class="p-column-title">Date</span>
                        <span></span>
                      </template>
                    </Column>
                    <Column field="status" header="Status">
                      <template>
                        <span class="p-column-title">Status</span>
                        <span></span>
                      </template>
                    </Column>
                    <Column field="activity" header="Score">
                      <template>
                        <span class="p-column-title">Score</span>
                      </template>
                    </Column>
                  </DataTable>
                </TabPanel>
                <TabPanel header="Log">
                    <div class="timeline">
                      <ul>
                        <li v-for="n in 20" v-bind:key="n">
                          <div class="p-grid">
                            <div class="p-col-fixed">
                              <div class="timeline-icon">
                                <i class="pi pi-inbox"></i>
                              </div>
                            </div>
                            <div class="p-col">
                              <div class="time-line-event">
                                <!--<span class="timeline-event-title">Info</span>-->
                                <div class="timeline-event-message">Transformer loaded into the remote brain.</div>
                                <!--<div class="timeline-event-time">
                                  2 mins ago
                                </div>-->
                              </div>
                            </div>
                          </div>
                        </li>
                      </ul>
                    </div>
                </TabPanel>
            </TabView>
        </div>
    </div>
</template>

<script>
export default {
    emits: ['wrapper-mode-change', 'layout-mode-change', 'layout-change', 'theme-change'],
    props: {
        theme: String,
        layout: String,
        layoutMode: {
            type: String,
            default: null
        },
        wrapperMode: {
            type: Boolean,
            default:false
        }
    },
    data() {
        return {
            active: false,
			componentThemes: [
                {name: 'Amber Accent', file: 'amber', color:'#FFC107'},
                {name: 'Blue Accent', file: 'blue', color:'#2196F3'},
                {name: 'Blue Gray Accent', file: 'bluegray', color:'#607D8B'},
                {name: 'Brown Accent', file: 'brown', color:'#795548'},
                {name: 'Cyan Accent', file: 'cyan', color:'#00BCD4'},
                {name: 'Deep Orange Accent', file: 'deeporange', color:'#FF5722'},
                {name: 'Deep Purple Accent', file: 'deeppurple', color:'#673AB7'},
                {name: 'Green Accent', file: 'green', color:'#4CAF50'},
                {name: 'Indigo Accent', file: 'indigo', color:'#3F51B5'},
                {name: 'Light Blue Accent', file: 'lightblue', color:'#03A9F4'},
                {name: 'Light Green Accent', file: 'lightgreen', color:'#8BC34A'},
                {name: 'Lime Accent', file: 'lime', color:'#CDDC39'},
                {name: 'Orange Accent', file: 'orange', color:'#FF9800'},
                {name: 'Pink Accent', file: 'pink', color:'#E91E63'},
                {name: 'Purple Accent', file: 'purple', color:'#9C27B0'},
                {name: 'Teal Accent', file: 'teal', color:'#00796B'},
                {name: 'Yellow Accent', file: 'yellow', color:'#FFEB3B'},
            ],
            layoutThemesImage: [
                {name: 'Aqua', file: 'layout-aqua', image: 'aqua.png', componentTheme: 'cyan'},
                {name: 'Arecaceae', file: 'layout-arecaceae', image: 'arecaceae.png', componentTheme: 'green'},
                {name: 'Canvas', file: 'layout-canvas', image: 'canvas.png', componentTheme: 'indigo'},
                {name: 'Cross', file: 'layout-cross', image: 'cross.png', componentTheme: 'brown'},
                {name: 'Dream', file: 'layout-dream', image: 'dream.png', componentTheme: 'teal'},
                {name: 'Emerald', file: 'layout-emerald', image: 'emerald.png', componentTheme: 'bluegray'},
                {name: 'Focus', file: 'layout-focus', image: 'focus.png', componentTheme: 'bluegray'},
                {name: 'Forest', file: 'layout-forest', image: 'forest.png', componentTheme: 'teal'},
                {name: 'Fractal', file: 'layout-fractal', image: 'fractal.png', componentTheme: 'teal'},
                {name: 'Gem', file: 'layout-gem', image: 'gem.png', componentTheme: 'amber'},
                {name: 'Grass', file: 'layout-grass', image: 'grass.png', componentTheme: 'lightgreen'},
                {name: 'Jungfraujoch', file: 'layout-jungfraujoch', image: 'jungfraujoch.png', componentTheme: 'lightblue'},
                {name: 'Mackenzie', file: 'layout-mackenzie', image: 'mackenzie.png', componentTheme: 'bluegray'},
                {name: 'Madrid', file: 'layout-madrid', image: 'madrid.png', componentTheme: 'bluegray'},
                {name: 'Marble', file: 'layout-marble', image: 'marble.png', componentTheme: 'purple'},
                {name: 'Metro', file: 'layout-metro', image: 'metro.png', componentTheme: 'bluegray'},
                {name: 'Milan', file: 'layout-milan', image: 'milan.png', componentTheme: 'bluegray'},
                {name: 'Mist', file: 'layout-mist', image: 'mist.png', componentTheme: 'cyan'},
                {name: 'Osterreich', file: 'layout-osterreich', image: 'osterreich.png', componentTheme: 'cyan'},
                {name: 'Palm', file: 'layout-palm', image: 'palm.png', componentTheme: 'bluegray'},
                {name: 'Polygon', file: 'layout-polygon', image: 'polygon.png', componentTheme: 'lightblue'},
                {name: 'Sand', file: 'layout-sand', image: 'sand.png', componentTheme: 'brown'},
                {name: 'Stone', file: 'layout-stone', image: 'stone.png', componentTheme: 'lightgreen'},
                {name: 'Wood', file: 'layout-wood', image: 'wood.png', componentTheme: 'green'}
            ],
            layoutThemesColored: [
                {name: 'Amber', file: 'layout-amber', color1: '#FFB300', color2: '#FF6F00', componentTheme: 'amber'},
                {name: 'Amethyst', file: 'layout-amethyst', color1: '#8E24AA', color2: '#5E35B1', componentTheme: 'purple'},
                {name: 'Blue', file: 'layout-blue', color1: '#1E88E5', color2: '#0D47A1', componentTheme: 'blue'},
                {name: 'Blue Grey', file: 'layout-bluegray', color1: '#546E7A', color2: '#263238', componentTheme: 'bluegray'},
                {name: 'Brown', file: 'layout-brown', color1: '#6D4C41', color2: '#3E2723', componentTheme: 'brown'},
                {name: 'Cyan', file: 'layout-cyan', color1: '#00ACC1', color2: '#006064', componentTheme: 'cyan'},
                {name: 'Deep Orange', file: 'layout-deeporange', color1: '#F4511E', color2: '#BF360C', componentTheme: 'deeporange'},
                {name: 'Deep Purple', file: 'layout-deeppurple', color1: '#5E35B1', color2: '#311B92', componentTheme: 'deeppurple'},
                {name: 'Fate', file: 'layout-fate', color1: '#3949AB', color2: '#D81B60', componentTheme: 'blue'},
                {name: 'Green', file: 'layout-green', color1: '#43A047', color2: '#1B5E20', componentTheme: 'green'},
                {name: 'Indigo', file: 'layout-indigo', color1: '#3949AB', color2: '#1A237E', componentTheme: 'indigo'},
                {name: 'Light Blue', file: 'layout-lightblue', color1: '#039BE5', color2: '#01579B', componentTheme: 'lightblue'},
                {name: 'Light Green', file: 'layout-lightgreen', color1: '#7CB342', color2: '#33691E', componentTheme: 'lightgreen'},
                {name: 'Lime', file: 'layout-lime', color1: '#C0CA33', color2: '#827717', componentTheme: 'lime'},
                {name: 'Midnight', file: 'layout-midnight', color1: '#2c3640', color2: '#15202b', componentTheme: 'blue'},
                {name: 'Orange', file: 'layout-orange', color1: '#FB8C00', color2: '#E65100', componentTheme: 'orange'},
                {name: 'Pink', file: 'layout-pink', color1: '#D81B60', color2: '#880E4F', componentTheme: 'pink'},
                {name: 'Purple', file: 'layout-purple', color1: '#8E24AA', color2: '#4A148C', componentTheme: 'purple'},
                {name: 'Rhyme', file: 'layout-rhyme', color1: '#1E88E5', color2: '#8E24AA', componentTheme: 'blue'},
                {name: 'Smoke', file: 'layout-smoke', color1: '#6c757d', color2: '#343a40', componentTheme: 'lightgreen'},
                {name: 'Soul', file: 'layout-soul', color1: '#1E88E5', color2: '#311B92', componentTheme: 'blue'},
                {name: 'Steel', file: 'layout-steel', color1: '#43464B', color2: '#212325', componentTheme: 'lightgreen'},
                {name: 'Teal', file: 'layout-teal', color1: '#00897B', color2: '#004D40', componentTheme: 'teal'},
                {name: 'Yellow', file: 'layout-yellow', color1: '#FDD835', color2: '#F57F17', componentTheme: 'yellow'}
            ]
        }
    },
    watch: {
        $route() {
            if (this.active) {
                this.active = false;
                this.unbindOutsideClickListener();
            }
        }
    },
    outsideClickListener: null,
    methods: {
        onChange(value) {
            this.$appState.inputStyle = value;
        },
        onRippleChange(value) {
            this.$primevue.ripple = value;
        },
        toggleConfigurator(event) {
            this.active = !this.active;
            event.preventDefault();

            if (this.active)
                this.bindOutsideClickListener();
            else
                this.unbindOutsideClickListener();
        },
        hideConfigurator(event) {
            this.active = false;
            this.unbindOutsideClickListener();
            event.preventDefault();
        },
        changeWrapperMode(event, mode) {
            this.$emit('wrapper-mode-change',mode);
        },
        changeLayoutMode(event, mode) {
            this.$emit('layout-mode-change', mode);
        },
        changeLayoutTheme(event, layout, theme) {
            this.$emit('layout-change', layout);
            this.$emit('theme-change', theme);
            this.changeStyleSheetUrl('layout-css', layout, 'layout');
			this.changeStyleSheetUrl('theme-css', theme, 'theme');
            event.preventDefault();
        },
        changeComponentTheme(event, theme) {
            this.changeStyleSheetUrl('theme-css', theme, 'theme');
            this.$emit('theme-change', theme);
            event.preventDefault();
        },
        bindOutsideClickListener() {
            if (!this.outsideClickListener) {
                this.outsideClickListener = (event) => {
                    if (this.active && this.isOutsideClicked(event)) {
                        this.active = false;
                    }
                };
                document.addEventListener('click', this.outsideClickListener);
            }
        },
        unbindOutsideClickListener() {
            if (this.outsideClickListener) {
                document.removeEventListener('click', this.outsideClickListener);
                this.outsideClickListener = null;
            }
        },
        isOutsideClicked(event) {
            return !(this.$el.isSameNode(event.target) || this.$el.contains(event.target));
        },
		changeStyleSheetUrl(id, value) {
			let element = document.getElementById(id);
			let urlTokens = element.getAttribute('href').split('/');

			if (id.localeCompare('layout-css') === 0) {
				urlTokens[urlTokens.length - 1] = value + '.css';
			}
			else {
				urlTokens[urlTokens.length - 1] = 'theme-' + value + '.css' ;
            }

			let newURL = urlTokens.join('/');
			this.replaceLink(element, newURL);
		},
		replaceLink(linkElement, href) {
			const id = linkElement.getAttribute('id');
			const cloneLinkElement = linkElement.cloneNode(true);

			cloneLinkElement.setAttribute('href', href);
			cloneLinkElement.setAttribute('id', id + '-clone');

			linkElement.parentNode.insertBefore(cloneLinkElement, linkElement.nextSibling);

			cloneLinkElement.addEventListener('load', () => {
				linkElement.remove();
				cloneLinkElement.setAttribute('id', id);
			});
		}
    },
    computed: {
        containerClass() {
            return ['layout-config', {'layout-config-active': this.active}];
        },
        rippleActive() {
            return this.$primevue.ripple;
        },
        value() {
            return this.$appState.inputStyle;
        }
    }
}
</script>

<style scoped lang="scss">

</style>
