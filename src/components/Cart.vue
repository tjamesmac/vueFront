<template>
  <div class="d-flex flex-column">
    <p class="cart-info cart-prod" v-if="cartProductsPrice.length">
      {{ cartProductsPrice.length }}
      <span v-if="cartProductsPrice.length > 1">products</span>
      <span v-else>product</span>
      : £{{ cartProdTotal.toFixed(2) }}
    </p>
    <p class="cart-info cart-sub" v-if="cartSubscriptionsPrice.length">
      {{ cartSubscriptionsPrice.length }}
      <span v-if="cartSubscriptionsPrice.length > 1">subscriptions</span>
      <span v-else>subscription</span>
      : £{{ cartSubTotal }} p/m
    </p>
  </div>
</template>

<script>
export default {
  name: "Cart",
  props: ["cartProductsPrice", "cartProdTotal", "cartSubscriptionsPrice", "cartSubTotal"]
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
