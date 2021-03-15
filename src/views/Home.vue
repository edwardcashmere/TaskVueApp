<template>
    <div v-show="show">
          <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks='tasks'/>
    <router-view></router-view>
</template>

<script>
import Tasks from '../components/Tasks';
import AddTask from '../components/AddTask';

export default {
    name: "Home",
    props:{
      show: Boolean
  },
    components:{
        AddTask,
        Tasks
    },
   
    data(){
        return{
            tasks: []
        }

        },
          methods:{
   
    async deleteTask (id){
      if(confirm("Are you sure")){
        const res =  await fetch(`api/tasks/${id}`,{
          method: "DELETE",
          
        })
        res.status === 200 ? this.tasks = this.tasks.filter(a => a.id !==id): alert("error deleting task")
 
      }
    },
   async toggleReminder(id){
      const task = await this.fetchTask(id)
      const updTask = { ...task, reminder: !task.reminder}

      const res = await fetch(`api/tasks/${id}`,{
        method: "PUT",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify(updTask)
      });
      const data  = await res.json()

      this.tasks = this.tasks.map((task)=> task.id ===id ? {...task, reminder: data.reminder}:task)
    },
    async addTask(newTask){
      const res = await fetch("api/tasks",{
        method: "POST",
        headers:{"Content-Type": "application/json"},
        body:JSON.stringify(newTask)
      })
      const data = await res.json()
      this.tasks = [...this.tasks, data]
    },
     async getTasks () {
      const res = await fetch("api/tasks")
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`/api/tasks/${id}`);
      const data = res.json();
      return data
    }
  
  },
  
 async created(){
    this.tasks = await this.getTasks()
  },
  
}

    

</script>