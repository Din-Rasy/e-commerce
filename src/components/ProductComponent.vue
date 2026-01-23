<template>
  <div class="product-card">
    <span v-if="computedBadge" class="product-badge" :class="badgeClass">{{ computedBadge }}</span>

    <img :src="image" alt="Product Image" class="product-image" />

    <div class="product-brand">Hodo Foods</div>
    <h3 class="product-name">{{ name }}</h3>

    <div class="product-rating">
      ⭐⭐⭐⭐ <span>{{ displayRating }}</span>
    </div>

    <div class="product-size">{{ displayWeight }}</div>

    <div class="product-price">
      <strong class="new-price">${{ price }}</strong>
      <span v-if="computedOldPrice" class="old-price">${{ computedOldPrice }}</span>
    </div>

    <div class="quantity-controls" v-if="quantity > 0">
      <button class="quantity-btn minus" @click="decreaseQuantity">−</button>
      <span class="quantity-number">{{ quantity }}</span>
      <button class="quantity-btn plus" @click="increaseQuantity">+</button>
    </div>

    <button class="add-btn" v-else @click="addToCart">Add +</button>
  </div>
</template>

<script>
export default {
  name: "ProductComponent",
  props: {
    image: String,
    category: String,
    name: String,
    size: String,
    price: Number,
    oldPrice: Number,
    badge: String,
    rating: Number,
    promotionAsPercentage: Number,
  },
  data() {
    return {
      quantity: 0,
    };
  },
  computed: {
    badgeClass() {
      if (this.badge === "Hot") return "hot";
      if (this.badge === "Sale") return "sale";
      return "discount";
    },
    computedBadge() {
      if (this.promotionAsPercentage) {
        return `-${this.promotionAsPercentage}%`;
      }
      return this.badge;
    },
    computedOldPrice() {
      if (this.promotionAsPercentage && this.price) {
        return (this.price / (1 - this.promotionAsPercentage / 100)).toFixed(2);
      }
      return this.oldPrice;
    },
    displayWeight() {
      return this.size || this.weight || '500g';
    },
    displayCategory() {
      return this.category || 'General';
    },
    displayRating() {
      return this.rating || 4.0;
    }
  },
  methods: {
    addToCart() {
      this.quantity = 1;
      this.$emit('add-to-cart', {
        id: this.name,
        name: this.name,
        price: this.price,
        quantity: 1,
        image: this.image
      });
    },
    increaseQuantity() {
      this.quantity++;
      this.$emit('update-quantity', {
        id: this.name,
        name: this.name,
        price: this.price,
        quantity: this.quantity,
        image: this.image
      });
    },
    decreaseQuantity() {
      if (this.quantity > 1) {
        this.quantity--;
        this.$emit('update-quantity', {
          id: this.name,
          name: this.name,
          price: this.price,
          quantity: this.quantity,
          image: this.image
        });
      } else {
        this.quantity = 0;
        this.$emit('remove-from-cart', {
          id: this.name,
          name: this.name,
          price: this.price,
          quantity: 0,
          image: this.image
        });
      }
    }
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
  gap: 8px;
}

.product-card:hover {
  box-shadow: 0 4px 20px rgba(0,0,0,0.06);
}

.product-image {
  width: 140px;
  height: 140px;
  object-fit: contain;
  align-self: center;
  border-radius: 8px;
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

.product-brand {
  font-size: 11px;
  color: #666;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.product-name {
  font-size: 14px;
  font-weight: 600;
  color: #222;
  line-height: 1.3;
  margin: 0;
}

.product-rating {
  font-size: 12px;
  color: #ffb200;
  display: flex;
  align-items: center;
  gap: 4px;
}

.product-size {
  font-size: 12px;
  color: #666;
  font-weight: 500;
}

.product-price {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: auto;
}

.new-price {
  font-size: 16px;
  color: #3bb77e;
  font-weight: bold;
}

.old-price {
  text-decoration: line-through;
  font-size: 13px;
  color: #aaa;
}

.add-btn {
  width: 100%;
  margin-top: 12px;
  padding: 10px;
  background: #3bb77e;
  color: #fff;
  border-radius: 8px;
  border: none;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
  font-size: 14px;
}

.add-btn:hover {
  background: #329b69;
}

.quantity-controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 12px;
  padding: 0;
  background: none;
  border-radius: 8px;
  border: 1px solid #3bb77e;
  height: 40px;
  width: 90px;
  margin-left: auto;
}

.quantity-btn {
  width: 30px;
  height: 100%;
  border: none;
  background: none;
  color: #3bb77e;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  border-radius: 0;
}

.quantity-btn:hover {
  background: #e6f4ee;
  transform: none;
}

.quantity-btn.minus {
  background: none;
  color: #3bb77e;
}

.quantity-btn.minus:hover {
  background: #e6f4ee;
}

.quantity-number {
  font-size: 16px;
  font-weight: 600;
  color: #333;
  min-width: 20px;
  text-align: center;
  flex-grow: 1;
}

.add-btn {
  width: 90px;
  height: 40px;
  margin-left: auto;
  background: #3bb77e;
  color: white;
  border-radius: 8px;
  border: none;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
  font-size: 14px;
}
</style>
