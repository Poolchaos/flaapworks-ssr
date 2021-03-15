<template>
  <div class="testimonials">
    <div class="flex--position-center-v mar--auto">
      <img alt="Flaapworks logo" class="logo" src="../static/testimonials-150.png">

      <div class="flex flex--wrap flex--justify-around record">
        <div v-for="item in testimonials" :key="item.profile" class="testimony">
          <a class="flex flex--direction-rows inherit-text hoverable--underlined" :href="'https://www.linkedin.com/in/' + item.contactId + '/'" target="_blank">

            <div id="hexcontainer">
              <div class="hex1 hex1--small hoverable">
                <div class="hex2">
                  <div
                    :id="item.profile"
                    class="hexlink"
                    @click="viewTestimonials()"
                  />
                </div>
              </div>
            </div>

            <div class="description flex flex--direction-cols">
              <span class="font--medium name"><b>
                {{ item.name }}
              </b></span>
              <span>{{ item.position }}</span>
              <span class="font--tiny">{{ item.dateAndRelation }}</span>
            </div>
          </a>
          <span class="font--medium relative">
            <span class="font--large start-quote">&ldquo;</span>
            {{ item.testimony }}
            <span class="font--large">&rdquo;</span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import { TESTIMONIALS } from '../assets/enums/testimonials'

export default Vue.extend({
  data () {
    return {
      testimonials: TESTIMONIALS
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.testimonials {

  .record {
    text-align: left;

    .testimony {
      min-width:40%;
      width:40%;
      margin: 20px 0;

      @media screen and (max-width: 749px) {
        width: 450px;
      }

      @media screen and (max-width: 450px) {
        width: 95%;
      }
    }
    .profile {
      width: 100px;
      height: 100px;
      max-height: 100px;
      border-radius: 100%;
    }

    .description {
      color: var(--gray);
    }
  }
}
</style>
