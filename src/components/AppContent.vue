<template>
  <div class="app-content">
    <div class="product-image">
      <img v-bind:src="image" />
    </div>
    <ProductInfo
      v-on:addToCart="addToCart"
      v-on:removeFromCart="removeFromCart"
      v-on:changeImage="changeImage"
    />
    <div class="cart">
      <p>Cart ({{ cart.length }})</p>
    </div>
    <Reviews />
  </div>
</template>

<script>
import ProductInfo from "./ProductInfo.vue";
import Reviews from "./Reviews.vue";

export default {
  components: {
    ProductInfo,
    Reviews
  },
  data() {
    return {
      cart: [],
      selectedVariant: 0,
      variantImage: "vmSocks-green.jpg"
    };
  },
  computed: {
    image() {
      let selectedImage = this.variantImage;
      return require(`@/assets/${selectedImage}`);
    }
  },
  methods: {
    addToCart(id) {
      this.cart.push(id);
    },
    removeFromCart(id) {
      for (let i = this.cart.length; i >= 0; i--) {
        if (this.cart[i] === id) {
          this.cart.splice(i, 1);
          return {};
        }
      }
    },
    changeImage(variantImage) {
      this.variantImage = variantImage;
    }
  }
};
</script>

<style scoped>
.app-content {
  display: flex;
  flex-grow: 7;
  flex-basis: 90%;
  flex-flow: row wrap;
}

.product-image {
  flex-basis: 40%;
}

img {
  width: 85%;
  margin: 40px;
}

.cart {
  flex-basis: 10%;
  margin: 20px;
  width: 150px;
  height: 50px;
  color: white;
  background-color: black;
  border: lightgray 1px solid;
  text-align: center;
  border-radius: 3em;
  break-after: always;
}
</style>
