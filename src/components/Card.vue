<template>
  <div id="card" v-on:click="handleClick">
    <span>{{name}}</span>
  </div>
</template>

<script lang="ts">
import router from '@/router'
import Vue from 'vue'

export default Vue.extend({
  name: 'Card',
  props: [ 'id', 'name', 'linkTo' ],
  methods: {
    handleClick: function() {
      router.push({ name: this.linkTo, params: { areaId: this.id }, query: { select: this.name} })
    }
  }
})
</script>

<style scoped>
  #card {
    padding: 24px 16px;
    margin: 8px;
    border-radius: 8px;
    background-color: #e7ecf3;
    text-align: center;
  }
</style>