<template>
  <div id="app">
    <the-header
      :cart="cart"
      @deleteAll="deleteAll"
      @decrement="decrement"
      @increment="incerement"
    />
    <product-card :cart="cart" @addToCart="addToCart" :products="products" />
  </div>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import ProductCard from "./components/ProductCard.vue";
import data from "../src/static/data.json";
export default {
  name: "App",
  components: {
    TheHeader,
    ProductCard,
  },
  data() {
    return {
      cart: data.cart,
      products: data.products,
    };
  },
  methods: {
    findProduct(productId) {
      return this.products.find((product) => product.id == productId);
    },
    addToCart(product) {
      let selectedProduct = this.findProduct(product.id);
      let selectedPrice = selectedProduct.sizeOfPrice.find(
        (price) => price.id == product.selectedPriceId
      );
      let findItem = this.cart.find(
        (x) =>
          x.id == product.id && x.selectedPriceId == product.selectedPriceId
      );
      if (findItem) {
        findItem.piece = findItem.piece + product.piece;
      } else {
        let cartItem = { ...selectedProduct, selectedPrice };
        this.cart = [...this.cart, cartItem];
      }
    },
    deleteAll() {
      this.cart = [];
    },
    decrement(item) {
      let piece = item.piece;
      if (piece == 1) {
        this.cart = this.cart.filter((el) => el !== item);
      } else {
        item.piece = piece - 1;
      }
    },
    incerement(item) {
      let piece = item.piece;
      item.piece = piece + 1;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
