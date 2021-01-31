<template>
	<div class="p-grid dashboard">
		<div class="p-col-12 p-md-6 p-lg-4" v-for="index in 10" :key="index">
			<div class="card user-card">
				<div class="user-card-header">
					<img src="assets/layout/images/dashboard/bg-head.jpg" alt="">
				</div>
				<div class="user-card-content">
					<img src="assets/layout/images/avatar/avatar-igor.jpg" alt="">
					<router-link to="grid">
						<Button type="button" icon="pi pi-arrow-right" @click="menuToggle"/>
					</router-link>

					<div class="user-card-name">
						<span>KasparoV Chess Bot</span>
					</div>
					<div class="user-card-status">
						<span>Google</span>
					</div>
					<div class="user-detail">
						<div>The purpose of this brain is to learn to play chess and master winning gameplay tactics and strategies.</div>
						<ul>
							<li>
								Status <div class="value">Active</div>
							</li>
							<li>
								Monthly Budget <div class="value">1,000$</div>
							</li>
							<li>
								Transformer Count <div class="value">20</div>
							</li>
							<li>
								Transformer Active/Inactive Ratio <div class="value">0.4</div>
							</li>
						</ul>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import ProductService from '../service/ProductService';

export default {
	data() {
		return {
			tasksCheckbox: [],
			chartData: {
				labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
                datasets: [{
                    label: 'Sales',
                    data: [12, 19, 3, 5, 2, 3, 9],
                    borderColor: [
                        '#4CAF50',
                    ],
                    borderWidth: 3,
                    borderDash:[5, 5],
                    fill: false,
                    pointRadius: 3
                }, {
                    label: 'Income',
                    data: [1, 2, 5, 3, 12, 7, 15],
                    backgroundColor: [
                        'rgba(187,222,251,0.2)',
                    ],
                    borderColor: [
                        '#00BCD4',
                    ],
                    borderWidth: 3,
                    fill: true
                },
                {
                    label: 'Expenses',
                    data: [7, 12, 15, 5, 3, 13, 21],
                    borderColor: [
                        '#e91e63',
                    ],
                    borderWidth: 3,
                    fill: false,
                    pointRadius: [4, 6, 4, 12, 8, 0, 4]
                },
                {
                    label: 'New Users',
                    data: [3, 7, 2, 17, 15, 13, 19],
                    borderColor: [
                        '#FF8F00',
                    ],
                    borderWidth: 3,
                    fill: false
                }]
			},
			chartOptions: {
                responsive: true,
                hover: {
                    mode: 'index'
                },
                scales: {
                    xAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Month'
                        }
                    }],
                    yAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Value'
                        }
                    }]
                }
			},
			textAreaValue:"",
			products: null,
			selectedProduct: null,
			items: [
				{ label: 'Save', icon: 'pi pi-fw pi-check' },
				{ label: 'Update', icon: 'pi pi-fw pi-refresh' },
				{ label: 'Delete', icon: 'pi pi-fw pi-trash' }
			]
		}
	},
	productService: null,
	created() {
		this.productService = new ProductService();
	},
	mounted() {
		this.productService.getProductsSmall().then(data => this.products = data);
	},
	methods: {
		formatCurrency(value) {
			return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
		},
		menuToggle(event) {
			this.$refs.menu.toggle(event);
		}
	}
}
</script>

<style scoped>

</style>
