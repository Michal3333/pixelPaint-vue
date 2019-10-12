<template>
  <div id="app" class="backgroud" v-bind:style="{backgroundColor: backgroundColor}">
    <Panel msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Panel from './components/Panel.vue'

export default {
  name: 'app',
  components: {
    Panel
  },
  data () {
    return {
      backgroundColor: '',
      currentColor: 180,
      maxGray: 200,
      minGray: 100,
      grayStep: 10,
      direction: 'down'
    }
  },
  methods: {
    generateColor: function () {
      let color = this.currentColor;
      if(this.direction === "down"){
        if(this.currentColor > this.minGray) this.currentColor -= this.grayStep;
        else this.currentColor = this.maxGray;
      }
      else{
        if(this.currentColor < this.maxGray) this.currentColor += this.grayStep;
        else this.currentColor = this.minGray;
      }
      return `rgb(${color}, ${color}, ${color})`
    }
  },
  created : function () {
    let that = this;
    this.backgroundColor = this.generateColor();
    setInterval(() => {
      that.backgroundColor = that.generateColor();
    },2000);
  }
}
</script>

<style>
  @import './assets/reset.css';
  .backgroud{
    transition-duration: 2.5s;
    height: 100vh;
    padding: 100px;
    display: flex;
    justify-content: center;
  }
</style>
