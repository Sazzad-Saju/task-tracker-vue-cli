<template>
    <button @click="addTaskFun()" :style="{background: color}" class="btn">{{text}}</button>
</template>

<script>
    export default{
        name: 'Button',
        props:{
            text: String,
            color: String, 
        },
        methods:{
            addTaskFun(){
                // console.log('Clicked add task');
                this.$emit('btn-click')
            },
        },
    }
</script>