<template>
	<div class="p-grid">
		<div class="p-col-12">
			<div class="card">
				<h4>My Transformers</h4>
				<p>Check the transformers you have submitted to improve the efficiency of this brain.</p>
				<DataTable :value="customer1" :paginator="true" class="p-datatable-customers" :rows="10" dataKey="id" :rowHover="true" v-model:selection="selectedCustomers1"
						:filters="filters1" :loading="loading1">
					<template #header>
						<div class="table-header p-d-flex p-flex-column p-flex-md-row p-jc-md-between">
							Create new transformer
							<span class="p-input-icon-left">
								<router-link to="/transformers/new">
									<Button label="New Transformer" class="p-mr-2 p-mb-2"></Button>
								</router-link>
              </span>
						</div>
					</template>
					<template #empty>
						No transformers found.
					</template>
					<template #loading>
						Loading transformers data. Please wait.
					</template>
					<Column field="name" header="Name" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Name</span>
							{{slotProps.data.name}}
						</template>
					</Column>
					<Column field="date" header="Date" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Date</span>
							<span>{{slotProps.data.date}}</span>
						</template>
					</Column>
					<Column field="status" header="Status" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Status</span>
							<span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
						</template>
					</Column>
					<Column field="activity" header="Score" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Score</span>
							<ProgressBar :value="slotProps.data.activity" :showValue="false" />
						</template>
					</Column>
					<Column headerStyle="width: 8rem; text-align: center" bodyStyle="text-align: center; overflow: visible">
						<template #body>
							<Button type="button" icon="pi pi-search" class="p-button-secondary"></Button>
						</template>
					</Column>
				</DataTable>
			</div>
		</div>
		<div class="p-col-12">
			<div class="card">
				<h4>Ranked Transformers</h4>
				<p>Check all the transformers sorted by their score (importance to achieve brain efficiency).</p>
				<DataTable :value="customer1" :paginator="true" class="p-datatable-customers" :rows="10" dataKey="id" :rowHover="true" v-model:selection="selectedCustomers1"
						:filters="filters1" :loading="loading1">
					<template #empty>
						No transformers found.
					</template>
					<template #loading>
						Loading transformers data. Please wait.
					</template>
					<Column field="name" header="Name" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Name</span>
							{{slotProps.data.name}}
						</template>
					</Column>
					<Column field="date" header="Date" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Date</span>
							<span>{{slotProps.data.date}}</span>
						</template>
					</Column>
					<Column field="status" header="Status" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Status</span>
							<span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
						</template>
					</Column>
					<Column field="activity" header="Score" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Score</span>
							<ProgressBar :value="slotProps.data.activity" :showValue="false" />
						</template>
					</Column>
				</DataTable>
			</div>
		</div>
	</div>
</template>

<script>
	import CustomerService from "../service/CustomerService";
	import ProductService from '../service/ProductService';

	export default {
		data() {
			return {
				customer1: null,
				customer2: null,
				customer3: null,
				selectedCustomers1: null,
				selectedCustomers2: null,
				filters1: {},
				filters2: {},
				loading1: true,
				loading2: true,
				products: null,
				expandedRows: []
			}
		},
		customerService: null,
		productService: null,
		created() {
			this.customerService = new CustomerService();
			this.productService = new ProductService();
		},
		mounted() {
			this.productService.getProductsWithOrdersSmall().then(data => this.products = data);
			this.customerService.getCustomersMedium().then(data => this.customer1 = data);
			this.customerService.getCustomersLarge().then(data => this.customer2 = data);
			this.customerService.getCustomersMedium().then(data => this.customer3 = data);
			this.loading1 = false;
			this.loading2 = false;
		},
		methods: {
			onRowExpand(event) {
				this.$toast.add({severity: 'info', summary: 'Product Expanded', detail: event.data.name, life: 3000});
			},
			onRowCollapse(event) {
				this.$toast.add({severity: 'success', summary: 'Product Collapsed', detail: event.data.name, life: 3000});
			},
			expandAll() {
				this.expandedRows = this.products.filter(p => p.id);
				this.$toast.add({severity: 'success', summary: 'All Rows Expanded', life: 3000});
			},
			collapseAll() {
				this.expandedRows = null;
				this.$toast.add({severity: 'success', summary: 'All Rows Collapsed', life: 3000});
			},
			formatCurrency(value) {
				return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
			},
			calculateCustomerTotal(name) {
				let total = 0;

				if (this.customer3) {
					for (let customer of this.customer3) {
						if (customer.representative.name === name) {
							total++;
						}
					}
				}

				return total;
			}
		}
	}
