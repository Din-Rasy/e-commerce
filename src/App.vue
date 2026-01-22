<template>
  <div class="app">

    <!-- Top: Featured Categories -->
    <MenuComponent
      :title="featuredTitle"
      :menus="menuItems"
      :activeMenu="selectedMenu"
      @change="selectedMenu = $event"
    />

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

    <!-- Bottom: Popular Products -->
    <MenuComponent
      :title="popularTitle"
      :menus="menuItems"
      :activeMenu="selectedMenu"
      @change="selectedMenu = $event"
    />

    <div class="products-section">
      <ProductComponent
        v-for="product in products"
        :key="product._id || product.name"
        :image="product.image"
        :category="product.category"
        :name="product.name"
        :weight="product.weight"
        :price="product.price"
        :oldPrice="product.oldPrice"
        :badge="product.badge"
      />
    </div>

  </div>
</template>

<script>
import axios from "axios";

import CategoryComponent from "./components/CategoryComponent.vue";
import PromotionComponent from "./components/PromotionComponent.vue";
import MenuComponent from "./components/MenuComponent.vue";
import ProductComponent from "./components/ProductComponent.vue";

export default {
  name: "App",
  components: {
    MenuComponent,
    CategoryComponent,
    PromotionComponent,
    ProductComponent,
  },
  data() {
    return {
      selectedMenu: "All",

      featuredTitle: "Featured Categories",
      popularTitle: "Popular Products",

      menuItems: [
        "All",
        "Milks & Dairies",
        "Coffes & Teas",
        "Pet Foods",
        "Meats",
        "Vegetables",
        "Fruits",
      ],

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
        this.products = res.data.map((item) => ({
          ...item,
          image: item.image ? "http://localhost:3000/" + item.image.replace(/\\/g, "/") : "/product/default.jpg",
        }));
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
.app {
  padding: 20px;
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



// categories: [
      //   {
      //     name: 'Cake & Milk',
      //     productCount: 14,
      //     color: '#E8F5E9',
      //     image: '/img/Cake and Milk.png',
      //   },
      //   {
      //     name: 'Peach',
      //     productCount: 17,
      //     color: '#FEFBE8',
      //     image: '/img/Peach.png',
      //   },
      //   {
      //     name: 'Oganic Kiwi',
      //     productCount: 21,
      //     color: '#E8F5E9',
      //     image: '/img/Oganic Kiwi.png',
      //   },
      //   {
      //     name: 'Red Apple',
      //     productCount: 68,
      //     color: '#FFF0E9',
      //     image: '/img/Red Apple.png',
      //   },
      //   {
      //     name: 'Snack',
      //     productCount: 34,
      //     color: '#FEF4EB',
      //     image: '/img/Snack.png',
      //   },
      //   {
      //     name: 'Black plum',
      //     productCount: 25,
      //     color: '#F3E5F5',
      //     image: '/img/Black plum.png',
      //   },
      //   {
      //     name: 'Vegetables',
      //     productCount: 65,
      //     color: '#E8F5E9',
      //     image: '/img/Vegetanles.png',
      //   },
      //   {
      //     name: 'Headphone',
      //     productCount: 33,
      //     color: '#E3F2FD',
      //     image: '/img/Headphone.png',
      //   },
      //   {
      //     name: 'Cake & Milk',
      //     productCount: 54,
      //     color: '#E8F5E9',
      //     image: '/img/Cake and Milk 1.png',
      //   },
      //   {
      //     name: 'Orange',
      //     productCount: 63,
      //     color: '#FEFBE8',
      //     image: '/img/Orange.png',
      //   },
      // ],
      // promotions: [
      //   {
      //     title: 'Everyday Fresh and Clean with Our Products',
      //     color: '#F0E9D7',
      //     image: '/promo/Onion.jpg',
      //     buttonColor: '#42B678',
      //     url: '/promotions/1',
      //     imageContainerWidth: '220px',
      //     imageContainerHeight: '220px',
      //     imageWidth: '220px',
      //     imageHeight: '220px',
      //     imageMaxHeight: '220px',
      //     imageObjectFit: 'contain',
      //   },
      //   {
      //     title: 'Make your Breakfast Healthy and Easy',
      //     color: '#F2E8E9',
      //     image: '/promo/Strawberry.png',
      //     buttonColor: '#42B678',
      //     url: '/promotions/2',
      //     imageContainerWidth: '150px',
      //     imageContainerHeight: '150px',
      //     imageWidth: '150px',
      //     imageHeight: '150px',
      //     imageMaxHeight: '150px',
      //     imageObjectFit: 'contain',
      //   },
      //   {
      //     title: 'The best Organic Products Online',
      //     color: '#E6EAF3',
      //     image: '/promo/Organic Porduct.jpg',
      //     buttonColor: '#FBC040',
      //     url: '/promotions/3',
      //     imageContainerWidth: '140px',
      //     imageContainerHeight: '140px',
      //     imageWidth: '140px',
      //     imageHeight: '140px',
      //     imageMaxHeight: '140px',
      //     imageObjectFit: 'contain',
      //   },
      // ],
