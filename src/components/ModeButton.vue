<template>
    <Button v-bind:class="[data.type === 'multi' ? 'fill' : 'draw', data.selected ? 'selected' : '']"
        @click="selectMode"/>
</template>
<script>

export default {
    name: 'ModeButton',
    props: {
        data: Object
    },
    computed: {
        getIcon: function () {
            let url = '../assets/drwaIcon.jpg';
            if(this.data.type === 'multi') url = '../assets/fillIcon.jpg';
            return {
                'background-image': `url("${url}")`
            }
        }
    },
    methods: {
        selectMode : function () {
            this.$emit("modeSelection", this.data.id, this.data.type);
        }
    }
}
</script>
<style scoped>
    Button{
        border-radius: 10%;
        background-color: red;
        background-position: center;
        background-size: cover;
        border: solid gray 3px;
        transition-duration: 0.5s;
    }
    Button:hover{
        border-color:lightgray;
    }
    .fill{
        background-image: url('../assets/fillIcon.jpg')
    }
    .draw{
        background-image: url('../assets/drwaIcon.jpg')
    }
    .selected{
        border-color: orange;
    }
    .selected:hover{
        border-color:yellow;
    }
</style>