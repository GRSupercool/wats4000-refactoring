<template>
  <div>
    <div v-if="errorList.length > 0">
      <h2>There was an error fetching data.</h2>
      <ul class="errors">
        <li v-for="(error, index) in errorList" :key="index">{{ error }}</li>
      </ul>
    </div>
    <div v-else>
        <h2>Loading...</h2>
  </div>
</template>

<script>
export default {
  name: 'ErrorList',
  data () {
    return {

    }
  },
  props: {
    errorList: []
  }
}
</script>

<style scoped>
  .errors li {
    color: red;
    border: solid red 1px;
    padding: 5px;
  }
</style>