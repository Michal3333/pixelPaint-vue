<template>
  <div id="all">
    <Title v-bind:title="title"/>
    <div class="controlPanel">
      <ColorPicker class="picker" @colorSelect="changeColor"/>
      <ModeSelector class="mode"
        @modeSelection="handleModeSelection"/>
    </div>
    <div class="panel" v-bind:style="applyRowNumerStyle">
      <Pixel v-for="pixel in pixels"
        v-bind:key="pixel.id"
        v-bind:value="pixel"
        v-bind:color="color"
        @colorClick="paint"/>
    </div>
    <div class="inputR">
      <label for="resolution">Resolution : </label>
      <input name="resolution" class="resolution" v-model="rowsAmountInput"/> 
    </div>
    
  </div>
  
</template>

<script>
import Pixel from './Pixel.vue'
import ColorPicker from './ColorPicker.vue'
import ModeSelector from './ModelSelector.vue'
import Title from './Title.vue'


export default {
  name: 'Panel',
  components: {
    Pixel,
    ColorPicker,
    ModeSelector,
    Title
  },
  props: {
    msg: String
  },
  data () {
    return {
      styleGrid : {
        'grid-template-columns': 'repeat(7, 1fr [col-start])',
        'grid-template-rows': 'repeat(7, 1fr [col-start])',
      },
      pixels: [],
      rowsAmountInput: 20,
      color : "MediumSpringGreen",
      mode : 'single',
      maxRows: 40,
      title: 'PIXELPAINT'
    }
  },
  computed: {
    rowsAmount: function () {
      let value = 2;
      if(this.rowsAmountInput >= this.maxRows) {
        value = this.maxRows;
      }
      else if(this.rowsAmountInput > 2){
        value = this.rowsAmountInput;
      }
      return value;
    },
    applyRowNumerStyle: function () {
      return {
        'grid-template-columns': `repeat(${this.rowsAmount}, 1fr [col-start])`,
        'grid-template-rows': `repeat(${this.rowsAmount}, 1fr [col-start])`,
      }
    },
    
  },
  watch: {
    rowsAmount: function (newValue) {
      if(newValue >= this.maxRows){
        this.rowsAmountInput = newValue;
      }
      this.pixels = [];
      this.pixels = this.setCanvaSize(newValue);
      this.changeAllColors('white')
    }
  },
  methods: {
    setCanvaSize: function (amount) {
        let newPixels = [];
        for(let i = 0; i < amount * amount; i++){
          newPixels.push({
            id : i,
            color : "white"
          });
        }
        return newPixels;
    },
    changeColor : function (color) {
      this.color = color;
    },
    changeAllColors: function (color) {
      this.pixels = this.pixels.map(element => {
        element.color = color
        return element});
    },
    handleModeSelection: function (mode) {
      this.mode = mode;
    },
    paint: function () {
      if(this.mode === 'multi') this.changeAllColors(this.color);
    }
  },
  created : function () {
    this.pixels = this.setCanvaSize(this.rowsAmount);
  }
}
</script>

<style scoped>
.panel{
  width: 35vw;
  height: 35vw;
  min-width: 500px;
  min-height: 500px;
  display: grid;
  border: solid 5px gray;
}
.picker{
  height: auto;
  flex-basis: 80%;
  /* width: 100%; */
}
.controlPanel{
  display: flex;
  /* width: 100%; */
  align-items: stretch;
  min-height: 110px;
}
.mode{
  height: auto;
  flex-basis: 20%;
  /* width: 100%; */
  /* height: 100%; */
} 
#all{
  padding: calc(20px + 0.6vw);
  background-color:mintcream;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
  height: min-content;
  border: solid gray 3px
}
.resolution{
  
  /* font-size:calc(25px + 1.2vw); */
  font-size: 25px;
  border-width: 3px;
  text-align: center;
  width: 50%;
}
.inputR{
  width: 50%;
  min-height: 40px;
  margin-top: calc(10px + 0.5vw);
  display: flexbox;
  align-items: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;  
  /* font-size:calc(25px + 1.5vw); */
  color: rgb(70, 70, 70);
}

</style>
