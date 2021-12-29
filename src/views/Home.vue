<template>
  <div class="home">
    <span class="page-title">
      Find Football Team by Area
    </span>
    <div class="container">
      <Card
        v-for="area in areas"
        v-bind:key="area.id"
        :id="area.id"
        :name="area.name"
        :linkTo="'Area'"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Card from '@/components/Card.vue'
import axios from 'axios'

export default Vue.extend({
  name: 'Home',
  components: {
    Card
  },
  data() {
    return {
      areas: []
    }
  },
  methods: {
    fetchArea: function() {
      axios({
        method: 'GET',
        url: 'https://api.football-data.org/v2/areas',
        headers: { 'X-Auth-Token': '0e7a5cbdc3d740188391d541fc010011' }
      })
        .then((response) => {
          if (response.data.areas) {
            this.areas = response.data.areas
          }
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  created() {
    this.fetchArea()
  }
});
</script>

<style scoped>
  .home {
    margin: 24px 48px;
  }

  .page-title {
    font-size: 24px;
  }

  .container {
    display: grid;
    grid-template-columns: repeat(4, 2fr);
    grid-template-rows: auto;
    column-gap: 8px;
    row-gap: 8px;
    margin: 16px 0;
  }

  @media only screen and (max-width: 600px) {
    .home {
      margin: 16px;
    }

    .container {
      display: flex;
      flex-direction: column;
      margin: 8px 0;
    }
  }
</style>
