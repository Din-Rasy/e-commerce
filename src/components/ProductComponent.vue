<template>
  <div class="product-card">
    <span v-if="badge" class="product-badge" :class="badgeClass">{{ badge }}</span>

    <img :src="image" alt="Product Image" class="product-image" />

    <p class="product-category">{{ category }}</p>
    <h3 class="product-name">{{ name }}</h3>

    <div class="product-info">
      <span class="product-weight">{{ weight }}</span>
    </div>

    <div class="product-rating">
      ⭐⭐⭐⭐⭐ <span>(4.0)</span>
    </div>

    <div class="product-price">
      <strong class="new-price">${{ price }}</strong>
      <span v-if="oldPrice" class="old-price">${{ oldPrice }}</span>
    </div>

    <button class="add-btn">Add +</button>
  </div>
</template>

<script>
export default {
  name: "ProductComponent",
  props: {
    image: String,
    category: String,
    name: String,
    weight: String,
    price: Number,
    oldPrice: Number,
    badge: String,
  },
  computed: {
    badgeClass() {
      if (this.badge === "Hot") return "hot";
      if (this.badge === "Sale") return "sale";
      return "discount";
    },
  },
};
</script>

<style scoped>
.product-card {
  width: 230px;
  padding: 18px;
  border-radius: 14px;
  background: #fff;
  border: 1px solid #ececec;
  text-align: left;
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.product-card:hover {
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}

.product-image {
  width: 140px;
  height: 140px;
  object-fit: contain;
  align-self: center;
}

.product-badge {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 12px;
  padding: 4px 8px;
  border-radius: 6px;
  font-weight: 600;
  color: white;
}

.hot {
  background-color: #ff4757;
}

.sale {
  background-color: orange;
}

.discount {
  background-color: #3bb77e;
}

.product-category {
  font-size: 12px;
  color: #777;
}

.product-name {
  font-size: 15px;
  font-weight: 600;
  color: #222;
}

.product-rating {
  font-size: 13px;
  color: #ffb200;
}

.product-price {
  display: flex;
  align-items: center;
  gap: 8px;
}

.new-price {
  font-size: 18px;
  color: #3bb77e;
  font-weight: bold;
}

.old-price {
  text-decoration: line-through;
  font-size: 14px;
  color: #aaa;
}

.add-btn {
  width: 100%;
  margin-top: 10px;
  padding: 8px;
  background: #3bb77e;
  color: #fff;
  border-radius: 8px;
  border: none;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

.add-btn:hover {
  background: #329b69;
}
</style>
