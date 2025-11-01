<script>
import CategoryComponent from './components/CategoryComponent.vue';
import PromotionComponent from './components/PromotionComponent.vue';

export default {
	name: 'App',
	components: {
		CategoryComponent,
		PromotionComponent
	},
	data() {
		return {
					categories: [
						{ name: 'Cake & Milk', productCount: 34, color: '#F8FFF2', image: '/img/Cake and Milk.png' },
						{ name: 'Peach', productCount: 17, color: '#FEFBE8', image: '/img/Peach.png' },
						{ name: 'Oganic Kiwi', productCount: 21, color: '#F0FFF4', image: '/img/Oganic Kiwi.png' },
						{ name: 'Red Apple', productCount: 68, color: '#FFF0E9', image: '/img/Red Apple.png' },
						{ name: 'Snack', productCount: 34, color: '#FEF4EB', image: '/img/Snack.png' },
						{ name: 'Black plum', productCount: 25, color: '#FFF8F8', image: '/img/Black plum.png' },
						{ name: 'Vegetables', productCount: 65, color: '#F0FFF0', image: '/img/Vegetanles.png' },
						{ name: 'Headphone', productCount: 33, color: '#FFF7FF', image: '/img/Headphone.png' },
						{ name: 'Cake & Milk (alt)', productCount: 54, color: '#F9FFF6', image: '/img/Cake and Milk 1.png' },
						{ name: 'Orange', productCount: 63, color: '#FFF9F2', image: '/img/Orange.png' }
					],
			promotions: [
						{
							title: 'Everyday Fresh and Clean with Our Products',
							color: '#F0E9D7',
							image: '/Onion.jpg',
							buttonColor: '#42B678',
							url: '/promotions/1'
						},
						{
							title: 'Make your Breakfast Healthy and Easy',
							color: '#F2E8E9',
							image: '/Strawberry.png',
							buttonColor: '#42B678',
							url: '/promotions/2'
						},
						{
							title: 'The best Organic Products Online',
							color: '#E6EAF3',
							image: '/Organic Porduct.jpg',
							buttonColor: '#FBC040',
							url: '/promotions/3'
						}
			]
		};
	}
};
</script>

<template>
	<main>
		<h1>This is my first VueJs project</h1>

		<h2>Categories</h2>
		<div class="category-container">
			<CategoryComponent
				v-for="category in categories"
				:key="category.name"
				:name="category.name"
				:imgSrc="category.image"
				:productCount="category.productCount"
				:style="{ backgroundColor: category.color }"
			/>
		</div>

		<h2>Promotions</h2>
		<div class="promotion-container">
			<PromotionComponent
				v-for="(promo, idx) in promotions"
				:key="promo.title || idx"
				:title="promo.title"
				:image="promo.image"
				:color="promo.color"
				:buttonColor="promo.buttonColor"
				:url="promo.url"
				buttonText="Shop Now"
			/>
		</div>
	</main>
</template>

<style>
main {
	padding: 20px;
	font-family: sans-serif;
}

.category-container,
.promotion-container {
	display: flex;
	flex-wrap: wrap;
	gap: 15px;
}

h2 {
	margin-top: 30px;
}
</style>
