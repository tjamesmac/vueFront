<template>
  <div>
    <h2>{{ info.name }}</h2>
    <p v-html="info.description"></p>
    <ul v-if="info.variants">
      <li v-for="item in info.variants" :key="item.id">
        <input
          type="radio"
          v-bind:id="item.name"
          :name="'group' + info.name"
          v-bind:value="item.name"
        />
        <label v-bind:for="'group' + info.name" class="pl-2">
          <span class="font-weight-bold">{{ item.name }}</span> :
          <span class="font-weight-bold" style="text-decoration: line-through;">
            £{{ item.price / 100 }}
          </span>
          <span class="text-danger font-weight-bold">
            £{{ (item.price / 2 / 100).toFixed(2) }}
          </span>
        </label>
      </li>
    </ul>
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
  },
  mounted() {
    console.log(this.info);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
// li {
//   display: inline-block;
//   margin: 0 10px;
// }
a {
  color: #42b983;
}
</style>
