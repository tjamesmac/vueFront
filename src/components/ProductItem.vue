<template>
  <div>
    <h2>{{ info.name }}</h2>
    <p v-html="info.description"></p>
    <button
      class="btn btn-primary btn-green"
      aria-label="Find out more about this product"
    >
      More about this product
    </button>
  </div>
</template>

<script>
export default {
  name: "ProductItem",
  props: {
    info: Object
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
  list-style-type: none;
  padding: 0;
}
</style>
