<template>
  <div>
    <div class="nav nav--wide flex flex--direction-rows flex--justify-around">
      <a href="https://www.termsfeed.com/live/62e38a2e-09d0-489f-9c9a-dd4077fbd722" target="_blank">Terms and Conditions</a>
      <div class="divider">
        &#9830;
      </div>
      <span>Copyright © 2021 <a click.trigger="navigate('Flaapworks')">Flaapworks</a>. <!--anchor--> All Rights Reserved</span>
      <div class="divider">
        &#9830;
      </div>
      <a href="https://www.privacypolicies.com/live/26abdabd-88b3-4191-a0ef-763262d8ebdb" target="_blank">Privacy Policy</a>
    </div>

    <div class="nav nav--thin flex flex--direction-cols">
      <a href="https://www.termsfeed.com/live/62e38a2e-09d0-489f-9c9a-dd4077fbd722" target="_blank">Terms and Conditions</a>
      <a href="https://www.privacypolicies.com/live/26abdabd-88b3-4191-a0ef-763262d8ebdb" target="_blank">Privacy Policy</a>
      <img alt="Flaapworks" class="logo" src="../static/logo-150.png">
      <span>Copyright © 2021 Flaapworks. All Rights Reserved</span>
    </div>
  </div>
</template>

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
    .logo {
      width: 40px!important;
      margin: 10px auto;
    }
  }
}
</style>
