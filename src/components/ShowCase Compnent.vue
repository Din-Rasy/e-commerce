<template>
  <div class="showcase-banner">
    <div class="showcase-content">
      <h1>Don’t miss amazing grocery deals</h1>
      <p>Sign up for the daily newsletter</p>

      <div class="input-box">
        <input type="email" placeholder="Your email address" />
        <button>Subscribe</button>
      </div>
    </div>

    <div class="showcase-image-container">
      <img src="/fresh-apples-shopping-mesh-bag-with-branch-apples-removebg 1.png" alt="Promo" class="showcase-image" />
    </div>
  </div>
</template>

<script>
export default {
  name: "ShowCaseComponent",
  props: {
    image: {
      type: String,
      default: "/assets/promo-image.png",
    },
  },
};
</script>

<style scoped>
.showcase-banner {
  display: flex;
  justify-content: space-between;
  padding: 40px;
  background: #fff4dd;
  border-radius: 16px;
}
.showcase-content h1 {
  width: 340px;
  font-size: 50px;
  font-weight: bold;
}
.input-box {
  display: flex;
  margin-top: 20px;
}
.input-box input {
  width: 220px;
  padding: 10px;
  border-radius: 6px 0 0 6px;
  border: none;
}
.input-box button {
  background: #29a754;
  color: white;
  padding: 10px 18px;
  border-radius: 0 6px 6px 0;
  border: none;
}
.showcase-image {
  width: 420px;
  object-fit: contain;
}
</style>
