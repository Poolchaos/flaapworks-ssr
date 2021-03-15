<template>
  <div id="contact">
    <div class="flex--position-center-v mar--auto">
      <img alt="Flaapworks logo" class="logo" src="../static/quote-150.png">
      <div class="flex flex--justify-around flex--direction-cols mar--t-20 mar--b-20">

        <form class="vue-form" @submit.prevent="submit">

          <div class="dialog">
            <div class="dialog--header flex flex--direction-cols flex--justify-between pad-20">
              <span v-if="$route.name==='Contact'"
                class="large-font red-text">How can we <b>HELP</b> you?</span>
              <span v-if="$route.name==='Quote'"
                class="large-font red-text">Get a <b>FREE</b> {{ $route.params.id }} Contact</span>
            </div>

            <div class="dialog--content gray flex flex--direction-cols flexjustify---around">
              <div class="flex relative error-wrap">
                <div class="error error--top error--right rounded-2"
                  v-if="errors.name">{{errors.name}}</div>
                <input type="text"
                  placeholder="* Enter Your Name"
                  v-model="name"
                  class="small-font flex--fill gray white-text white-border"
                  :class="{ 'hasValue' : name.length }" />
              </div>
              <div class="flex relative error-wrap">
                <input type="text"
                  placeholder="   Number"
                  v-model="phone"
                  class="small-font flex--fill"
                  :class="{ 'hasValue' : phone.length }" />
              </div>
              <div class="flex relative error-wrap">
                <div class="error error--top error--right rounded-2"
                  v-if="errors.email">{{errors.email}}</div>
                <input type="text"
                  placeholder="* Email"
                  v-model="email"
                  class="small-font flex--fill"
                  :class="{ 'hasValue' : email.length }" />
              </div>
              <div class="flex relative mar-5-20">
                <select v-model="service"
                  :class="{ 'hasValue' : service }"
                  v-if="$route.name==='Quote'">
                  <option value="">Choose...</option>
                  <option value='website'>Website</option>
                  <option value="webApplication">Web Application</option>
                  <option value="brochure">Brochure Site</option>
                  <option value="eCommerce">E-Commerce</option>
                  <option value="seo">SEO</option>
                  <option value="consulting">Consulting</option>
                </select>
              </div>
              <div class="flex relative error-wrap"
                v-if="$route.name==='Quote' && (service === 'website' || service === 'webApplication')">
                <input type="number"
                  placeholder="* Number of pages"
                  v-model="pages"
                  class="small-font flex--fill"
                  min="0"
                  :class="{ 'hasValue' : pages !== null && pages !== '' }" />
              </div>
              <div class="flex flex--direction-rows"
                v-if="$route.name==='Quote' && (service !== 'seo' && service !== 'consulting')">
                <div class="flex--position-center-v pad--l-20 pad--r-20">Do you need a design?</div>
                <Toggle @change="designCheck"/>
              </div>
              <div class="flex relative error-wrap">
                <div class="error error--top error--right rounded-2"
                  v-if="errors.message">{{errors.message}}</div>
                <textarea type="text"
                  id="text-area"
                  class="small-font flex--fill"
                  placeholder="* Add some notes or context"
                  v-model="message"
                  :class="{ 'hasValue' : message.length }"
                  v-on:input="updateHeight()"
                ></textarea>
              </div>
            </div>

            <div v-if="messageSent" class="background--gray text--white pad--all-20">
              <div>Your message has been sent.</div>
              We will be in contact with you shortly
            </div>

            <div class="dialog--footer pad-20">
              <div style="display: flex;justify-content: center;">

                <button
                  class="hoverable font--large background--red text--white pad--all-20 mar--t-20 rounded-5 relative"
                  @click="submitContact()"
                  :disabled="submitted"
                  v-if="$route.name==='Contact'">
                  Submit
                </button>

                <button
                  class="hoverable font--large background--red text--white pad--all-20 mar--t-20 rounded-5 relative"
                  @click="getQuote()"
                  :disabled="submitted"
                  v-if="$route.name==='Quote'">
                  Request a <b>FREE</b> Contact
                </button>

              </div>
            </div>
          </div>

        </form>

      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import axios from 'axios'

