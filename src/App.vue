<template>
  <div id="app">
    <main class="container">
      <div class="row">
        <div class="col-12">
          <div class="card d-flex flex-md-row">
            <div class="card-section">
              <h2>Help boost your business</h2>
              <p>
                Some tailored deals to help you achieve your business and
                clinical goals
              </p>
              <p class="font-weight-bold text-danger">
                *** Introductory offer - up to {{ discountPercent }}
                % off ***
              </p>
            </div>
            <div class="card-section text-md-right">
              <p>products go here</p>
              <p>subscription goes here</p>
              <button class="btn btn-primary btn-orange">Checkout</button>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <ul class="card-container">
            <li
              v-for="(product, index) in products"
              :key="index"
              class="card"
              v-on:click="clicker"
              v-bind:data-item="index"
            >
              <ProductItem
                msg="Welcome to Your Vue.js App"
                :info="productData[product]"
              />
            </li>
          </ul>
        </div>
      </div>
    </main>
    <DealModal />
  </div>
</template>

<script>
import ProductItem from "./components/ProductItem.vue";
import DealModal from "./components/DealModal.vue";
import jsonData from "./assets/sample.json";

export default {
  name: "app",
  data: function() {
    return {
      productData: jsonData.products,
      discountPercent: jsonData.discountPercent,
      modalData: null
    };
  },
  computed: {
    products: function() {
      const keys = Object.keys(this.productData);
      return keys;
    }
  },
  methods: {
    clicker: function(event) {
      const target = event.currentTarget.getAttribute("data-item");
      console.log(target);
      this.modalData = target + 1;
    }
  },
  components: {
    ProductItem,
    DealModal
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #fcfcfc;

  ul {
    padding-left: 0px;
    list-style: none;
  }
  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  .card {
    // flex: 0 1 45%;
    width: 100%;
    background-color: #fff;
    border-radius: 0.125rem;
    border-bottom-width: 4px;
    border-color: lightgray;
    line-height: 2;
    margin-bottom: 30px;
    padding: 2.5rem 1.5rem;
    box-shadow: 0 1px 5px 0 rgba(0, 0, 0, 0.3);
  }
  .card-section {
    flex: 0 0 50%;
  }
  .btn-primary {
    vertical-align: top;
    background-color: #f2f2f2;
    border-radius: 0.125rem;
    border-bottom-width: 4px;
    border-color: #dedede;
    font-weight: 700;
    display: inline-block;
    text-transform: uppercase;
    outline: 0;
    position: relative;
    text-align: center;
    font-size: 0.875rem;
    color: #353537;
    line-height: 1.25;
    appearance: none;
    padding: 12px 16px;
    transition: colour 0.2s ease, background-colour 0.2s ease, border 0.2s ease,
      padding 0.2s ease;
    &:hover,
    &:focus {
      background-color: #238e6b;
      background-color: #dedede;
      border-bottom-width: 0;
      outline: 0;
      color: #fff;
      padding: 14px 16px;
    }
  }
  .btn-orange {
    background-color: #ee7836;
    border-color: #ce5311;
    color: #fff;
    &:hover,
    &:focus {
      background-color: #ce5311;
    }
  }
  .btn-green {
    background-color: #45b490;
    border-color: #238e6b;
    color: #fff;
    &:hover,
    &:focus {
      background-color: #238e6b;
    }
  }
  @media (min-width: 768px) {
    .card {
      flex: 0 0 49%;
    }
  }
}
</style>
