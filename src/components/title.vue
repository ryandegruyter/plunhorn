<template>
  <div class="container">
    <!--<h1 class='title'>Plunging Hornet</h1>-->
    <h1 @mouseover='onTitleHover'
        class='f2'
        @mouseout='onMouseOut'><span>[</span>dangersun<span>]</span></h1>
    <p class='coming-soon'>coming soon</p>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'
  import Component from 'vue-class-component';
  import 'gsap';
  import {Strong, Bounce, Elastic, Circ, TweenMax, TimelineLite} from 'gsap';

  @Component({})
  export default class AppTitle extends Vue {

    comingSoon;
    brackets;
    timeLineLite = new TimelineLite();
    blue = '96CCFF';
    gold = 'FFD700';

    mounted() {
      this.comingSoon = this.$el.querySelector('.coming-soon');
      this.brackets = this.$el.querySelectorAll('h1 span');
      console.log(this.brackets[0]);
      this.timeLineLite.pause();
      this.timeLineLite.from(this.brackets[0], 0.5, {autoAlpha: 0, x: '-.5em', ease: Circ.easeInOut});
      this.timeLineLite.from(this.brackets[1], 0.5, {autoAlpha: 0, x: '.5em '}, '-=0.5');
      this.timeLineLite.fromTo(this.comingSoon, 0.6, {alpha: 0, y: -25}, {alpha: 1, ease: Circ.easeInOut, y: -10}, '-=0.5');
      this.timeLineLite.to(this.comingSoon, 0.5, {color: this.createColor(this.gold), ease: Circ.easeInOut}, '-=0.3');
    }

    createColor(color: string): string {
      return `#${color}`;
    }

    onMouseOut() {
      this.timeLineLite.reverse();
    }

    onTitleHover() {
      this.timeLineLite.restart();
    }
  }
</script>

<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    height: 100%;
    justify-content: center;
    align-items: center;
    color: #fff;
  }

  .coming-soon {
    margin-top: 8px;
  }

  h1 {
    padding-bottom: .5em;
    cursor: pointer;
    font-family: 'Jura', sans-serif;
    /*font-family: 'Tenor Sans', sans-serif;*/
    margin: 0;
  }

  h1 span {
    color: #FFD700;
    display: inline-block;
    margin: 0 .5em;
  }
</style>
