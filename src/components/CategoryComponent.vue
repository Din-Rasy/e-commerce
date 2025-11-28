<template>
  <div class="category-card" :style="{ backgroundColor: color }">
    <img :src="image" :alt="name" class="category-image" />
    <h3 class="category-name">{{ name }}</h3>
    <p class="product-count">{{ productCount }} items</p>
  </div>
</template>

<script>
export default {
  name: 'CategoryComponent',
  props: {
    name: {
      type: String,
      required: true,
    },
    productCount: {
      type: Number,
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
  },
}
</script>

<!-- <style scoped>
.category-card {
  border-radius: 8px;
  padding: 10px;
  text-align: center;
  width: 100px;
  height: 140px;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  box-sizing: border-box;
  overflow: hidden;
  flex-shrink: 0;
}


.category-image {
  width: 100%;
  max-width: 70px;
  height: 60px;
  object-fit: contain;
  margin-bottom: 8px;
  flex-shrink: 0;
}

.category-name {
  margin: 0;
  font-size: 11px;
  font-weight: 600;
  color: #333;
  line-height: 1.3;
  word-wrap: break-word;
  overflow-wrap: break-word;
  max-height: 2.6em;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
}

.product-count {
  margin: 4px 0 0 0;
  font-size: 10px;
  color: #666;
}
</style>
 -->
<style scoped>
.category-card {
  width: 200px;
  height: 220px;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 3px 12px rgba(0,0,0,0.08);
  padding: 12px;
  text-align: center;
  transition: transform 0.25s ease, box-shadow 0.25s ease;
}

.category-card:hover {
  transform: scale(1.06);
  box-shadow: 0 6px 20px rgba(0,0,0,0.12);
}

.category-image {
  width: 90%;
  height: 120px;
  object-fit: contain;
  margin-bottom: 10px;
}

.category-name {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 6px;
}

.category-count {
  font-size: 0.9rem;
  color: #666;
}
</style>

