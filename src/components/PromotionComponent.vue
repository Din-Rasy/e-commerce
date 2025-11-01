<script setup>
import ButtonComponent from './ButtonComponent.vue';

const { title, image, color, buttonColor, url, buttonText } = defineProps({
  title: { type: String, required: true },
  image: { type: String, default: '' },
  color: { type: String, default: '#ffffff' },
  buttonColor: { type: String, default: '#42B678' },
  url: { type: String, default: '#' },
  buttonText: { type: String, default: 'Shop Now' }
});

const resolveImage = (src) => {
  if (!src) return '';
  // If path is absolute (starts with '/') it's served from public/ and can be used directly
  if (src.startsWith('/')) return src;
  try {
    return new URL(src, import.meta.url).href;
  } catch {
    return src;
  }
};

const promotion = { title, image, color, buttonColor, url };

const shopNow = (promo) => {

  if (promo && promo.title) {
    window.alert("Let's shop: " + promo.title);
  } else {
    window.alert("Let's shop!");
  }
};
</script>

<template>
  <div class="promotion-card" :style="{ backgroundColor: color }">
    <div class="promo-content">
      <h3 class="promo-title">{{ title }}</h3>
      <ButtonComponent :btnText="buttonText" :btnColor="buttonColor" @click="shopNow(promotion)" />
    </div>
    <div class="promo-image" v-if="image">
      <img :src="resolveImage(image)" :alt="title" />
    </div>
  </div>
</template>

<style scoped>
.promotion-card {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
  border-radius: 12px;
  min-width: 280px;
  flex: 1 1 320px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.05);
}
.promo-content {
  max-width: 60%;
}
.promo-title {
  font-size: 18px;
  margin: 0 0 12px 0;
}
.promo-image img {
  max-width: 140px;
  height: auto;
  border-radius: 8px;
}
a { text-decoration: none; }
</style>
