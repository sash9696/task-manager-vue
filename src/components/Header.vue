<template>
    <header>
        <h1>{{title}}</h1>
        <Button @toggle-add-task = "$emit('toggle-add-task')"  :text="showAddTask ? 'Close' : 'AddTask' "  :color="showAddTask ? 'red': 'green' "/>
        <!-- <Button text="Delete" color='red'/> -->
    </header>
</template>

<script>
    import Button from './Button'
    export default {
        name: 'Header',
        // props: ['title']
        components: {
            Button
        },
        props : {
            title : String,
            showAddTask: Boolean,
        }

    }
</script>
<style scoped>
    header{
        display: flex;
        align-items: center;
        justify-content: center;
        
       
    }

</style>