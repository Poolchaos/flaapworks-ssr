<template>
  <div class="about" :class="deviceType">

    <transition name="slide-fade" mode="out-in">
      <div class="flex--position-center-v mar--auto" v-if="isAboutHome" key="home">
        <img alt="Flaapworks logo" class="logo" src="../static/about-150.png">
        <div class="flex flex--justify-around">

          <div id="hexcontainer" class="flex">

            <div class="hex1 hoverable">
              <div class="hex2">
                <div class="hexlink" id="profile" @click="viewProfile()">
                  <div class="hexcover"></div>
                  <h3>Profile</h3>
                  <div class="plus"></div>
                </div>
              </div>
            </div>
            <div class="hex1 hoverable">
              <div class="hex2">
                <div class="hexlink" id="testimonial" @click="viewTestimonials()">
                  <div class="hexcover"></div>
                  <h3>Testimonials</h3>
                  <div class="plus"></div>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </transition>

    <transition name="slide-fade" mode="out-in">
      <div key="Profile" class="relative" v-if="isProfile">
        <button class="btn--back font--large" title="Back" @click="showAboutHome()">&#60;</button>
        <!-- <Profile/> -->
      </div>
    </transition>

    <transition name="slide-fade" mode="out-in">
      <div key="Testimonial" class="relative" v-if="isTestimonials">
        <button class="btn--back font--large" title="Back" @click="showAboutHome()">&#60;</button>
        <!-- <Testimonials/> -->
      </div>
    </transition>

  </div>
</template>

<script lang="ts">
import Vue from 'vue'

// import Testimonials from '../components/Testimonials.vue'
// import Profile from '../components/Profile.vue'

import DeviceDetector, { DeviceDetectorResult } from 'device-detector-js'
const deviceDetector = new DeviceDetector()
const device: DeviceDetectorResult = deviceDetector.parse(navigator.userAgent)

export default class Footer extends Vue {
  static components = {
    // Testimonials,
    // Profile
  }
  deviceType = device && device.device ? device.device.type : undefined

  slideTime = 1000
  isAboutHome = true
  isProfile = false
  isTestimonials = false
  viewProfile () {
    this.hideAboutHome()
      .then(() => {
        this.isProfile = true
      })
  }

  viewTestimonials () {
    this.hideAboutHome()
      .then(() => {
        this.isTestimonials = true
      })
  }

  hideAboutHome () {
    return new Promise(resolve => {
      this.isAboutHome = false
      this.wait(this.slideTime, () => {
        resolve({})
      })
    })
  }

  showAboutHome () {
    this.isProfile = false
    this.isTestimonials = false

    this.wait(this.slideTime, () => {
      this.isAboutHome = true
    })
  }

  wait (waitTime: number, callback: () => void) {
    console.log()
    setTimeout(() => {
      callback()
    }, waitTime)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.about {
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
