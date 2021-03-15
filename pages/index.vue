<template>
  <div class="disable-select">
    <Navigation/>
    <Footer/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import '../assets/css/main.scss';

import Navigation from '../components/Navigation.vue';
import Footer from '../components/Footer.vue';

export default Vue.extend({
  components: {
    Navigation,
    Footer
  }
})
</script>

<style lang="scss">
/* shared styles between navigation and footer */

.nav {
  position: relative;
  padding: 10px 30px;

  @media screen and (max-width: 500px) {
    padding: 10px 0;
  }

  a, .divider {
    align-self: center;
  }

  a {
    font-weight: bold;
    color: var(--gray);
    text-decoration: none;
    text-transform: uppercase;

    &.router-link-exact-active,
    &.a:hover {
      border-bottom: 1px solid var(--gray);
    }
  }

  .logo {
    height: 50px;
    width: 50px;
  }
}
</style>