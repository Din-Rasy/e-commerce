<script setup>
const { btnText, btnColor } = defineProps({
	btnText: {
		type: String,
		default: 'Shop Now'
	},
	btnColor: {
		type: String,
		default: '#3BB77E'
	}
});
const emit = defineEmits(['click']);
const handleClick = (e) => {
	emit('click', e);
};
</script>

<template>
	<button class="btn" :style="{ backgroundColor: btnColor }" @click="handleClick">
		<span>{{ btnText }}</span>
	</button>
</template>

<style scoped>
.btn {
	color: white;
	padding: 8px 14px;
	border: none;
	border-radius: 6px;
	cursor: pointer;
	font-weight: 600;
}
</style>


