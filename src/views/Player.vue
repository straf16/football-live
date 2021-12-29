<template>
  <div class="wrapper">
    <div class="page-link" v-on:click="handleBack">
      BACK
    </div>
    <span class="page-title">
      {{this.player.name}} Profile
    </span>
    <div id="detail">
      <div id="player-profile">
        <div id="information">
          <div class="row">
            <span class="field">Name: </span>
            <span class="bold">{{this.player.name ? this.player.name : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">First name: </span>
            <span class="bold">{{this.player.firstName ? this.player.firstName : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">Last name: </span>
            <span class="bold">{{this.player.lastName ? this.player.lastName : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">Date of birth: </span>
            <span class="bold">{{this.player.dateOfBirth ? this.player.dateOfBirth : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">Country of birth: </span>
            <span class="bold">{{this.player.countryOfBirth ? this.player.countryOfBirth : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">Nationality: </span>
            <span class="bold">{{this.player.nationality ? this.player.nationality : '-'}}</span>
          </div>
          <div class="row">
            <span class="field">Position: </span>
            <span class="bold">{{this.player.position ? this.player.position : '-'}}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
import Vue from 'vue'

export default Vue.extend({
  name: 'Player',
  data() {
    return {
      player: {}
    }
  },
  methods: {
    handleBack: function() {
      window.history.back()
    },
    fetchPlayer: function() {
      axios({
        method: 'GET',
        url: `https://api.football-data.org/v2/players/${this.$route.params.id}`,
        headers: { 'X-Auth-Token': '0e7a5cbdc3d740188391d541fc010011' }
      })
        .then((response) => {
          if (response.data) {
            this.player = response.data
          }
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  created() {
    this.fetchPlayer()
  }
})
</script>

<style scoped>
  .page-link {
    font-size: 16px;
    color: #42b983;
    margin-bottom: 16px;
  }

  .page-title{
    font-size: 24px;
  }

  #detail {
    display: flex;
    flex-direction: column;
    margin: 16px 0 48px;
    padding: 16px;
    background-color: #f8f8f8;
    border-radius: 12px;
  }

  #player-profile {
    display: flex;
  }

  #information {
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

    #player-profile {
      flex-direction: column;
      width: 100%;
    }

    .row {
      display: grid;
      grid-template-columns: 100px auto;
      align-items: flex-start;
    }

    #information {
      font-size: 18px;
    }

    .field {
      font-size: 12px;
    }
  }
</style>