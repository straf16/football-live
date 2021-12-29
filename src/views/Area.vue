<template>
  <div class="wrapper">
    <div class="page-link" v-on:click="handleBack">
      BACK
    </div>
    <span class="page-title">
      Selected Area: {{ this.$route.query.select }}
    </span>
    <div class="container" v-if="teams.length > 0">
      <Card
        v-for="team in teams"
        v-bind:key="team.id"
        :id="team.id"
        :name="team.name"
        :linkTo="'About'"
      />
    </div>
    <div class="empty" v-else-if="loading">
      <span class="page-title">
        Please wait!
      </span>
    </div>
    <div class="empty" v-else>
      <span class="page-title">
        Sorry, Data not found
      </span>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Card from '@/components/Card.vue'
import axios from 'axios'

export default Vue.extend({
  name: 'Area',
  components: {
    Card
  },
  data() {
    return {
      loading: false,
      teams: []
    }
  },
  methods: {
    fetchTeam: function() {
      axios({
        method: 'GET',
        url: `https://api.football-data.org/v2/teams?areas=${this.$route.params.areaId}`,
        headers: { 'X-Auth-Token': '0e7a5cbdc3d740188391d541fc010011' }
      })
        .then((response) => {
          if (response.data.teams) {
            this.teams = response.data.teams
          }
          this.loading = false
        })
        .catch(err => {
          console.log(err)
        })
    },
    handleBack: function() {
      window.history.back()
    }
  },
  created() {
    this.loading = true
    this.fetchTeam()
  }
})
</script>

<style scoped>
  .page-title{
    font-size: 24px;
  }

  .page-link {
    font-size: 16px;
    color: #42b983;
    margin-bottom: 16px;
  }

  .container {
    display: grid;
    grid-template-columns: repeat(4, 2fr);
    grid-template-rows: auto;
    column-gap: 8px;
    row-gap: 8px;
    margin: 16px 0;
  }

  .empty {
    display: flex;
    justify-content: center;
    padding: 16px 8px;
  }

  @media only screen and (max-width: 600px) {
    .container {
      display: flex;
      flex-direction: column;
      margin: 8px 0;
    }

    .page-title {
      font-size: 20px;
    }
  }
</style>
