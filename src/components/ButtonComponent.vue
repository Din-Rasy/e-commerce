<template>
  <button class="shop-now-button" :style="{ backgroundColor: color }" @click="$emit('click')">
    <slot>Shop Now →</slot>
  </button>
</template>

<script>
export default {
  name: 'ButtonComponent',
  props: {
    color: {
      type: String,
      default: '#42B678',
    },
  },
}
</script>

<style scoped>
.shop-now-button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  transition: opacity 0.2s, transform 0.2s;
  width: fit-content;
  white-space: nowrap;
}

.shop-now-button:hover {
  opacity: 0.9;
  transform: scale(1.05);
}

.shop-now-button:active {
  transform: scale(0.98);
}
</style>
