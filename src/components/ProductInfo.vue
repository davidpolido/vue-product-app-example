<template>
  <div class="product-info">
    <h1>{{ title }}</h1>
    <div class="info-pills-container">
      <p class="info-pills" v-if="inStock">In stock</p>
      <p
        class="info-pills"
        v-else
        v-bind:style="{ backgroundColor: '#7c1e1e' }"
      >
        Out of stock
      </p>
      <div class="info-pills" v-if="onSale">{{ sale }}</div>
    </div>

    <div class="shipping-details-container">
      <h3>Details</h3>
      <ul>
        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
      </ul>
      <h3>Shipping</h3>
      <p>{{ shipping }}</p>
    </div>

    <h3>Colors</h3>
    <div class="colors-container">
      <div
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{ backgroundColor: variant.color }"
        v-on:mouseover="updateProduct(index)"
      ></div>
    </div>

    <h3>Sizes</h3>
    <div class="sizes-container">
      <ul>
        <li v-for="(size, index) in sizes" :key="index">
          {{ size.toUpperCase() }}
        </li>
      </ul>
    </div>

    <div class="buttons-container">
      <button v-on:click="addToCart" :class="{ disabledButton: !inStock }">
        Add to Cart
      </button>
      <button v-on:click="removeFromCart">
        Remove from Cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      product: "Socks",
      brand: "Vue Mastery",
      selectedVariant: 0,
      details: ["80% Cotton", "20% Unicorn Hair", "Fully smelly"],
      variants: [
        {
          variantId: 1234,
          color: "green",
          variantImage: "vmSocks-green.jpg",
          variantQuantity: 10
        },
        {
          variantId: 4321,
          color: "blue",
          variantImage: "vmSocks-blue.jpg",
          variantQuantity: 0
        }
      ],
      sizes: ["xs", "s", "m", "l", "xl", "wow"],
      onSale: true,
      sale: "On Sale",
      reviews: []
    };
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    shipping() {
      if (this.premium) {
        return "Free";
      } else {
        return "2.99";
      }
    }
  },
  methods: {
    addToCart() {
      this.$emit("addToCart", this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
      this.$emit(
        "changeImage",
        this.variants[this.selectedVariant].variantImage
      );
    },
    removeFromCart() {
      this.$emit(
        "removeFromCart",
        this.variants[this.selectedVariant].variantId
      );
    }
  }
};
</script>

<style scoped>
.product-info {
  flex-grow: 1;
  padding-left: 20px;
}

h1 {
  margin-top: 25px;
  margin-bottom: 5px;
}

.info-pills-container {
  display: flex;
  /* justify-content: flex-start; */
  margin-top: 5px;
  align-items: center;
  /* justify-content: center; */
}
.info-pills {
  width: 80px;
  margin: 0px;
  height: 16px;
  background-color: #83cf6a;
  color: white;
  border-radius: 1em;
  text-align: center;
  font-size: 12px;
}

.colors-container {
  display: flex;
  margin-left: 5px;
}

.color-box {
  width: 30px;
  height: 30px;
  padding: 5px;
  margin: 5px;
  margin-top: 0px;
  border-radius: 1em;
}

.sizes-container {
  margin-left: 5px;
}

.sizes-container ul {
  padding: 0;
  display: flex;
  list-style: none;
  justify-content: flex-start;
}

.sizes-container li {
  width: 55px;
  text-align: center;
  margin: 0 5px;
  padding: 5px 0;
  border: 2px rgb(236, 236, 236) solid;
  border-radius: 1em;
  font-size: 12px;
}

.buttons-container {
  margin-top: 40px;
  display: flex;
  justify-content: flex-end;
  height: 60px;
}

button {
  border: none;
  background-color: #1e95ea;
  padding: 5px;
  color: white;
  height: 50px;
  width: 90px;
  font-size: 14px;
  margin: 0px 10px;
  border-radius: 1em;
}

.disabledButton {
  background-color: #d8d8d8;
}
</style>
