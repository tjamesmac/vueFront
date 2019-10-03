<template>
  <div v-if="productInfo !== null">
    <div class="modal" tabindex="-1">
      <div class="modal-dialog">
        <div class="modal-header">
          <h2>{{ productInfo.name }}</h2>
          <button
            class="close font-weight-bold"
            v-on:click="this.handleClose"
            aria-label="close"
          >
            <span>X</span>
          </button>
        </div>
        <p v-if="productInfo.detail" v-html="productInfo.detail"></p>
        <p v-else>{{ productInfo.description }}</p>
        <p class="text-danger font-weight-bold" v-if="productInfo.dealText">
          ***{{ productInfo.dealText }}***
        </p>
        <ul v-if="productInfo.variants">
          <li v-for="item in productInfo.variants" :key="item.id">
            <input
              type="radio"
              v-bind:id="item.name"
              :name="'group' + productInfo.name"
              v-bind:value="item.price / 100"
            />
            <label v-bind:for="'group' + productInfo.name" class="pl-2">
              <span class="font-weight-bold">{{ item.name }}</span> :
              <span
                class="font-weight-bold"
                style="text-decoration: line-through;"
              >
                £{{ item.price / 100 }}
              </span>
              <span class="text-danger font-weight-bold">
                £{{ (item.price / 2 / 100).toFixed(2) }}
              </span>
            </label>
          </li>
        </ul>
        <p class="font-weight-bold" v-if="productInfo.price">
          Price: £{{ productInfo.price / 100 }}
        </p>
        <p class="font-weight-bold" v-if="productInfo.subscription">
          {{ productInfo.subscription.name }}
          £{{ productInfo.subscription.price / 100 }} per
          {{ productInfo.subscription.label }}
        </p>
        <button
          class="btn btn-primary btn-orange"
          aria-label="add product to cart"
          v-on:click="this.addToCart"
        >
          Add to cart
        </button>
      </div>
    </div>
    <div class="modal-backdrop"></div>
  </div>
</template>

<script>
export default {
  name: "DealModal",
  props: {
    productInfo: Object || null
  },
  mounted() {
    console.log(this.productInfo);
  },
  methods: {
    handleClose: function() {
      this.$emit("closeModal");
    },
    addToCart: function() {
      // this.$emit("addToCart");
      if (this.productInfo.variants) {
        console.log("I am here");
        const variantName = "group" + this.productInfo.name;
        const radio = document.querySelector(
          `input[name="${variantName}"]:checked`
        );
        if (radio) {
          const radioValue = (radio.value / 2).toFixed(2);
          const productPrice = { product: radioValue };
          this.$emit("addToCart", productPrice);
        } else {
          alert("Please select an option");
        }
      } else if (this.productInfo.subscription) {
        const subPrice = this.productInfo.subscription.price / 100;
        const productPrice = this.productInfo.price / 100;
        if (subPrice &&  productPrice) {
          const priceObject = {
            subscription: {
              sub: subPrice,
              price: productPrice
            }
          };
          console.log(priceObject);
          return this.$emit("addToCart", priceObject);
        } else {
          alert("Please select an option");
        }
      } else {
        console.log(this.productInfo.price / 100);
        const value = this.productInfo.price / 100;
        if (value) {
          const productPrice = { product: value };
          return this.$emit("addToCart", productPrice);
        } else {
          alert("Please select an option");
        }
      }
    },
    getPrice: function() {
      console.log(this.productInfo.price);
    }
  },
  computed: {
    propCheck() {
      console.log(this.productInfo);
      return this.productInfo;
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
