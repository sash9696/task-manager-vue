<template>
    <form @submit="onSubmit">
        <div class="input">
            <label>Task</label>
            <input type="text" v-model="text" placeholder="Add Task" />
         </div>
         <div class="input">
            <label>Day and Time</label>
            <input type="text" v-model="day" name="day" placeholder="Add Task" />
         </div>
         <div class="input">
            <label>Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder" placeholder="Add Task" />
         </div>    
             <input type="submit" value="Save Task"/>
    </form>

</template>
<script>
    export default{
        data(){
            return {
                text: '',
                day: '',
                reminder: false
            }
        },
        methods: {
            onSubmit(e){
                e.preventDefault()
                if(!this.text){
                    alert('Please add a task')
                    return
                }
                const newTask = {
                    // id: Math.floor(Math.random() * 1000),
                    text: this.text,
                    day: this.day,
                    reminder: this.reminder
                }
                this.$emit('add-task',  newTask)
                this.text = ''
                this.day = ''
                this.reminder = ''
            }
        }
    }
</script>

<style>
    .input{
        width: 300px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 10px;
    }
 </style> 