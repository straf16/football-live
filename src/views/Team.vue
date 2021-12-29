<template>
  <div class="wrapper">
    <div class="page-link" v-on:click="handleBack">
      BACK
    </div>
    <span class="page-title">
      Team: {{ this.$route.query.select }}
    </span>
    <div id="detail">
      <div id="team-profile">
        <div id="image-wrapper">
          <img :src="team.crestUrl" class="logo" />
        </div>
        <div id="information">
          <div class="row">
            <span class="field">Name: </span><span class="bold">{{this.team.name}}</span>
          </div>
          <div class="row">
            <span class="field">Founded: </span><span class="bold">{{this.team.founded}}</span>
          </div>
          <div class="row">
            <span class="field">Squad size: </span>
            <span class="bold">{{this.team.squad.length > 0 ? this.team.squad.length : 'Squad Not Found'}}</span>
          </div>
          <div class="row">
            <span class="field">Stadium: </span><span class="bold">{{this.team.venue}}</span>
          </div>
          <div class="row">
            <span class="field">Colors: </span><span class="bold">{{this.team.clubColors}}</span>
          </div>
          <div class="row">
            <span class="field">Address: </span><span class="bold">{{this.team.address}}</span>
          </div>
          <div class="row">
            <span class="field">Website: </span><a class="bold" :href="team.website">Visit Website</a>
          </div>
        </div>
      </div>
      <div>
        <SquadList :squad="team.squad"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'
import SquadList from '@/components/SquadList.vue'

export default Vue.extend({
  name: 'Team',
  components: {
    SquadList
  },
  data() {
    return {
      loading: false,
      team: {}
    }
  },
  methods: {
    handleBack: function() {
      window.history.back()
    },
    fetchTeamDetail: function () {
      axios({
        method: 'GET',
        url: `https://api.football-data.org/v2/teams/${this.$route.params.id}`,
        headers: { 'X-Auth-Token': '0e7a5cbdc3d740188391d541fc010011' }
      })
        .then((response) => {
          if (response.data) {
            this.team = response.data
          }
          this.loading = false
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  created() {
    this.fetchTeamDetail()
  }
})
</script>

<style scoped>
  .page-title{
    font-size: 18px;
  }

  .page-link {
    font-size: 16px;
    color: #42b983;
    margin-bottom: 16px;
  }

  #detail {
    display: flex;
    flex-direction: column;
    margin: 48px 0;
    padding: 16px;
    background-color: #f8f8f8;
    border-radius: 12px;
  }

  #team-profile {
    display: flex;
    margin-bottom: 48px;
  }

  #image-wrapper {
    background-color: white;
    width: 180px;
    height: 220px;
  }

  .logo {
    width: 100%;
    height: 100%;
  }

  #information {
    margin-left: 50px;
    font-size: 24px;
  }

  .row {
    display: grid;
    grid-template-columns: 200px auto;
    align-items: center;
  }

  .bold {
    font-weight: 500;
  }

  .field {
    font-size: 18px;
  }

  @media only screen and (max-width: 800px) {
    .page-title {
      font-size: 20px;
    }

    #team-profile {
      flex-direction: column;
      width: 100%;
    }

    #image-wrapper {
      width: 130px;
      height: 160px;
      align-self: center;
    }

    .row {
      display: grid;
      grid-template-columns: 70px auto;
      align-items: flex-start;
    }

    #information {
      margin-top: 16px;
      margin-left: 0px;
      font-size: 14px;
    }

    .field {
      font-size: 11px;
    }
  }
</style>