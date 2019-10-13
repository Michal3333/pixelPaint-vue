<template>
    <div class="colorPicker">
        <Color 
            v-for="color in colorsTab"
            v-bind:key="color.id"
            v-bind:info="color"
            @colorSelect="changeColor"/>
    </div>
    
</template>

<script>
import Color from './Color'

export default {
    name: 'ColorPicker',
    components: {
        Color
    },
    data () {
        return {
            colorsTab : [],
            baseColors : ['black', 'white',
                'darkred', 'crimson', 'orangered', 'yellow',
                'greenyellow', 'yellowgreen','forestgreen', 'darkgreen',
                'mediumblue', 'steelblue', 'DeepSkyBlue','turquoise', 'Teal',
                'lightcyan', 'lightgray', 'BlanchedAlmond', 'tan', 'saddlebrown'],
            id : 0,
        }
    },
    methods: {
        addBaseColors : function () {
            this.colorsTab = this.baseColors.map((color, nr) => ({id : nr, color : color, selected: false}));
            let first = this.colorsTab[0];
            first.selected = true;
            this.emitColor(first.color);
            this.id = this.colorsTab.length;
        },
        emitColor : function (color) {
            this.$emit("colorSelect", color);
        },
        changeColor : function (color, id) {
            this.emitColor(color);
            this.colorsTab.forEach(element => {
                element.selected = false;
            });
            let selected = this.colorsTab.find((element) => element.id === id);
            selected.selected = true;
        }

    },
    created: function () {
        this.addBaseColors()

    }
}
</script>

<style scoped>
.colorPicker{
    /* width: 100%; */
    height: auto;
    grid-template-columns: repeat(10, 1fr [col-start]);
    grid-auto-rows : min-content;
    display: grid;
    grid-gap: 10px 5px;
    padding: 10px;
    background-color: rgb(200, 200, 200);
    border: solid gray 5px;
    border-bottom: none;
    border-top-left-radius: 20px;
}
</style>