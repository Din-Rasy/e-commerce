<template>
  <div class="product-view">
    <!-- Search Box with Logo and Account Links -->
    <SearchBoxComponent />

    <!-- Main Navigation Menu -->
    <MenuItemComponent />

    <!-- Page Header -->
    <div class="page-header">
      <div class="breadcrumb">
        <router-link to="/" class="breadcrumb-link">Home</router-link>
        <span class="breadcrumb-separator">></span>
        <router-link to="/categories" class="breadcrumb-link">Categories</router-link>
        <span class="breadcrumb-separator">></span>
        <router-link :to="`/categories/${product.category?._id}`" class="breadcrumb-link">{{ categoryName }}</router-link>
        <span class="breadcrumb-separator">></span>
        <span class="breadcrumb-current">{{ product.name }}</span>
      </div>
    </div>

    <!-- Product Details -->
    <div v-if="!loading && !error" class="product-detail">
      <div class="product-container">
        <!-- Product Images -->
        <div class="product-images">
          <div class="main-image">
            <img :src="product.image" :alt="product.name" />
          </div>
          <div v-if="productImages.length > 1" class="thumbnail-images">
            <img
              v-for="(image, index) in productImages"
              :key="index"
              :src="image"
              :alt="`${product.name} ${index + 1}`"
              @click="setMainImage(image)"
              :class="{ active: currentMainImage === image }"
            />
          </div>
        </div>

        <!-- Product Info -->
        <div class="product-info">
          <h1 class="product-name">{{ product.name }}</h1>

          <div class="product-rating">
            <span class="stars">★★★★★</span>
            <span class="rating-value">{{ product.rating }}/5.0</span>
          </div>

          <div class="product-price">
            <span class="current-price">${{ product.price }}</span>
            <span v-if="product.oldPrice" class="old-price">${{ product.oldPrice }}</span>
            <span v-if="product.promotionAsPercentage" class="discount">-{{ product.promotionAsPercentage }}%</span>
          </div>

          <div class="product-meta">
            <div v-if="product.weight" class="meta-item">
              <span class="meta-label">Weight:</span>
              <span class="meta-value">{{ product.weight }}</span>
            </div>
            <div v-if="product.size" class="meta-item">
              <span class="meta-label">Size:</span>
              <span class="meta-value">{{ product.size }}</span>
            </div>
            <div v-if="product.category" class="meta-item">
              <span class="meta-label">Category:</span>
              <span class="meta-value">{{ product.category.name }}</span>
            </div>
          </div>

          <div class="product-actions">
            <div class="quantity-selector">
              <button @click="decreaseQuantity" :disabled="quantity <= 1">-</button>
              <input v-model.number="quantity" type="number" min="1" max="99" />
              <button @click="increaseQuantity" :disabled="quantity >= 99">+</button>
            </div>
            <button class="add-to-cart-btn" @click="addToCart">
              Add to Cart
            </button>
          </div>

          <div v-if="product.description" class="product-description">
            <h3>Description</h3>
            <p>{{ product.description }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Loading state -->
    <div v-if="loading" class="loading">
      Loading product details...
    </div>

    <!-- Error state -->
    <div v-if="error" class="error">
      {{ error }}
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBoxComponent from "../components/searchBoxComponent.vue";
import MenuItemComponent from "../components/MenuItemComponent.vue";

export default {
  name: "ProductView",
  components: {
    SearchBoxComponent,
    MenuItemComponent,
  },
  data() {
    return {
      product: {},
      productImages: [],
      currentMainImage: "",
      categoryName: "",
      quantity: 1,
      loading: false,
      error: null,
    };
  },
  methods: {
    async fetchProductDetails() {
      const productId = this.$route.params.productId;
      this.loading = true;
      this.error = null;

      try {
        // Fetch product details
        const res = await axios.get(`http://localhost:3000/api/products/${productId}`);
        this.product = res.data;

        // Process images
        if (this.product.image) {
          try {
            const images = JSON.parse(this.product.image);
            if (Array.isArray(images)) {
              this.productImages = images.map(img => "http://localhost:3000/" + img.replace(/\\/g, "/"));
            } else {
              this.productImages = ["http://localhost:3000/" + this.product.image.replace(/\\/g, "/")];
            }
          } catch {
            this.productImages = ["http://localhost:3000/" + this.product.image.replace(/\\/g, "/")];
          }
        } else {
          this.productImages = ["/product/default.jpg"];
        }
        this.currentMainImage = this.productImages[0];
        this.product.image = this.currentMainImage;

        // Set category name
        if (this.product.category && this.product.category.name) {
          this.categoryName = this.product.category.name;
        }

        // Set default values
        this.product.rating = this.product.rating || 4.0;
        this.product.promotionAsPercentage = this.product.promotionAsPercentage || 0;

      } catch (error) {
        console.error("Error fetching product details:", error);
        this.error = "Failed to load product details. Please try again.";
      } finally {
        this.loading = false;
      }
    },

    setMainImage(image) {
      this.currentMainImage = image;
      this.product.image = image;
    },

    increaseQuantity() {
      if (this.quantity < 99) {
        this.quantity++;
      }
    },

    decreaseQuantity() {
      if (this.quantity > 1) {
        this.quantity--;
      }
    },

    addToCart() {
      // TODO: Implement cart functionality
      alert(`Added ${this.quantity} x ${this.product.name} to cart!`);
    },
  },
  watch: {
    '$route.params.productId': {
      immediate: true,
      handler() {
        this.fetchProductDetails();
      }
    }
  },
  mounted() {
    this.fetchProductDetails();
  },
};
</script>

<style scoped>
.product-view {
  width: 100%;
  padding: 0 20px;
}

.page-header {
  margin: 20px 0 30px 0;
}

.breadcrumb {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  font-size: 14px;
}

.breadcrumb-link {
  color: #666;
  text-decoration: none;
  transition: color 0.3s ease;
}

.breadcrumb-link:hover {
  color: #29a754;
}

.breadcrumb-separator {
  margin: 0 8px;
  color: #999;
}

.breadcrumb-current {
  color: #333;
  font-weight: 500;
}

.product-detail {
  margin: 40px 0;
}

.product-container {
  display: flex;
  gap: 40px;
  max-width: 1200px;
  margin: 0 auto;
}

.product-images {
  flex: 1;
  max-width: 500px;
}

.main-image {
  width: 100%;
  height: 400px;
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 20px;
  border: 1px solid #e0e0e0;
}

.main-image img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.thumbnail-images {
  display: flex;
  gap: 10px;
  overflow-x: auto;
}

.thumbnail-images img {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 4px;
  cursor: pointer;
  border: 2px solid transparent;
  transition: border-color 0.3s ease;
}

.thumbnail-images img:hover,
.thumbnail-images img.active {
  border-color: #29a754;
}

.product-info {
  flex: 1;
  max-width: 600px;
}

.product-name {
  font-size: 28px;
  font-weight: bold;
  color: #333;
  margin: 0 0 15px 0;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.stars {
  color: #ffc107;
  font-size: 16px;
}

.rating-value {
  color: #666;
  font-size: 14px;
}

.product-price {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 25px;
}

.current-price {
  font-size: 24px;
  font-weight: bold;
  color: #29a754;
}

.old-price {
  font-size: 18px;
  color: #999;
  text-decoration: line-through;
}

.discount {
  background: #ff4444;
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
  font-weight: 600;
}

.product-meta {
  margin-bottom: 30px;
}

.meta-item {
  display: flex;
  margin-bottom: 10px;
}

.meta-label {
  font-weight: 600;
  color: #333;
  min-width: 80px;
}

.meta-value {
  color: #666;
}

.product-actions {
  display: flex;
  gap: 20px;
  align-items: center;
  margin-bottom: 30px;
}

.quantity-selector {
  display: flex;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.quantity-selector button {
  background: #f5f5f5;
  border: none;
  width: 40px;
  height: 40px;
  cursor: pointer;
  font-size: 16px;
  transition: background 0.3s ease;
}

.quantity-selector button:hover:not(:disabled) {
  background: #e0e0e0;
}

.quantity-selector button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.quantity-selector input {
  width: 60px;
  height: 40px;
  text-align: center;
  border: none;
  border-left: 1px solid #ddd;
  border-right: 1px solid #ddd;
  font-size: 16px;
}

.add-to-cart-btn {
  background: #29a754;
  color: white;
  border: none;
  padding: 12px 30px;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease;
}

.add-to-cart-btn:hover {
  background: #1e7a3a;
}

.product-description {
  margin-top: 30px;
}

.product-description h3 {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-bottom: 10px;
}

.product-description p {
  color: #666;
  line-height: 1.6;
}

.loading {
  text-align: center;
  padding: 40px;
  font-size: 16px;
  color: #666;
}

.error {
  text-align: center;
  padding: 40px;
  font-size: 16px;
  color: #d32f2f;
  background-color: #ffebee;
  border-radius: 8px;
  margin: 20px 0;
}

@media (max-width: 768px) {
  .product-container {
    flex-direction: column;
    gap: 30px;
  }

  .product-images,
  .product-info {
    max-width: 100%;
  }

  .main-image {
    height: 300px;
  }

  .product-actions {
    flex-direction: column;
    align-items: stretch;
  }

  .quantity-selector {
    justify-content: center;
  }
}
</style>
