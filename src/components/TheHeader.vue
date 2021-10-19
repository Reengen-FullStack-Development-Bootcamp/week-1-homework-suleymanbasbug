<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">Home</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-dropdown variant="primary" right>
            <template #button-content>
              <b-icon icon="cart" aria-hidden="true"></b-icon> Cart
            </template>
            <div v-if="cart.length==0">Sepetiniz boş. Lütfen ürün ekleyin.</div>
            <div v-for="(item, i) in cart" :key="i">
              <b-dropdown-item-button
                ><button @click="decrement(item)" class="btn btn-danger btn-sm mr-1">-</button>{{ item.title }}
                <button @click="increment(item)" class="btn btn-success btn-sm ml-1">+</button>
                <b-col
                  ><b-badge variant="success">Piece : {{ item.piece }}</b-badge>
                  <b-badge variant="warning"
                    >Number : {{ item.selectedPrice.size }}</b-badge
                  >
                </b-col>
              </b-dropdown-item-button>
              <b-dropdown-divider></b-dropdown-divider>
            </div>
            <b-dropdown-divider></b-dropdown-divider>
            <b-dropdown-item-button  v-if="cart.length>0" variant="danger" @click="deleteAll">
              <b-icon icon="trash-fill" aria-hidden="true"></b-icon>
              Delete All
            </b-dropdown-item-button>
          </b-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "TheHeader",
  props: {
    cart: Array,
  },
  methods: {
    deleteAll() {
      this.$emit("deleteAll");
    },
    decrement(item) {
      this.$emit("decrement", item);
    },
    increment(item) {
      this.$emit("increment", item);
    },
  },
};
</script>

<style></style>
