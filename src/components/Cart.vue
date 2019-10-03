<template>
  <div class="d-flex flex-column">
    <p class="cart-info cart-prod" v-if="cartProductsPrice.length">
      {{ cartProductsPrice.length }}
      <span v-if="cartProductsPrice.length > 1">products</span>
      <span v-else>product</span>
      : £{{ cartProductsTotal.toFixed(2) }}
    </p>
    <p class="cart-info cart-sub" v-if="cartSubscriptionsPrice.length">
      {{ cartSubscriptionsPrice.length }}
      <span v-if="cartSubscriptionsPrice.length > 1">subscriptions</span>
      <span v-else>subscription</span>
      : £{{ cartSubscriptionsTotal }} p/m
    </p>
  </div>
</template>

<script>
export default {
  name: "Cart",
  data: function() {
    return {
      cartProductsPrice: [],
      cartProductsTotal: 0,
      cartSubscriptionsPrice: [],
      cartSubscriptionsTotal: 0
    };
  },
  updated() {
    console.log("i am updating");
  },
  props: ["cartProducts", "cartSubscriptions"],
  watch: {
    cartProducts: function() {
      console.log(this.cartProducts, "inside the cart");
      this.cartProductsPrice = [];
      this.cartSubscriptionsPrice = [];
      for (const item of this.cartProducts) {
        console.log(item.product);
        const keys = Object.keys(item);
        if (keys.includes("subscription")) {
          this.cartSubscriptionsPrice.push(item.subscription.sub);
          this.cartProductsPrice.push(item.subscription.product);
        } else {
          console.log(item.product);
          this.cartProductsPrice.push(item.product);
          console.log(this.cartProductsPrice);
        }
      }
    },
    cartProductsPrice: function() {
      let total = 0;
      for (const item of this.cartProductsPrice) {
        const float = parseFloat(item);
        total += float;
      }
      this.cartProductsTotal = total;
    },
    cartSubscriptionsPrice: function() {
      let total = 0;
      for (const item of this.cartSubscriptionsPrice) {
        const float = parseFloat(item);
        total += float;
      }
      this.cartSubscriptionsTotal = total;
    }
  }
};
</script>

<style lang="scss">
.cart-info {
  display: inline;
  padding: 5px;
}
.cart-prod {
  background-color: rgb(218, 216, 216);
}
.cart-sub {
  background-color: darkgray;
}
@media (min-width: 768px) {
  .card-info {
    align-self: flex-end;
  }
}
</style>
