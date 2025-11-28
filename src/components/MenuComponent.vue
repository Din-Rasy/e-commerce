<template>
  <div class="menu-header">
    <h2 class="section-title">{{ title }}</h2>
    <ul class="menu-list">
      <li
        v-for="(item, index) in menus"
        :key="index"
        @click="$emit('change', item)"
        :class="{ active: item === activeMenu }"
      >
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MenuComponent",
  props: {
    title: {
      type: String,
      required: true,
    },
    menus: {
      type: Array,
      required: true,
    },
    activeMenu: {
      type: String,
      default: "All",
    },
  },
};
</script>

<style scoped>
.menu-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 8px;
  border-bottom: 1px solid #e6e6e6;
  margin-bottom: 20px;
}

.section-title {
  font-size: 22px;
  font-weight: 600;
  color: #222;
}

.menu-list {
  display: flex;
  gap: 28px;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu-list li {
  font-size: 15px;
  color: #777;
  cursor: pointer;
  transition: 0.25s;
  padding-bottom: 5px;
}

.menu-list li:hover {
  color: #3bb77e;
}

.menu-list li.active {
  color: #3bb77e;
  border-bottom: 2px solid #3bb77e;
  font-weight: 600;
}
</style>
