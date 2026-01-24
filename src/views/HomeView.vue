<template>
  <div class="home">

    <!-- Search Box with Logo and Account Links -->
    <SearchBoxComponent />

    <!-- Main Navigation Menu -->
    <MenuItemComponent />

    <!-- ShowCase Banner -->
    <ShowCaseComponent />

    <!-- Featured Categories -->
    <div class="section">
      <h2 class="section-title">Featured Categories</h2>
      <div class="categories-section">
        <CategoryComponent
          v-for="category in categories"
          :key="category._id || category.name"
          :name="category.name"
          :product-count="category.productCount"
          :color="category.color"
          :image="category.image"
        />
      </div>
    </div>

    <!-- Promotional Banners -->
    <div class="section">
      <div class="promotions-section">
        <PromotionComponent
          v-for="promotion in promotions"
          :key="promotion._id || promotion.url"
          :title="promotion.title"
          :color="promotion.color"
          :image="promotion.image"
          :button-color="promotion.buttonColor"
          :url="promotion.url"
          :image-container-width="promotion.imageContainerWidth"
          :image-container-height="promotion.imageContainerHeight"
          :image-width="promotion.imageWidth"
          :image-height="promotion.imageHeight"
          :image-max-height="promotion.imageMaxHeight"
          :image-object-fit="promotion.imageObjectFit"
        />
      </div>
    </div>

    <!-- Popular Products -->
    <div class="section">
      <h2 class="section-title">Popular Products</h2>
      <div class="products-section">
        <ProductComponent
          v-for="product in products"
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

  </div>
</template>

<script>
import axios from "axios";

import CategoryComponent from "../components/CategoryComponent.vue";
import PromotionComponent from "../components/PromotionComponent.vue";
import SearchBoxComponent from "../components/searchBoxComponent.vue";
import MenuItemComponent from "../components/MenuItemComponent.vue";
import ShowCaseComponent from "../components/ShowCase Compnent.vue";
import ProductComponent from "../components/ProductComponent.vue";

export default {
  name: "HomeView",
  components: {
    SearchBoxComponent,
    MenuItemComponent,
    ShowCaseComponent,
    CategoryComponent,
    PromotionComponent,
    ProductComponent,
  },
  data() {
    return {
      categories: [],
      promotions: [],
      products: [],
    };
  },

  methods: {
    async fetchCategories() {
      try {
        const res = await axios.get("http://localhost:3000/api/categories");
        this.categories = res.data.map((item) => ({
          ...item,
          image: "http://localhost:3000/" + item.image.replace(/\\/g, "/"),
        }));
      } catch (error) {
        console.error(error);
      }
    },

    async fetchPromotions() {
      try {
        const res = await axios.get("http://localhost:3000/api/promotions");
        this.promotions = res.data.map((item) => ({
          ...item,
          image: "http://localhost:3000/" + item.image.replace(/\\/g, "/"),
        }));
      } catch (error) {
        console.error(error);
      }
    },

    async fetchProducts() {
      try {
        const res = await axios.get("http://localhost:3000/api/products");
        this.products = res.data.map((item) => {
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
        console.error(error);
      }
    },

  },

  mounted() {
    this.fetchCategories();
    this.fetchPromotions();
    this.fetchProducts();
  },
};
</script>

<style scoped>
.home {
  width: 100%;
  padding: 0 20px;
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

/* Category Cards */
.categories-section {
  display: flex;
  gap: 12px;
  margin-bottom: 40px;
  justify-content: center;
  overflow-x: auto;
  padding: 10px 0;
}

/* Promotions Cards */
.promotions-section {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
}

/* Product Cards Section */
.products-section {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  margin-top: 30px;
}
</style>
