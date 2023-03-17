<template>
	<div id="product-list-one">
		<h2>Product list one</h2>
		<ul>
			<li v-for="(product, index) in saleProducts" v-bind:key="index">
				<span class="name">{{ product.name }}</span>
				<span class="price">${{ product.price }}</span>
			</li>
		</ul>
		<button v-on:click="reducePrice(4)">Reduce price</button>
	</div>
</template>

<script>
export default {
	computed: {
		products() {
			return this.$store.state.products;
		},
		saleProducts() {
			return this.$store.getters.saleProducts;
		},
	},
	methods: {
		reducePrice: function(amount) {
			// this.$store.commit("reducePrice");
			// better practice is to dispatch an action that commits the mutation itself
			// helps in tracking async code which is not possible when commiting mutation from
			// the methods themselves.
			this.$store.dispatch("reducePrice", amount);
		},
	},
};
</script>

<style scoped>
#product-list-one {
	background: #fff8b1;
	box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
	margin-bottom: 30px;
	padding: 10px 20px;
}
#product-list-one ul {
	padding: 0;
}
#product-list-one li {
	display: inline-block;
	margin-right: 10px;
	margin-top: 10px;
	padding: 20px;
	background: rgba(255, 255, 255, 0.7);
}
.price {
	font-weight: bold;
	color: #e8800c;
}
</style>
