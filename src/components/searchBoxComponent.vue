<template>
  <div class="searchbox-wrapper">
    <!-- Logo Section -->
    <div class="logo-box">
      <img src="/Logo.png" alt="Logo" class="logo-image" />
    </div>

    <!-- Search Container -->
    <div class="searchbox-container">
      <div class="category-dropdown">
        <span class="category-text">All Categories</span>
        <span class="dropdown-arrow">▼</span>
      </div>

      <div class="divider"></div>

      <input
        type="text"
        class="search-input"
        placeholder="Search for items"
      />

      <button class="search-button">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <circle cx="11" cy="11" r="8"></circle>
          <path d="m21 21-4.35-4.35"></path>
        </svg>
      </button>
    </div>

    <!-- Account Links -->
    <div class="account-links">
      <div class="link-item">
        <div class="link-icon">👤</div>
        <span class="link-text">Account</span>
      </div>
      <div class="link-item">
        <div class="link-icon">⚖️</div>
        <span class="link-text">Compare</span>
      </div>
      <div class="link-item">
        <div class="link-icon">❤️</div>
        <span class="link-text">Wishlist</span>
      </div>
      <div class="link-item">
        <div class="link-icon">🛒</div>
        <span class="link-text">Cart</span>
      </div>
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
.searchbox-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 30px;
  padding: 20px;
  width: 100%;
}

.logo-box {
  flex-shrink: 0;
}

.logo-image {
  height: 40px;
  width: auto;
  cursor: pointer;
}

.searchbox-container {
  display: flex;
  align-items: center;
  flex: 1;
  max-width: 600px;
  height: 50px;
  background: #f8f9fa;
  border: 1px solid #e9ecef;
  border-radius: 8px;
  padding: 0 5px;
}

.category-dropdown {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 0 15px;
  cursor: pointer;
  border-right: 1px solid #e9ecef;
  height: 100%;
  min-width: 140px;
}

.category-text {
  font-size: 14px;
  font-weight: 500;
  color: #495057;
}

.dropdown-arrow {
  font-size: 12px;
  color: #6c757d;
}

.divider {
  width: 1px;
  height: 30px;
  background: #e9ecef;
}

.search-input {
  flex: 1;
  border: none;
  outline: none;
  font-size: 14px;
  padding: 0 15px;
  background: transparent;
}

.search-input::placeholder {
  color: #adb5bd;
}

.search-button {
  background: none;
  border: none;
  padding: 10px;
  cursor: pointer;
  color: #6c757d;
  border-radius: 6px;
  transition: all 0.3s ease;
}

.search-button:hover {
  background: #e9ecef;
  color: #495057;
}

.account-links {
  display: flex;
  gap: 25px;
  flex-shrink: 0;
}

.link-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
}

.link-item:hover {
  transform: translateY(-2px);
}

.link-icon {
  font-size: 20px;
  margin-bottom: 4px;
  transition: all 0.3s ease;
}

.link-item:hover .link-icon {
  transform: scale(1.1);
}

.link-text {
  font-size: 12px;
  font-weight: 500;
  color: #495057;
}

.link-item:hover .link-text {
  color: #29a754;
}

@media (max-width: 768px) {
  .searchbox-wrapper {
    flex-wrap: wrap;
    gap: 20px;
  }

  .searchbox-container {
    order: 3;
    max-width: 100%;
  }

  .account-links {
    gap: 20px;
  }

  .link-text {
    display: none;
  }

  .link-icon {
    margin-bottom: 0;
  }
}
</style>
