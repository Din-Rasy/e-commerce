<template>
  <div class="promotion-banner" :style="{ backgroundColor: color }">
    <div class="promotion-content">
      <h2 class="promotion-title">{{ title }}</h2>
      <ButtonComponent :color="buttonColor" @click="shopNow(promotion)">
        Shop Now →
      </ButtonComponent>
    </div>
    <div class="promotion-image-container" :style="imageContainerStyle">
      <img :src="image" :alt="title" class="promotion-image" :style="imageStyle" />
    </div>
  </div>
</template>

<script>
import ButtonComponent from './ButtonComponent.vue'
export default {
  name: 'PromotionComponent',
  components: { ButtonComponent },
  props: {
    title: {
      type: String,
      required: true,
    },
    color: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
    buttonColor: {
      type: String,
      required: true,
    },
    url: {
      type: String,
      required: true,
    },
    imageContainerWidth: {
      type: String,
      default: '100px',
    },
    imageContainerHeight: {
      type: String,
      default: '100%',
    },
    imageWidth: {
      type: String,
      default: '100%',
    },
    imageHeight: {
      type: String,
      default: '100%',
    },
    imageMaxHeight: {
      type: String,
      default: '160px',
    },
    imageObjectFit: {
      type: String,
      default: 'contain',
    },
  },
  computed: {
    promotion() {
      return {
        title: this.title,
        url: this.url,
      }
    },
    imageContainerStyle() {
      return {
        width: this.imageContainerWidth,
        height: this.imageContainerHeight,
      }
    },
    imageStyle() {
      return {
        width: this.imageWidth,
        height: this.imageHeight,
        maxHeight: this.imageMaxHeight,
        objectFit: this.imageObjectFit,
      }
    },
  },
  methods: {
    shopNow(promotion) {
      alert("Let's shop: " + promotion.title)
    },
  },
}
</script>

<style scoped>
.promotion-banner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-radius: 8px;
  width: 360px;
  height: 180px;
  gap: 12px;
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
  flex-shrink: 0;
}

.promotion-content {
  flex: 1;
  z-index: 2;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-width: 0;
}

.promotion-title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-bottom: 12px;
  line-height: 1.4;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

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


.promotion-image-container {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}
</style>

