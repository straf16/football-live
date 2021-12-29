<template>
  <div id="navbar">
    <span>Football Live</span>
 </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'Navbar'
})
</script>

<style scoped>
  #navbar {
    padding: 24px;
    background-color: #42b983;
  }

  #navbar > span {
    font-size: 24px;
    font-weight: bold;
  }

  @media only screen and (max-width: 600px) {
    #navbar {
      padding: 16px;
    }

    #navbar > span {
      font-size: 18px;
    }
  }

</style>