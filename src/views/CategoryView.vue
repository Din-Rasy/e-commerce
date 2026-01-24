<template>
  <div class="category-view">
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
        <span class="breadcrumb-current">{{ categoryName }}</span>
      </div>
      <h1 class="page-title">{{ categoryName }}</h1>
    </div>

    <!-- Products in this category -->
    <div class="section">
      <h2 class="section-title">Products in {{ categoryName }}</h2>
      <div class="products-section">
        <ProductComponent
          v-for="product in categoryProducts"
          :key="product._id || product.name"
          :image="product.image"
          :category="product.category"
          :name="product.name"
          :weight="product.weight"
          :size="product.size"
          :price="product.price"
          :oldPrice="product.oldPrice"
          :badge="product.badge"
          :rating="product.rating"
          :promotionAsPercentage="product.promotionAsPercentage"
        />
      </div>
    </div>

    <!-- Loading state -->
    <div v-if="loading" class="loading">
      Loading products...
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
import ProductComponent from "../components/ProductComponent.vue";

export default {
  name: "CategoryView",
  components: {
    SearchBoxComponent,
    MenuItemComponent,
    ProductComponent,
  },
  data() {
    return {
      categoryName: "",
      categoryProducts: [],
      loading: false,
      error: null,
    };
  },
  methods: {
    async fetchCategoryProducts() {
      const categoryId = this.$route.params.categoryId;
      this.loading = true;
      this.error = null;

      try {
        // Fetch category details
        const categoryRes = await axios.get(`http://localhost:3000/api/categories/${categoryId}`);
        this.categoryName = categoryRes.data.name;

        // Fetch products for this category
        const productsRes = await axios.get(`http://localhost:3000/api/products?category=${categoryId}`);
        this.categoryProducts = productsRes.data.map((item) => {
          let imagePath = "/product/default.jpg";
          if (item.image) {
            try {
              const images = JSON.parse(item.image);
              if (Array.isArray(images) && images.length > 0) {
                imagePath = "http://localhost:3000/" + images[0].replace(/\\/g, "/");
              } else if (typeof item.image === 'string') {
                imagePath = "http://localhost:3000/" + item.image.replace(/\\/g, "/");
              }
            } catch {
              imagePath = "http://localhost:3000/" + item.image.replace(/\\/g, "/");
            }
          }
          return {
            ...item,
            image: imagePath,
            rating: item.rating || 4.0,
            promotionAsPercentage: item.promotionAsPercentage || 0
          };
        });
      } catch (error) {
        console.error("Error fetching category products:", error);
        this.error = "Failed to load category products. Please try again.";
      } finally {
        this.loading = false;
      }
    },
  },
  watch: {
    '$route.params.categoryId': {
      immediate: true,
      handler() {
        this.fetchCategoryProducts();
      }
    }
  },
  mounted() {
    this.fetchCategoryProducts();
  },
};
</script>

<style scoped>
.category-view {
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

.page-title {
  font-size: 32px;
  font-weight: bold;
  color: #333;
  margin: 0;
}

.section {
  margin: 40px 0;
}

.section-title {
  font-size: 28px;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.products-section {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  margin-top: 30px;
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
</style>
