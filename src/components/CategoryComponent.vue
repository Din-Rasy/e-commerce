<script setup>
const { name, imgSrc, productCount, color } = defineProps({
	name: {
		type: String,
		required: true
	},
	imgSrc: {
		type: String,
		default: ''
	},
	productCount: {
		type: [Number, String],
		default: 0
	},
	color: {
		type: String,
		default: '#ffffff'
	}
});

const resolveImage = (src) => {
	if (!src) return '';
	try {
		return new URL(src, import.meta.url).href;
	} catch {
		return src;
	}
};
</script>

<template>
	<div class="category-card" :style="{ backgroundColor: color }">
		<img v-if="imgSrc" :src="resolveImage(imgSrc)" :alt="name" />
		<div class="category-info">
			<strong class="name">{{ name }}</strong>
			<small class="count">{{ productCount }} items</small>
		</div>
	</div>
</template>

<style scoped>
.category-card {
	width: 100px;
	padding: 12px;
	border-radius: 12px;
	text-align: center;
	font-size: 13px;
	display: flex;
	flex-direction: column;
	align-items: center;

	box-shadow: 0 1px 2px rgba(0,0,0,0.05);
}
.category-card img {
	width: 64px;
	height: 64px;
	object-fit: cover;
	border-radius: 10px;
}
.category-info .name {
	display: block;
	margin-top: 2px;
}
.category-info .count {
	color: #7a7a7a;
}
</style>
