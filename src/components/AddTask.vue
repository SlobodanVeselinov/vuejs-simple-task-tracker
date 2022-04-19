<template>
  <div class="px-4 mb-5">
    <form @submit.prevent="onSubmit">
      <input class="mb-2 border border-blue-500 rounded px-2 py-3 w-full" type="text" v-model="text" name="text" placeholder="Add task" />      
      <input class="mb-2 border border-blue-500 rounded px-2 py-3 w-full" type="text" v-model="day" name="day" placeholder="Set Day and time" />      
      <div class="flex items-center">
        <input type="checkbox" v-model="reminder" name="reminder" class="w-5 h-5 mr-2">
        <span>Set Reminder</span>
      </div>
      <button class="w-full bg-blue-900 text-blue-100 py-3 mt-5 rounded">Create Task</button>

    </form>
  </div>
</template>

<script>
export default{
  name: 'AddTask-Component', 
  data(){
    return{
      text: '',
      day: '',
      reminder: false
    }
  },
  methods: {
    onSubmit(){
      if(!this.text || !this.day){
        alert('Please fill all fields!')
      }

      const newTask = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }

      this.text = ''
      this.day = ''
      this.reminder = false

      this.$emit('add-task', newTask)
    }
  },
}
</script>
