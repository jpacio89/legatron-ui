<template>
    <div class="p-grid p-fluid">
        <div class="p-col-12">
            <div class="card">
                <h5>Carousel</h5>
                <Carousel :value="products" :numVisible="3" :numScroll="3" :circular="false" :responsiveOptions="carouselResponsiveOptions">
                    <template #item="product">
                        <div class="product-item">
                            <div class="product-item-content">
                                <div class="p-mb-3">
                                    <img :src="'assets/demo/images/product/' + product.data.image" :alt="product.data.name" class="product-image" />
                                </div>
                                <div>
                                    <h4 class="p-mb-1">
                                        {{ product.data.name }}
                                    </h4>
                                    <h6 class="p-mt-0 p-mb-3">${{ product.data.price }}</h6>
                                    <span :class="'product-badge status-' + product.data.inventoryStatus.toLowerCase()">{{ product.data.inventoryStatus }}</span>
                                    <div class="car-buttons p-mt-5">
                                        <Button type="button" class="p-button p-button-rounded p-mr-2" icon="pi pi-search"></Button>
                                        <Button type="button" class="p-button-success p-button-rounded p-mr-2" icon="pi pi-star"></Button>
                                        <Button type="button" class="p-button-help p-button-rounded" icon="pi pi-cog"></Button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </template>
                </Carousel>
            </div>
        </div>

        <div class="p-col-12">
            <div class="card">
                <h5>Galleria</h5>
                <Galleria :value="images" :responsiveOptions="galleriaResponsiveOptions" :numVisible="7" :circular="true" containerStyle="max-width: 800px; margin: auto">
                    <template #item="slotProps">
                        <img :src="'assets/' + slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
                    </template>
                    <template #thumbnail="slotProps">
                        <img :src="'assets/' + slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" tyle="width: 100%; display: block;" />
                    </template>
                </Galleria>
            </div>
        </div>
    </div>
</template>

<script>
import ProductService from "../service/ProductService";
import PhotoService from "../service/PhotoService";
export default {
    data() {
        return {
            products: [],
            images: [],
            galleriaResponsiveOptions: [
                {
                    breakpoint: "1024px",
                    numVisible: 5,
                },
                {
                    breakpoint: "960px",
                    numVisible: 4,
                },
                {
                    breakpoint: "768px",
                    numVisible: 3,
                },
                {
                    breakpoint: "560px",
                    numVisible: 1,
                },
            ],
            carouselResponsiveOptions: [
                {
                    breakpoint: "1024px",
                    numVisible: 3,
                    numScroll: 3,
                },
                {
                    breakpoint: "768px",
                    numVisible: 2,
                    numScroll: 2,
                },
                {
                    breakpoint: "560px",
                    numVisible: 1,
                    numScroll: 1,
                },
            ],
        };
    },
    created() {
        this.productService = new ProductService();
        this.photoService = new PhotoService();
    },
    mounted() {
        this.productService.getProductsSmall().then((products) => {
            this.products = products;
        });
        this.photoService.getImages().then((images) => {
            this.images = images;
        });
    },
};
</script>

<style lang="scss" scoped>
.product-item {
    .product-item-content {
        border: 1px solid var(--surface-d);
        border-radius: 3px;
        margin: 0.3rem;
        text-align: center;
        padding: 2rem 0;
    }
    .product-image {
        width: 50%;
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    }
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
</style>