</script>

<style scoped lang="scss">
::v-deep(.p-progressbar) {
	height: .5rem;
	background-color: #D8DADC;

	.p-progressbar-value {
		background-color: #607D8B;
	}
}

.p-datatable .p-column-filter {
	display: none;
}

.table-header {
	display: flex;
	justify-content: space-between;
}

::v-deep(.p-datatable.p-datatable-customers) {
	.p-datatable-header {
		padding: 1rem;
		text-align: left;
		font-size: 1.5rem;
	}

	.p-paginator {
		padding: 1rem;
	}

	.p-datatable-thead > tr > th {
		text-align: left;
	}

	.p-datatable-tbody > tr > td {
		cursor: auto;
	}

	.p-dropdown-label:not(.p-placeholder) {
		text-transform: uppercase;
	}
}

/* Responsive */
.p-datatable-customers .p-datatable-tbody > tr > td .p-column-title {
	display: none;
}

.customer-badge {
	border-radius: 2px;
	padding: .25em .5rem;
	text-transform: uppercase;
	font-weight: 700;
	font-size: 12px;
	letter-spacing: .3px;

	&.status-qualified {
		background: #C8E6C9;
		color: #256029;
	}

	&.status-unqualified {
		background: #FFCDD2;
		color: #C63737;
	}

	&.status-negotiation {
		background: #FEEDAF;
		color: #8A5340;
	}

	&.status-new {
		background: #B3E5FC;
		color: #23547B;
	}

	&.status-renewal {
		background: #ECCFFF;
		color: #694382;
	}

	&.status-proposal {
		background: #FFD8B2;
		color: #805B36;
	}
}

.p-progressbar-value.ui-widget-header {
	background: #607d8b;
}

@media (max-width: 640px) {
	.p-progressbar {
		margin-top: .5rem;
	}
}

.product-image {
	width: 100px;
	box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23)
}

.orders-subtable {
	padding: 1rem;
}

.product-badge {
	border-radius: 2px;
	padding: .25em .5rem;
	text-transform: uppercase;
	font-weight: 700;
	font-size: 12px;
	letter-spacing: .3px;

	&.status-instock {
		background: #C8E6C9;
		color: #256029;
	}

	&.status-outofstock {
		background: #FFCDD2;
		color: #C63737;
	}

	&.status-lowstock {
		background: #FEEDAF;
		color: #8A5340;
	}
}

.order-badge {
	border-radius: 2px;
	padding: .25em .5rem;
	text-transform: uppercase;
	font-weight: 700;
	font-size: 12px;
	letter-spacing: .3px;

	&.order-delivered {
		background: #C8E6C9;
		color: #256029;
	}

	&.order-cancelled {
		background: #FFCDD2;
		color: #C63737;
	}

	&.order-pending {
		background: #FEEDAF;
		color: #8A5340;
	}

	&.order-returned {
		background: #ECCFFF;
		color: #694382;
	}
}

@media screen and (max-width: 960px) {
	::v-deep(.p-datatable) {
		&.p-datatable-customers {
			.p-datatable-thead > tr > th,
			.p-datatable-tfoot > tr > td {
				display: none !important;
			}

			.p-datatable-tbody > tr {
				border-bottom: 1px solid var(--surface-d);

				> td {
					text-align: left;
					display: block;
					border: 0 none !important;
					width: 100% !important;
					float: left;
					clear: left;
					border: 0 none;

					.p-column-title {
						padding: .4rem;
						min-width: 30%;
						display: inline-block;
						margin: -.4rem 1rem -.4rem -.4rem;
						font-weight: bold;
					}

					.p-progressbar {
						margin-top: .5rem;
						display: inline-block;
						width: 60%;
					}
					.p-rating {
						display: inline-block;
					}
				}
			}

			.p-datatable-tbody > tr.p-rowgroup-footer{
				display: flex;
			}
		}
	}
}
</style>
