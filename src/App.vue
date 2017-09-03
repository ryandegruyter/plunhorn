<template>
  <div id="app">
    <app-title></app-title>
  </div>
</template>

<script lang="ts">
  import AppTitle from './components/title.vue';
  import Vue from 'vue'
  import Component from 'vue-class-component'

  @Component({
    components:{
      appTitle: AppTitle
    }
  })
  export default class App extends Vue {
  }
</script>

<style>
  html, body {
    height: 100%;
  }

  .title {
    text-transform: uppercase;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    background-color: #000;
    height: 100%;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
</style>
