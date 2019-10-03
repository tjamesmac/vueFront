<template>
  <div v-if="cartToggle">
    <div class="modal" tabindex="-1">
      <div class="modal-dialog">
        <div class="modal-header">
          <h2>Shopping Cart</h2>
          <button
            class="close font-weight-bold"
            v-on:click="this.handleClose"
            aria-label="close"
          >
            <span>X</span>
          </button>
        </div>
        <div v-if="cartProducts.length">
          <div v-for="(item, index) in cartProducts" :key="index">
            <div class="d-flex flex-row align-items-center" v-if="item.type">
              {{ item.productName }} - {{ item.type }} - £{{ item.product }}
              <button
                class="btn btn-primary text-danger ml-4"
                v-on:click="removeItemProd(index)"
              >
                X
              </button>
            </div>
          </div>
        </div>
        <div v-if="cartSubscriptions.length">
          <div v-for="(item, index) in cartSubscriptions" :key="item + index">
            <div
              class="d-flex flex-row align-items-center"
              v-if="item.subscription"
            >
              {{ item.subscription.productName }} - £{{ item.subscription.product }}
                - £{{ item.subscription.sub }}p/m
              <button
                class="btn btn-primary text-danger ml-4"
                v-on:click="removeItemSub(index)"
              >
                X
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="modal-backdrop"></div>
  </div>
</template>

<script>
export default {
  name: "CartModal",
  data: function() {
    return {
      cartProductsItems: [],
      cartSubscriptionsItems: []
    };
  },
  props: ["cartToggle", "cartProducts", "cartSubscriptions"],
  methods: {
    handleClose: function() {
      this.$emit("closeCartModal");
    },
    removeItemProd: function(index) {
      const cartProd = this.cartProducts;
      cartProd.splice(index, 1);
      this.cartProducts = cartProd;
      this.$emit("removeCartItemProd", this.cartProducts);
    },
    removeItemSub: function(index) {
      const subProd = this.cartSubscriptions;
      const cartProd = this.cartProducts;
      subProd.splice(index, 1);
      cartProd.splice(index, 1);
      this.cartSubscriptions = subProd;
      this.cartProducts = cartProd;
      this.$emit("removeCartItemSub", { subs:this.cartSubscriptions, prods: this.cartProducts } );
    },
    getKeys: function() {
      const cartProductKeys = Object.keys(this.cartProducts);
      return cartProductKeys;
    }
  },
  watch: {
    cartProducts: function() {
      this.cartProductsItems = [];
      this.cartSubscriptionsItems = [];
      for (const item of this.cartProducts) {
        const keys = Object.keys(item);
        if (keys.includes("subscription")) {
          this.cartSubscriptionsItems.push(item.subscription.sub);
          this.cartProductsItems.push(item.subscription.product);
        } else {
          this.cartProductsItems.push(item.product);
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.modal {
  position: fixed;
  z-index: 1050;
  display: block;
  width: 100%;
  outline: 0;
}
.modal-dialog {
  position: relative;
  flex: 0 0 auto;
  width: auto;
  height: auto;
  margin: 0.5 auto;
  padding: 2.5rem 1.5rem;
  background-color: white;
  // z-index: 1051;
  // overflow-y: auto;
  pointer-events: auto;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #22211f;
  opacity: 0.8;
}
.modal-header {
  border-bottom: none;
  padding: 0;
}
.close {
  padding: 0rem 1rem;
  pointer-events: auto;
}

body {
  overflow: hidden;
}
</style>
