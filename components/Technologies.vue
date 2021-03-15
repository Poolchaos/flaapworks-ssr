<template>

  <div class="technology">
    <div class="flex--position-center-v mar--auto">
      <img alt="Flaapworks logo" class="logo" src="../static/testimonials-150.png">

      <div id="hexcontainer">

        <div class="hex1 hoverable" v-for="item in stack" :key="item.name">
          <div class="hex2">
            <div class="hexlink skill">
              <div class="hexcover"></div>
              <div class="image" :class="'image-' + item.name"></div>
              <h3>{{ item.label }}</h3>
            </div>
          </div>
        </div>

      </div>

    </div>
  </div>

</template>

<script lang="ts">
import Vue from 'vue'

import { TOOLS } from '../assets/enums/tools'

export default Vue.extend ({
  data () {
    return {
      stack: TOOLS
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.technology {

  #hexcontainer {
    margin: 30px 0 50px 0;

    .hex1 {
      margin: 0px 10px;
    }
  }

  .logo {
    width: 150px;
    height: 150px;
  }

  .hex1, h3 {
    cursor: default;
  }
}
</style>
