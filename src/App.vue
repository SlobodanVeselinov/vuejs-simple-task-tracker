<template>
  <div class="h-screen">
    <Header 
    title="Task Tracker" 
    @toggle-add-task="toggleAddTask"
    :showAddTask="showAddTask"
    />
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks 
      :tasks="tasks" 
      @delete-task="deleteTask" 
      @toggle-reminder="toggleReminder"
    />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
    Footer
  },
  data(){
    return { 
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }, 
    async deleteTask(id){
      const response = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: 'DELETE'
      })
      
      if(response.status ===200){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    async toggleReminder(id){
      const taskToToggle = await this.fetchTask(id)
      const updateTask = {...taskToToggle, reminder:!taskToToggle.reminder}
      const response = await fetch(`http://localhost:3000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body:JSON.stringify(updateTask)
      })

      const data = await response.json()

      this.tasks = this.tasks.map(
        (task) => task.id === id ? {...task, reminder: data.reminder} : task
      )
    },
    async addTask(task){
      const response = await fetch('http://localhost:3000/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json', 
        },
        body: JSON.stringify(task)
      })
      const data = await response.json()
      this.tasks = [...this.tasks, data]
      this.showAddTask = false
    },
    async fetchTasks(){
      const response = await fetch('http://localhost:3000/tasks')
      const data = await response.json()
      return data
    },
    async fetchTask(id){
      const response = await fetch(`http://localhost:3000/tasks/${id}`)
      const data = await response.json()
      return data
    }
  },
  async created(){
    this.tasks = await this.fetchTasks()
  }
}
</script>

