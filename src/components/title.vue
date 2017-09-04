<template>
  <div class="container">
    <!--<h1 class='title'>Plunging Hornet</h1>-->
    <h1 @mouseover='onTitleHover'
        class='f2'
        @mouseout='onMouseOut'>
      <span v-bind:class="isGold ? 'yellow' : 'light-blue'">[</span>
      dangersun
      <span v-bind:class="isGold ? 'yellow' : 'light-blue'">]</span>
    </h1>
    <p class='coming-soon'>coming soon</p>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'
  import Component from 'vue-class-component';
  import 'gsap';
  import {Strong, TweenLite, Bounce, Elastic, Circ, TweenMax, TimelineLite} from 'gsap';

  @Component({})
  export default class AppTitle extends Vue {

    comingSoon;
    brackets;
    timeLineLite = new TimelineLite();
    blue = '96CCFF';
    gold = 'FFD700';

    isGold = true;

    mounted() {
      this.comingSoon = this.$el.querySelector('.coming-soon');
      this.brackets = this.$el.querySelectorAll('h1 span');
      this.resetTweens();
    }

    data() {
      return {
        isGold: this.isGold
      }
    }

    resetTweens(): void {
      this.isGold = Math.random() >= 0.5;
      for (let obj of this.timeLineLite.getChildren()) {
        this.timeLineLite.remove(obj);
      }
      this.timeLineLite.pause();
      this.timeLineLite.add(TweenLite.fromTo(this.brackets[0], 0.5, {alpha: 0, x: '-.5em'}, {
        alpha: 1,
        x: 0,
        ease: Circ.easeInOut
      }));
      this.timeLineLite.add(TweenLite.fromTo(this.brackets[1], 0.5, {alpha: 0, x: '.5em '}, {
        alpha: 1,
        x: 0,
        ease: Circ.easeInOut
      }), '-=0.5');
      this.timeLineLite.add(TweenLite.fromTo(this.comingSoon, 0.6, {alpha: 0, y: -25}, {
        alpha: 1,
        ease: Circ.easeInOut,
        y: -10
      }), '-=0.5');
      this.timeLineLite.add(TweenLite.to(
        this.comingSoon,
        0.5,
        {
          onReverseComplete: this.resetTweens,
          color: this.createColor(this.isGold ? this.gold : this.blue),
          ease: Circ.easeInOut
        }), '-=0.4');
      this.timeLineLite.getChildren();
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

<style scoped
       sass>
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

  @media only screen and (max-device-width: 480px) {
    h1 {
      font-size: 5em;
    }
    p{
      font-size: 3em;
    }
  }

  h1 {
    padding-bottom: .5em;
    cursor: pointer;
    font-family: 'Jura', sans-serif;
    /*font-family: 'Tenor Sans', sans-serif;*/
    margin: 0;
  }

  h1 span {
    display: inline-block;
    margin: 0 .5em;
  }
</style>
