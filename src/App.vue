<template>
  <div class="app-container">
    <Header @toggle-add-task ="toggleAddTask" title="Task Tracker" :showAddTask = "showAddTask" />
    <div  v-if="showAddTask" > 
        <AddTask @add-task = "addTask"  />

    </div>


    <Tasks @toggle-reminder ="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from './components/AddTask.vue'

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    };
  },
  methods: {
    toggleAddTask(){
      
      this.showAddTask =  !this.showAddTask
    },
    async addTask(task){
      console.log(task)
      const res = await fetch('http://localhost:3000/tasks',{
        method: 'POST',
        headers: {
          'Content-type' : 'application/json'
        },
        body: JSON.stringify(task)

      })
      const data = await res.json()
      this.tasks.push(data)
    },
    async deleteTask(id) {
      if (confirm("Are you sure you want to delete")) {
        const res = await fetch(`http://localhost:3000/tasks/${id}`,{
          method: 'DELETE',

        })
        res.status = 200 || 204 ? this.tasks = this.tasks.filter((item) => item.id !== id) : alert('Error');

      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) => (
        task.id == id ?
        {
        ...task, reminder: !task.reminder
      } : task ))
    },
      async fetchTasks(){
        const res = await fetch('http://localhost:3000/tasks')
        const data = await res.json()

      return data
  },
  },
  
  async created() {
    this.tasks = await this.fetchTasks()
  },
};
</script>

<style>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  border: 1px solid grey;
  width: 600px;
  max-height: 200vh;
}
#app {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
}
</style>
