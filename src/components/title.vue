<template>
  <div class="container">
    <h1>Plunging Hornet</h1>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'
  import Component from 'vue-class-component'

  @Component({})
  export default class AppTitle extends Vue {
  }
</script>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: center;
    align-items: center;
  }

  h1 {
    color: #fff;
    margin: 0;
    text-transform: uppercase;
  }
</style>
