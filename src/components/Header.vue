<template>
  <div class="sticky top-0 sm:w-1/5 w-full mx-auto bg-blue-900 flex justify-between items-center px-3 py-5 mb-3">
    <h1 class="text-blue-100 text-xl font-semibold">{{ title }}</h1>
    <Button 
    :text="showAddTask ? 'Close' : 'Add Task'" 
    @toggle-add-task="$emit('toggle-add-task')" 
    />
  </div>
</template>

<script>
import Button from './Button'

export default ({
  name: 'Header-Component',
  components: {
    Button,
  },
  props: {
    title: String,
    showAddTask: Boolean,
  }
})
</script>
