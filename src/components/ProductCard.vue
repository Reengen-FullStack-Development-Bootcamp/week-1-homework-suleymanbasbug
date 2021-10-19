<template>
  <div class="mt-3 ml-3">
    <b-container>
      <b-row class="d-flex justify-content-around">
        <b-card
          v-for="(product, i) in products"
          :key="i"
          class="overflow-hidden mt-3"
          :class="product.color === 'pink' ? 'pink-border' : 'blue-border'"
          style=" width:560px"
        >
          <b-row no-gutters>
            <b-col md="6">
              <b-card-img
                :src="product.imageUrl"
                alt="Image"
                class="rounded-3 ml-2"
              ></b-card-img>
              <b-row class="mt-3 ml-2">
                <button
                  class="btn ml-2 mt-1"
                  :class="product.color == 'pink' ? 'pink-button' : 'blue-button' "
                  v-for="(number, i) in product.sizeOfPrice"
                  :key="i"
                  @click="selectNumber(product.id, number.id)"
                >
                  {{ number.size }}
                </button>
              </b-row>
            </b-col>
            <b-col md="6">
              <b-card-body>
                <b-card-text :class="product.color === 'pink' ? 'pink-category' : 'blue-category'">
                  {{ product.category }}
                </b-card-text>
                <b-card-text class="pink-title">
                  {{ product.title }}
                </b-card-text>
                <b-card-text :class="product.color === 'pink' ? 'pink-price' : 'blue-price'">
                  ${{
                    product.sizeOfPrice.find(
                      (x) => x.id == product.selectedPriceId
                    ).price
                  }}
                </b-card-text>
                <b-card-text class="pink-description">
                  {{ product.description }}
                </b-card-text>
                
                <b-form-select
                  v-model="product.piece"
                  :options="options"
                ></b-form-select>
                <b-form-rating
                  v-model="product.star"
                  variant="warning"
                  class="mt-2"
                  readonly
                ></b-form-rating>
                <button
                  @click="addToCart(product)"
                  class="btn btn-md mt-2"
                  :class="product.color === 'pink' ? 'pink-button' : 'blue-button'"
                >
                  ADD TO CART
                </button>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import data from "../static/data.json";
export default {
  name: "ProductCard",
  props: {
    cart: Array,
    products: Array,
  },
  data() {
    return {
      options: data.selectOptions,
      starValue: 3,
    };
  },
  computed: {},
  methods: {
    findProduct(productId) {
      return this.products.find((product) => product.id == productId);
    },
    selectNumber(productId, numberId) {
      let selectedProduct = this.findProduct(productId);
      selectedProduct.selectedPriceId = numberId;
    },
    addToCart(product) {
      this.$emit("addToCart", product);
      this.$bvToast.toast(`Ürün Sepete Eklendi`, {
          title: 'Ürün Eklendi!',
          autoHideDelay: 2000,
          appendToast: true,
          toaster: 'b-toaster-bottom-left'
        })
    },
  },
};
</script>

<style>
.pink-button{
  color: #f6f4f5 !important;
  background-color: #be837f !important;
}
.pink-button:hover{
  color: #be837f !important;
  background-color: #f6f4f5 !important;
}
.pink-price{
  font-size:30px;
  color: #d3adac;
  font-weight: 900;
  text-align: left;
}
.pink-category{
  font-size:15px;
  text-align: left;
  color: #d3adac;
  font-weight: 700
}
.pink-title{
  font-size: 25px;
  text-align: left;
}
.pink-description{
  font-size:13px;
  text-align:left;
}
.blue-button{
  color: #D5F3FE !important;
  background-color: #0F5298 !important;
}
.blue-button:hover{
  color: #0F5298 !important;
  background-color:  #D5F3FE !important;
}
.blue-price{
  font-size:30px;
  font-weight: 900;
  color: #0F5298;
  text-align: left;
}
.blue-category{
  font-size:15px;
  text-align: left;
  color: #0F5298;
  font-weight: 700
}
.pink-border{
  box-shadow: 2px 2px #d3adac;
}
.blue-border{
  box-shadow: 2px 2px #2565AE;
}
</style>
