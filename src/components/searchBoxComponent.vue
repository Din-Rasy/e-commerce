<template>
  <div class="searchbox-wrapper">

    <!-- Logo Section -->
    <div class="logo-box">
      <img src="/Logo.png" alt="Logo" class="logo-image" />
    </div>

    <!-- Search Container -->
    <div class="searchbox-container">

      <div class="category-box">
        <span class="category-text">All Categories</span>
        <span class="arrow">▼</span>
      </div>

      <div class="divider"></div>

      <input
        type="text"
        class="search-input"
        placeholder="Search for items"
      />

      <button class="search-btn">
        🔍
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchBoxComponent",
  props: {
    logoUrl: {
      type: String,
      default: "/logo.png", // replace with your actual logo path
    }
  }
};
</script>

<style scoped>
/* Whole Area: Logo + SearchBar */
.searchbox-wrapper {
  display: flex;
  align-items: center;
  gap: 20px;
  width: 100%;
}

/* Logo Size */
.logo-box {
  display: flex;
  align-items: center;
}
.logo-image {
  height: 50px;
  width: auto;
  cursor: pointer;
}

/* Search Container */
.searchbox-container {
  display: flex;
  align-items: center;
  width: 600px;
  padding: 10px 15px;
  background: white;
  border-radius: 8px;
  border: 1px solid #b7e4c7;
}

/* Category dropdown */
.category-box {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.category-text {
  font-size: 14px;
  font-weight: 600;
  margin-right: 6px;
}

.arrow {
  font-size: 12px;
}

/* Divider */
.divider {
  width: 1px;
  height: 20px;
  background: #ddd;
  margin: 0 12px;
}

/* Input */
.search-input {
  flex: 1;
  border: none;
  outline: none;
  font-size: 14px;
}

/* Search Button */
.search-btn {
  background: transparent;
  border: none;
  cursor: pointer;
  font-size: 18px;
}
.search-btn:hover {
  opacity: 0.7;
}
</style>
