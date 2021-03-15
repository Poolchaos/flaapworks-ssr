<template>
  <div class="services">
    <div class="flex--position-center-v mar--auto">
      <img alt="Flaapworks logo" class="logo" src="../static/services-150.png">
      <div class="flex flex--justify-around">

        <div id="hexcontainer" class="flex flex--direction-rows flex--justify-around flex--wrap">

          <div class="hex1 hoverable" v-for="(item, index) in services" :key="index" :class="{ 'showHover' : item.selected }">
            <div class="hex2">
              <div class="hexlink" :id="item.id" @click="select(item)">
                <div class="hexcover"></div>
                <h3>{{ item.name }}</h3>
                <div class="plus"></div>
              </div>
            </div>
          </div>

        </div>
      </div>
      <div v-if="serviceIsSelected" class="flex flex--direction-cols services--selected">
        <span class="font--large mar--b-20"><b>{{ service.name }}</b></span>
        <span class="font--medium description">{{ service.description }}</span>

          <router-link :to="'/quote/' + service.id">
            <button
              class="hoverable font--large background--red text--white pad--all-20 mar--t-20 rounded-5"
              click.trigger="getQuote()">
              Get a <b>FREE</b> Quote
            </button>
          </router-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import { SERVICES } from '../assets/enums/services'

export default class Services extends Vue.extend({
  data() {
    return {
      services: SERVICES
    }
  },
  watch: {
    $route () {
      this.services.forEach((service: { id: string; name: string; description: string; selected: boolean }) => {
        service.selected = false
      })
    }
  }
}) {
  services = SERVICES
  service = {}
  serviceIsSelected = false

  select (item: { id: string; name: string; description: string; selected: boolean }) {
    for (let i = 0; i < this.services.length; i++) {
      this.services[i].selected = false
    }
    item.selected = true
    this.serviceIsSelected = true
    this.service = item
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.services {
  padding: 40px 0 50px 0;

  &--selected {
    max-width: 650px;
    margin: auto;
  }

  .logo {
    width: 150px;
    height: 150px;
  }

  #hexcontainer {
    margin: 30px 0 50px 0;
    max-width: 650px;

    .hex1 {
      margin: 10px;
    }
  }

  .description {
    min-height: 90px;
  }
}
</style>
