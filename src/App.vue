<template>
  <div id="app">
    <div>
      <VueOTPField :onFieldCompleted="onFieldCompleted" :onFill="onFill" />
    </div>
  </div>
</template>

<script>
import VueOTPField from '@/components/VueOTPField'

export default {
  name: 'app',
  components: {
    VueOTPField
  },
  methods: {
    onFieldCompleted (value) {
      console.log('SUBMITTING')
    },
    onFill (inputObj) {
      console.log(inputObj)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
