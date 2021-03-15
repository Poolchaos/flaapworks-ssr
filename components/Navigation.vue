<template>
  <div>
    <div class="nav nav--wide flex flex--justify-around">
      <router-link to="/services">Services</router-link>
      <div class="divider">&#9830;</div>
      <router-link to="/explore">Explore</router-link>
      <router-link to="/">
        <div class="font--medium pad--all-10">Flaapworks</div>
      </router-link>
      <router-link to="/about">About</router-link>
      <div class="divider">&#9830;</div>
      <router-link to="/contact">Get In Touch</router-link>
    </div>

    <div class="nav nav--thin flex flex--justify-between">
      <div class="font--medium pad--all-10 identity flex">
        <img alt="Flaapworks" class="logo" src="../static/logo-150.png">
        <span class="flex--position-center-v">Flaapworks</span>
      </div>
      <div
        class="burger mar--all-10" @click="toggleBurger()">
        <div class="burger--handle hoverable">&#9776;</div>
        <div
          class="burger--items flex flex--direction-cols"
          v-bind:class="{ active: active }">
          <router-link to="/">Flaapworks</router-link>
          <router-link to="/services">Services</router-link>
          <router-link to="/explore">Explore</router-link>
          <router-link to="/about">About</router-link>
          <router-link to="/contact">Get In Touch</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'


export default Vue.extend({
  data() {
    return {
      active: false
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.nav {
  display: none;

  &--wide {
    @media screen and (min-width: 750px) {
      display: flex!important;
    }
  }
  &--thin {
    @media screen and (max-width: 749px) {
      display: flex!important;
    }
    .identity {
      font-weight: bold;
      text-transform: uppercase;

      .logo {
        height: 40px!important;
      }
    }
    .burger {
      position: relative;
      text-align: left!important;
      font-weight: bold;
      color: var(--gray);
      text-decoration: none;
      text-transform: initial;
      margin-right: 20px;

      &--handle {
        padding: 10px;
        border: 1px solid var(--gray);
        border-radius: 3px;
        text-align: center;
      }

      &--items {
        position: absolute;
        top: 100%;
        right: 0;
        width: 95px;
        border-radius: 3px;
        background-color: var(--gray);
        padding: 5px 10px;
        display: none;

        &.active {
          display: flex;
        }

        a {
          width: 100%;
          color: var(--white)!important;
          font-weight: 100;
          text-transform: unset;
          padding: 5px 0;
        }
      }
    }
  }
}
</style>