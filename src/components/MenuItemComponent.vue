<template>
  <nav class="menu-container">
    <div class="menu-content">
      <!-- Left side - Browse Categories -->
      <div class="menu-left">
        <div class="browse-categories">
          <span class="browse-icon">📋</span>
          <span class="browse-text">Browse All Categories</span>
          <span class="browse-arrow">▼</span>
        </div>
      </div>

      <!-- Center - Main Navigation -->
      <div class="menu-center">
        <ul class="menu-list">
          <li v-for="item in menuItems" :key="item.label" class="menu-item">
            {{ item.label }}
          </li>
        </ul>
      </div>

      <!-- Right side - Hot Deals and Phone -->
      <div class="menu-right">
        <div class="hot-deals">
          <span class="hot-icon">🔥</span>
          <span class="hot-text">Hot Deals</span>
        </div>
        <div class="phone-support">
          <span class="phone-icon">📞</span>
          <span class="phone-number">+880 1234 5678</span>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "MenuItemComponent",
  data() {
    return {
      menuItems: [
        { label: "Home" },
        { label: "Food" },
        { label: "Vegetables" },
        { label: "Drink" },
        { label: "Cookies" },
        { label: "Meat & Seafood" },
        { label: "Bakery" },
      ],
    };
  },
};
</script>

<style scoped>
.menu-container {
  background: #29a754;
  padding: 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.menu-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0 20px;
  height: 60px;
}

.menu-left {
  display: flex;
  align-items: center;
}

.browse-categories {
  display: flex;
  align-items: center;
  gap: 8px;
  background: rgba(255, 255, 255, 0.15);
  padding: 10px 16px;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
  color: white;
}

.browse-categories:hover {
  background: rgba(255, 255, 255, 0.25);
}

.browse-icon {
  font-size: 16px;
}

.browse-text {
  font-size: 14px;
  font-weight: 600;
}

.browse-arrow {
  font-size: 12px;
}

.menu-center {
  flex: 1;
  display: flex;
  justify-content: center;
}

.menu-list {
  display: flex;
  gap: 35px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu-item {
  color: white;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  padding: 5px 0;
}

.menu-item:hover {
  opacity: 0.8;
}

.menu-item::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background: white;
  transition: width 0.3s ease;
}

.menu-item:hover::after {
  width: 100%;
}

.menu-right {
  display: flex;
  align-items: center;
  gap: 30px;
}

.hot-deals {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #ffcc00;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.hot-deals:hover {
  color: #ffd700;
}

.hot-icon {
  font-size: 18px;
}

.hot-text {
  font-size: 14px;
}

.phone-support {
  display: flex;
  align-items: center;
  gap: 8px;
  color: white;
  font-weight: 500;
}

.phone-icon {
  font-size: 16px;
}

.phone-number {
  font-size: 14px;
}

@media (max-width: 768px) {
  .menu-content {
    flex-wrap: wrap;
    height: auto;
    padding: 10px 20px;
  }

  .menu-center {
    order: 3;
    width: 100%;
    margin-top: 10px;
  }

  .menu-list {
    gap: 20px;
    flex-wrap: wrap;
    justify-content: center;
  }

  .menu-item {
    font-size: 14px;
  }

  .phone-support {
    display: none;
  }
}
</style>
