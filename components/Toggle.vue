<template>
  <div id="switch">
    <label class="switch flex">
      <label for="check" class="text font--small flex--position-center-v">{{ selected ? 'Yes' : 'No' }}</label>
      <input id="check" type="checkbox" v-model="selected" />
      <span class="slider round"></span>
    </label>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend ({
  data () {
    return {
      selected: false
    }
  }
})
</script>

<style scoped lang="scss">
#switch {
  cursor: pointer;

  .switch {
    position: relative;
    width: 110px;
    height: 34px;
  }

  /* Hide default HTML checkbox */
  .switch input {
    opacity: 0;
    width: 0;
    height: 0;
  }

  .text {
    position: absolute;
    left: 35%;
    cursor: pointer;
    z-index: 2;
    color: var(--white);
    -webkit-transition: .4s;
    transition: .4s;
  }

  /* The slider */
  .slider {
    position: absolute;
    cursor: pointer;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: var(--red);
    color: var(--white);
    -webkit-transition: .4s;
    transition: .4s;
  }

  .slider:before {
    position: absolute;
    content: "";
    height: 26px;
    width: 26px;
    left: 4px;
    bottom: 4px;
    background-color: white;
    -webkit-transition: .4s;
    transition: .4s;
  }

  input:checked + .slider {
    background-color: var(--gray);
  }

  input:focus + .slider {
    box-shadow: 0 0 1px var(--gray);
  }

  input:checked + .slider:before,
  input:checked + .text:before {
    -webkit-transform: translateX(76px);
    -ms-transform: translateX(76px);
    transform: translateX(76px);
  }

  /* Rounded sliders */
  .slider.round {
    border-radius: 34px;
  }

  .slider.round:before {
    border-radius: 50%;
  }
}
</style>
