<template>
    <div class="color" v-bind:style="{'background':info.color}"
        v-bind:class="{selected : info.selected}"
        @click="selectColor"/>
</template>

<script>
export default {
    name : 'Color',
    props : ['info'],
    methods: {
        selectColor: function () {
            this.$emit("colorSelect", this.info.color, this.info.id);
        }
    },
    computed: {
        colorWithGradient: function () {
            return `linear-gradient(45deg,${this.info.color} 9%, rgb(200, 200, 200) 0%)`
        }

    }
}
</script>

<style scoped>
div.color{
    align-self: stretch;
    justify-self: stretch;
    border: solid;
    transition-duration: 0.5s;
    border-radius: 10%;
    height: 2vw;
    width: 2vw;
    min-width: 35px;
    min-height: 35px;
    border: 3px solid gray;
}
div.color:hover{
    border-color: lightgray ;
}
div.selected{
    border-color: orange;
    border-width: 4px;
}
div.selected:hover{
    border-color: yellow;
}
</style>