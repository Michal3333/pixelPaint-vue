<template>
    <div id="selector">
        <ModeButton
            class="button"
            v-for="button in buttons"
            v-bind:key="button.id"
            v-bind:data="button"
            @modeSelection="handleModeSelection"/>
    </div>
</template>

<script>
import ModeButton from './ModeButton';
export default {
    name: 'ModelSelector',
    components: {
        ModeButton
    },
    data() {
        return {
            buttons : [
                {
                    id: 0,
                    type: 'single',
                    selected: true
                },
                {
                    id: 1,
                    type: 'multi',
                    selected: false
                }
            ]
        }
        
    },
    methods: {
        handleModeSelection: function (id, type) {
            this.buttons.forEach(element => element.id === id ? element.selected = true : element.selected = false);
            this.$emit('modeSelection', type);
        }
    }
}
</script>

<style scoped>
#selector{
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    border: solid gray 5px;
    border-bottom: none;
    border-left: none;
    background-color: rgb(232, 232, 227);
    border-top-right-radius: 20px;
}
.button{
    width: 60%;
    height: 40%;
    /* border-radius: 10%;
    background-image: url('../assets/drwaIcon.jpg');
    background-color: white;
    background-position: center;
    background-size: cover;
    border: solid gray 3px; */
}

</style>