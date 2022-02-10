<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <DropdownListAutocomplete :dropdowndata="dropdowndata"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import DropdownListAutocomplete from './components/DropdownListAutocomplete.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    DropdownListAutocomplete
  },
  data () {
    return {
      dropdowndata: [
        {id:0, text:'00000000'},
        {id:1, text: '1111111111'}, 
        {id:2, text: '2222222'},
        {id:3, text: '33333333'},
        {id:4, text: '44444444'},
        {id:5, text: '55555555'},
        {id:6, text: '66666666'},
        {id:7, text: '77777777'},
        {id:8, text: '8888888'},
        {id:9, text: '99999999'},
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
