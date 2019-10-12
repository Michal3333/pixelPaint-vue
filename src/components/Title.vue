<template>
    <div class="title">
        {{this.title}}
    </div>
</template>
<script>
export default {
    name: 'Title',
    props: {
        title: String
    }
}
</script>
<style scoped>
    .title{
        font-size: 40px;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        margin-bottom: 5px;
        color: rgb(70, 70, 70);
    }
</style>