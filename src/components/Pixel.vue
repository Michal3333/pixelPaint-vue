<template>
    <div class="pixel" 
        v-bind:style="{'background-color':value.color}"
        draggable="true"
        @click="changeColorClick"
        @dragenter="changeColorDrag"
        @dragstart="changeColorDrag">
    </div>
</template>

<script>
export default {
    name: 'Pixel',
    props: {
        value : Object,
        color : String
    },
    data () {
        return {
            info: this.value
        }
    },
    methods: {
        changeColorDrag : function (e) {
            let img = new Image();
            e.dataTransfer.setDragImage(img, 0, 0);
            this.value.color = this.color;
        },
        changeColorClick: function () {
            this.value.color = this.color;
            this.$emit("colorClick");
        }
    }
}
</script>

<style scoped>
.pixel{
    align-self: stretch;
    justify-self: stretch;
    border: solid 1px rgba(100, 92, 92, 0.267);
}
</style>