<template>
	<div class="p-grid">
		<div class="p-col-12">
			<div class="card">
				<h4>My Transformers</h4>
				<p>Check the transformers you have submitted to improve the efficiency of this brain.</p>
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
					<Column headerStyle="width: 8rem; text-align: center" bodyStyle="text-align: center; overflow: visible">
						<template #body>
							<Button type="button" icon="pi pi-cog" class="p-button-secondary"></Button>
						</template>
					</Column>
				</DataTable>
			</div>
		</div>
		<div class="p-col-12">
			<div class="card">
				<h4>Customized</h4>
				<p>Scrollable table with gridlines (<mark>.p-datatable-gridlines</mark>), striped rows (<mark>.p-datatable-striped</mark>) and smaller paddings (<mark>p-datatable-sm</mark>).</p>
				<DataTable :value="customer2" :paginator="true" class="p-datatable-striped p-datatable-sm p-datatable-responsive p-datatable-gridlines p-datatable-customers"
							:rows="10" dataKey="id" :rowHover="true" v-model:selection="selectedCustomers2" :filters="filters2" :loading="loading2">
					<template #header>
						<div class="table-header p-d-flex p-flex-column p-flex-md-row p-jc-md-between">
							Customers
							<span class="p-input-icon-left">
							<i class="pi pi-search"/>
							<InputText v-model="filters2['global']" placeholder="Search"/>
						</span>
						</div>
					</template>

					<template #empty>
						No customers found.
					</template>
					<template #loading>
						Loading customers data. Please wait.
					</template>

					<Column field="name" header="Name" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Name</span>
							{{slotProps.data.name}}
						</template>
					</Column>
					<Column header="Country" :sortable="true" sortField="country.name" filterField="country.name">
						<template #body="slotProps">
							<span class="p-column-title">Country</span>
							<span :class="'flag flag-' + slotProps.data.country.code" style="width: 30px; height: 20px"/>
							<span style="vertical-align: middle; margin-left: .5em">{{slotProps.data.country.name}}</span>
						</template>
					</Column>
					<Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name">
						<template #body="slotProps">
							<span class="p-column-title">Representative</span>
							<img :alt="slotProps.data.representative.name" :src="'assets/demo/images/avatar/' + slotProps.data.representative.image" width="32" style="vertical-align: middle"/>
							<span style="vertical-align: middle; margin-left: .5em">{{slotProps.data.representative.name}}</span>
						</template>
					</Column>
					<Column field="date" header="Join Date" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Join Date</span>
							<span>{{slotProps.data.date}}</span>
						</template>
					</Column>
					<Column field="status" header="Status" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Status</span>
							<span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
						</template>
					</Column>
					<Column field="activity" header="Activity" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Activity</span>
							<ProgressBar :value="slotProps.data.activity" :showValue="false"/>
						</template>
					</Column>
				</DataTable>
			</div>
		</div>

		<div class="p-col-12">
			<div class="card">
				<h4>Row Expand</h4>

				<Toast />
				<DataTable :value="products" class="p-datatable-customers" v-model:expandedRows="expandedRows" dataKey="id" @row-expand="onRowExpand" @row-collapse="onRowCollapse">
					<template #header>
						<div class="table-header-container">
							<Button icon="pi pi-plus" label="Expand All" @click="expandAll" class="p-mr-2 p-mb-2" />
							<Button icon="pi pi-minus" label="Collapse All" @click="collapseAll" class="p-mb-2" />
						</div>
					</template>
					<Column :expander="true" headerStyle="width: 3rem" />
					<Column field="name" header="Name" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Name</span>
							{{slotProps.data.name}}
						</template>
					</Column>
					<Column header="Image">
						<template #body="slotProps">
							<span class="p-column-title">Image</span>
							<img :src="'assets/demo/images/product/' + slotProps.data.image" :alt="slotProps.data.image" class="product-image" />
						</template>
					</Column>
					<Column field="price" header="Price" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Price</span>
							{{formatCurrency(slotProps.data.price)}}
						</template>
					</Column>
					<Column field="category" header="Category" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Category</span>
							{{slotProps.data.category}}
						</template>
					</Column>
					<Column field="rating" header="Reviews" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Reviews</span>
							<Rating :modelValue="slotProps.data.rating" :readonly="true" :cancel="false" />
						</template>
					</Column>
					<Column field="inventoryStatus" header="Status" :sortable="true">
						<template #body="slotProps">
							<span class="p-column-title">Status</span>
							<span :class="'product-badge status-' + (slotProps.data.inventoryStatus ? slotProps.data.inventoryStatus.toLowerCase() : '')">{{slotProps.data.inventoryStatus}}</span>
						</template>
					</Column>
					<template #expansion="slotProps">
						<div class="orders-subtable">
							<h5>Orders for {{slotProps.data.name}}</h5>
							<DataTable :value="slotProps.data.orders">
								<Column field="id" header="Id" :sortable="true">
									<template #body="slotProps">
										<span class="p-column-title">Id</span>
										{{slotProps.data.id}}
									</template>
								</Column>
								<Column field="customer" header="Customer" :sortable="true">
									<template #body="slotProps">
										<span class="p-column-title">Customer</span>
										{{slotProps.data.customer}}
									</template>
								</Column>
								<Column field="date" header="Date" :sortable="true">
									<template #body="slotProps">
										<span class="p-column-title">Date</span>
										<span>{{slotProps.data.date}}</span>
									</template>
								</Column>
								<Column field="amount" header="Amount" :sortable="true">
									<template #body="slotProps" :sortable="true">
										<span class="p-column-title">Amount</span>
										{{formatCurrency(slotProps.data.amount)}}
									</template>
								</Column>
								<Column field="status" header="Status" :sortable="true">
									<template #body="slotProps">
										<span class="p-column-title">Status</span>
										<span :class="'order-badge order-' + (slotProps.data.status ? slotProps.data.status.toLowerCase() : '')">{{slotProps.data.status}}</span>
									</template>
								</Column>
								<Column headerStyle="width:4rem">
									<template #body>
										<Button icon="pi pi-search" />
									</template>
								</Column>
							</DataTable>
						</div>
					</template>
				</DataTable>
			</div>
		</div>

		<div class="p-col-12">
			<div class="card">
				<h4>Row Group</h4>
				<DataTable :value="customer3" class="p-datatable-customers" rowGroupMode="subheader" groupRowsBy="representative.name" sortMode="single" sortField="representative.name" :sortOrder="1">
					<Column field="representative.name" header="Representative">
						<template #body="slotProps">
							<span class="p-column-title">Representative</span>
							<span>{{slotProps.data.representative}}</span>
						</template>
					</Column>
					<Column field="name" header="Name">
						<template #body="slotProps">
							<span class="p-column-title">Name</span>
							<span>{{slotProps.data.name}}</span>
						</template>
					</Column>
					<Column field="country" header="Country">
						<template #body="slotProps">
							<span class="p-column-title">Country</span>
							<img src="assets/demo/flags/flag_placeholder.png" :class="'flag flag-' + slotProps.data.country.code" width="30" />
							<span style="margin-left: .5em; vertical-align: middle" class="image-text">{{slotProps.data.country.name}}</span>
						</template>
					</Column>
					<Column field="company" header="Company">
						<template #body="slotProps">
							<span class="p-column-title">Company</span>
							<span>{{slotProps.data.company}}</span>
						</template>
					</Column>
					<Column field="status" header="Status">
						<template #body="slotProps">
							<span class="p-column-title">Status</span>
							<span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
						</template>
					</Column>
					<Column field="date" header="Date">
						<template #body="slotProps">
							<span class="p-column-title">Date</span>
							<span>{{slotProps.data.date}}</span>
						</template>
					</Column>
					<template #groupheader="slotProps">
						<img :alt="slotProps.data.representative.name" :src="'assets/demo/images/avatar/' + slotProps.data.representative.image" width="32" style="vertical-align: middle" />
						<span style="margin-left: .5em; vertical-align: middle" class="image-text">{{slotProps.data.representative.name}}</span>
					</template>
					<template #groupfooter="slotProps">
						<td colspan="4" class="p-text-bold" style="text-align: right">Total Customers</td>
						<td class="p-text-bold">{{calculateCustomerTotal(slotProps.data.representative.name)}}</td>
					</template>
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