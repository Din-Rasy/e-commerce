<template>
  <nav class="menu-container">
    <ul class="menu-list">
      <li v-for="item in menuItems" :key="item.label" class="menu-item">
        {{ item.label }} ▼
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "MenuItemComponent",
  data() {
    return {
      menuItems: [
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
  padding: 10px 0;
  border-bottom: 1px solid #eee;
}
.menu-list {
  display: flex;
  justify-content: center;
  gap: 28px;
  list-style: none;
  padding: 0;
  margin: 0;
}
.menu-item {
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
}
.menu-item:hover {
  color: #29a754;
}
</style>
