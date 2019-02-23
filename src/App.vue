<template>
  <div id="app">
    <h1>Watchers</h1>
    <p>Watchers allow us to watch a prop of the data obj or computed prop for changes</p>
    <p>Change the value after a delay</p>
    <input type="text" v-model="inputValue">
    <p>Five seconds ago, the input said "{{ oldInputValue }}".</p>
    <h2>Filters</h2>
    <p>Filters are great for changing data as they are written to the template.</p>
    <p>Filters are also more readable than formatting data in the template.</p>
    <p>Product one cost: {{ productOneCost | formatCost }}</p>
    <p>Product two cost: {{ productTwoCost | formatCost }}</p>
    <p>Product three cost: {{ productThreeCost | formatSymbol('¥') }}</p>
    <p>The other format for vue filters are: 
      <code>
        Vue.filter('filtername', function(params) {
          return param;
        });
      </code>
      <br>
      ... which is good for registering code for use all over the app.
      Caveats:<br>
      - can't use this
      - they can only be used in interpolation and with v-bind directives
    </p>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      count: 0,
      inputValue: '',
      oldInputValue: '',
      formData: {
        userName: ''
      },
      productOneCost: 998,
      productTwoCost: 2399,
      productThreeCost: 5300
    }
  },
  watch: {
    inputValue() {
      const newValue = this.inputValue;

      setTimeout(() => {
        this.oldInputValue = newValue;
      }, 5000)
    },
    'formData.userName' (val, oldVal) {
      // this.formData userName has been changed
      // watchers are passed 2 args when the prop is changed
      // the new val and the old val
      // this is useful for seeing what changed
    },
    count() {
      // this count has changed
    }
  },
  filters: {
    formatCost(value) {
      return '$' + (value / 100).toFixed(2)
    },
    formatSymbol(value, symbol) {
      return symbol + (value / 100).toFixed(2)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
