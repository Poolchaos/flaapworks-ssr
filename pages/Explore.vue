<template>
  <div class="explore" :class="deviceType">

    <transition name="slide-fade" mode="out-in">
      <div class="flex--position-center-v mar--auto" v-if="isExploreHome" key="home">
        <img alt="Flaapworks logo" class="logo" src="../static/explore-150.png">
        <div class="flex flex--justify-around">

          <div id="hexcontainer" class="flex">

            <div class="hex1 hoverable">
              <div class="hex2">
                <div class="hexlink" id="projects"
                  @click="viewProjects()">
                  <div class="hexcover"></div>
                  <h3>Projects</h3>
                  <div class="plus"></div>
                </div>
              </div>
            </div>
            <div class="hex1 hoverable">
              <div class="hex2">
                <div class="hexlink" id="technology"
                  @click="viewTechnologies()">
                  <div class="hexcover"></div>
                  <h3>Tech</h3>
                  <div class="plus"></div>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </transition>

    <transition name="slide-fade" mode="out-in">
      <div key="Projects" class="relative" v-if="isProjects">
        <button class="btn--back font--large" title="Back"
          @click="showExploreHome()">&#60;</button>
        <Projects/>
      </div>
    </transition>

    <transition name="slide-fade" mode="out-in">
      <div key="Technology" class="relative" v-if="isTechnologies">
        <button class="btn--back font--large" title="Back"
          @click="showExploreHome()">&#60;</button>
        <Technologies/>
      </div>
    </transition>

  </div>
</template>

<script lang="ts">
import Vue from 'vue'

import Technologies from '../components/Technologies.vue'
import Projects from '../components/Projects.vue'

import DeviceDetector, { DeviceDetectorResult } from 'device-detector-js'
const deviceDetector = new DeviceDetector()
const device: DeviceDetectorResult = deviceDetector.parse(navigator.userAgent)

export default Vue.extend({
  components: {
    Technologies,
    Projects
  },
  data () {
    return {
      deviceType: device && device.device ? device.device.type : undefined,

      slideTime: 1000,
      isExploreHome: true,
      isProjects: false,
      isTechnologies: false,

      viewProjects () {
        this.hideExploreHome()
          .then(() => {
            this.isProjects = true
          })
      },

      viewTechnologies () {
        this.hideExploreHome()
          .then(() => {
            this.isTechnologies = true
          })
      },

      hideExploreHome () {
        return new Promise(resolve => {
          this.isExploreHome = false
          this.wait(this.slideTime, () => {
            resolve({})
          })
        })
      },

      showExploreHome () {
        this.isProjects = false
        this.isTechnologies = false

        this.wait(this.slideTime, () => {
          this.isExploreHome = true
        })
      },

      wait (waitTime: number, callback: () => void) {
        setTimeout(() => {
          callback()
        }, waitTime)
      }
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.explore {
  padding: 40px 0 50px 0;

  .logo {
    width: 150px;
    height: 150px;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
  }
  .slide-fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

  .slide-fade-enter,
  .slide-fade-leave-to {
    transform: translateY(-150px);
  }
}
</style>
