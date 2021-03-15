<template>
  <div class="profile">
    <div class="flex--position-center-v mar--auto">
      <img alt="Flaapworks logo" class="logo" src="../static/profile-150.png">

      <div id="hexcontainer">
        <div class="hex1 hoverable" :class="{ 'showHover' : isProfile }">
          <div class="hex2">
            <div
              id="profile"
              class="hexlink"
              @click="viewProfile()"
            >
              <div class="hexcover" />
              <h3>About</h3>
              <div class="plus" />
            </div>
          </div>
        </div>
        <div class="hex1 hoverable" :class="{ 'showHover' : isHistory }">
          <div class="hex2">
            <div
              id="testimonial"
              class="hexlink"
              @click="viewHistory()"
            >
              <div class="hexcover" />
              <h3>History</h3>
              <div class="plus" />
            </div>
          </div>
        </div>
      </div>

      <div v-if="isProfile" class="description font--medium">
        <div class="font--large mar--b-20">
          Phillip-Juan van der Berg
        </div>
        I am a highly motivated, adaptable person with a strong positive outgoing personality, who enjoys dealing with a wide variety of people and situations. I work well under pressure and can be described as enthusiastic and passionate. I am conscientious, hard working, committed and self-motivated. I enjoy relating to people.
      </div>

      <div v-if="isHistory" class="description description--left">
        <div
          v-for="item in history"
          :key="item.company"
          class="flex flex--direction-cols pad--b-20"
        >
          <div class="company--wrap flex flex--direction-rows">
            <span class="font--large">
              <a class="flex flex--direction-rows inherit-text hoverable--underlined" :href="item.url" target="_blank">
                {{ item.company }}
              </a>
            </span>&nbsp;
            <span class="company--type font--medium flex--position-end-v">({{ item.softwareType }})</span>
          </div>
          <span class="font--medium mar--b-10">{{ item.role }}</span>
          <div
            v-for="(resp, index) in item.responsibilities"
            :key="index"
            class="flex flex--direction-cols font--small"
          >
            {{ resp }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import { EMPLOYMENT_HISTORY } from '../assets/enums/employment-history'

export default Vue.extend({
  data () {
    return {
      isProfile: true,
      isHistory: false,
      history: EMPLOYMENT_HISTORY,

      viewProfile () {
        this.isProfile = true
        this.isHistory = false
      },

      viewHistory () {
        this.isProfile = false
        this.isHistory = true
      }
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.profile {

  #hexcontainer {
    margin-bottom: 50px;
  }

  .description {
    margin: 20px auto;
    max-width: 500px;

    @media screen and (max-width: 500px) {
      width: 95%;

      .company {
        &--wrap {
          flex-direction: column;
        }
        &--type {
          align-self: flex-start!important;
        }
      }
    }

    &--left {
      text-align: left;
    }
  }

  .logo {
    width: 150px;
    height: 150px;
  }

  a {
    color: var(--gray)
  }
}
</style>
