<template>
    <header>
        <!-- <h1>Task Tracker</h1> -->
        <h1>{{ title }}</h1>
        <!-- <Button @popup-add-task="$emit('popup-add-task')" text="Add Task" color="green" /> 
        above passing static value see bellow
        --> 
        <Button @btn-click="$emit('popup-add-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green' " />
        <!-- <Button text="Update Task" color="blue" />
        <Button text="Delete Task" color="red" /> -->
    </header>
</template>

<script>
    import Button from './Button'
    export default{
        name: 'Header',
        // props: ['title'], //as array or object
        props: {
            title: String, 
            showAddTask: Boolean
        },
        // props:{
        //     title:{
        //         type: String,
        //         default: 'Hello World',
        //     }
        // }
        components:{
            Button
        }
    }
</script>

// scoped: anything here for only for this component
<style scoped> 
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>