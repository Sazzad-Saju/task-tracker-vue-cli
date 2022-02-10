<template>
  <div class="container">
    <!-- <h1>Hello World</h1> -->
    <!-- <Header /> -->
    <Header @popup-add-task="popupAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <!-- <AddTask @add-task="addTask" /> -->
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" /> <!-- v-bind tasks to tasks data -->
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  // fill with data
  data(){
    return{
      tasks: [], //defined as empty array
      showAddTask: false, //show add task based on this
    }
  },
  methods:{
    popupAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks,task]
    },
    deleteTask(id){
      // console.log('task',id)
      if(confirm('Are you sure?')){
        this.tasks = this.tasks.filter((tasks) => tasks.id !== id)  
        }
    },
    toggleReminder(id){
      // console.log(id)
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    },
  },
  created(){
    //Load from LS
    let Total_Tasks;
    if(localStorage.getItem('Total_Tasks') === null){
      Total_Tasks = []
    } else{
      Total_Tasks = JSON.parse(localStorage.getItem('Total_Tasks'));
    }
    Total_Tasks.forEach(item => {
      this.tasks.push(item);
    })
    //**************/
    /*
    this.tasks = [
      {
        id:1,
        text: 'Intern at NetCoden',
        day: 'February 1st at 9:00 AM',
        reminder: true,
      },
      {
        id:2,
        text: 'Project with Vue.js',
        day: 'February 6th at 3:30 PM',
        reminder: true,
      },
      {
        id:3,
        text: 'Food Shopping',
        day: 'February 14th at 6:30 PM',
        reminder: false,
      },
    ] */
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: 'Poppins',sans-serif;
}
.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn{
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration:none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus{
  outline: none;
}
.btn:active{
  transform: scale(0.98);
}
.btn-block{
  display:block;
  width:100%;
}
</style>