import Toggle from '../components/Toggle.vue'

import { init } from 'emailjs-com'
init('user_HB0sidICvn4VKjVvChK57')

export default class Contact extends Vue {
  errors: { [key: string]: string } = { name: '', email: '', message: '' }
  submitted = false
  messageSent = false
  name = ''
  phone = ''
  email = ''
  service = ''
  pages = null
  requireDesign = false
  message = ''
  
  components = {
    Toggle
  }
  
  mounted () {
    this.$nextTick(() => {
      if (this.$route.params.id) {
        this.service = this.$route.params.id
      }
    })
  }

  updateHeight () {
    const element: HTMLElement | null = document.querySelector('#text-area')
    if (element && element.scrollHeight > 100) {
      if (element.scrollHeight < 500) {
        element.style.cssText = 'height: auto;overflow-y: hidden;'
      } else {
        element.style.cssText = 'height: auto;'
      }
      element.style.cssText = 'height:' + (element.scrollHeight - 10) + 'px'
    }
  }

  designCheck (event: { target: HTMLInputElement }) {
    this.requireDesign = event.target.checked
  }

  validateEmail () {
    // eslint-disable-next-line
    const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    return re.test(this.email)
  }

  validate () {
    this.errors = { name: '', email: '', message: '' }
    let error = false

    return new Promise((resolve, reject) => {
      if (!this.name || this.name.length === 0) {
        this.errors.name = 'Please enter your name.'
        error = true
      }
      if (!this.email || this.email.length === 0) {
        this.errors.email = 'Please enter your email.'
        error = true
      } else if (!this.validateEmail()) {
        this.errors.email = 'Please enter a valid email.'
        error = true
      }
      if (!this.message || this.message.length === 0) {
        this.errors.message = 'Please enter your message.'
        error = true
      }
      console.log(' ::>> this.errors >>>> ', this.errors)

      if (error) {
        reject(new Error(''))
      } else {
        resolve({})
      }
    })
  }

  clearForm () {
    this.name = ''
    this.phone = ''
    this.email = ''
    this.service = ''
    this.pages = null
    this.requireDesign = false
    this.message = ''
  }

  submitContact () {
    this.submitted = true

    this.validate()
      .then(() => {
        console.log('form is valid')
        this.sendEmail()
      })
      .catch(() => {
        console.log('form is invalid')
        this.submitted = false
      })
  }

  getQuote () {
    this.submitted = true

    this.validate()
      .then(() => {
        console.log('form is valid')
        this.sendEmail()
      })
      .catch(() => {
        console.log('form is invalid')
        this.submitted = false
      })
  }

  sendEmail () {
    const emailContent = {
      name: this.name,
      phone: this.phone,
      email: this.email,
      service: this.service,
      pages: this.pages,
      requireDesign: this.requireDesign,
      message: this.message
    }
    console.log(' ::>> submit ', emailContent)

    axios.defaults.headers.post['Content-Type'] = 'application/json'
    axios
      .post('https://api.emailjs.com/api/v1.0/email/send', {
        // eslint-disable-next-line
        user_id: 'user_HB0sidICvn4VKjVvChK57',
        // eslint-disable-next-line
        service_id: 'service_d6die1r',
        // eslint-disable-next-line
        template_id: 'template_8ld8gcv',
        // eslint-disable-next-line
        template_params: emailContent
      })
      .then(() => {
        this.clearForm()
        this.messageSent = true
        this.submitted = false

        setTimeout(() => {
          this.messageSent = false
        }, 4000)
      })
      .catch(() => {
        console.log(' ::>> failed to send email')
        this.submitted = false
      })
  }
}

</script>

<style scoped lang="scss">
#contact {
  padding: 40px 0 50px 0;
  width: 500px;
  margin: auto;

  @media screen and (max-width: 500px) {
    width: 95%;
  }

  .logo {
    width: 150px;
    height: 150px;
  }
}
</style>
