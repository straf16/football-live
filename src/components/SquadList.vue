<template>
  <div class="list">
    <div class="first-row">
      <span class="title-column">No.</span>
      <span class="title-column">Name</span>
      <span class="title-column">Nationality</span>
      <span class="title-column">Position</span>
    </div>
    <div class="squad-list" v-for="(player, index) in squad" v-bind:key="player.id">
      <span class="player-detail">{{ index + 1 }}</span>
      <span class="player-detail">{{ player.name }}</span>
      <span class="player-detail">{{ player.nationality }}</span>
      <span class="player-detail">{{ player.position }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'SquadList',
  props: ['squad'],
  methods: {
    getDate(date: Date) {
      return new Date(date).toDateString()
    }
  }
})
</script>

<style scoped>
  .list {
    padding: 16px;
  }

  .first-row {
    display: grid;
    grid-template-columns: 50px 300px 200px 150px;
    column-gap: 16px;
    row-gap: 8px;
  }

  .squad-list {
    display: grid;
    grid-template-columns: 50px 300px 200px 150px;
    grid-template-rows: 50px;
    column-gap: 16px;
    row-gap: 8px;
    align-items: center;
  }

  .title-column {
    font-size: 18px;
    font-weight: 500;
  }

  .player-detail {
    font-size: 18px;
    font-weight: bold;
  }

  @media only screen and (max-width: 600px) {
    .list {
      padding: 8px;
    }

    .first-row {
      display: grid;
      grid-template-columns: 15px 120px 80px 60px;
      column-gap: 8px;
      row-gap: 4px;
    }

    .squad-list {
      display: grid;
      grid-template-columns: 15px 120px 80px 60px;
      grid-template-rows: 50px;
      column-gap: 8px;
      row-gap: 4px;
      align-items: center;
    }

    .title-column {
      font-size: 11px;
      font-weight: 500;
    }

    .player-detail {
      font-size: 11px;
      font-weight: bold;
    }
  }
</style>