<template>
  <div 
  @click="$emit('toggle-reminder', task.id)"
  class="sm:w-1/5 w-full mx-auto px-3 py-3 border border-blue-600 rounded-lg mb-2 flex items-center justify-between"
  :class="[task.reminder ? 'border-l-8 border-l-green-600' : '']">
    <div>
      <h3 class="font-semibold">{{ task.text }}</h3>
      <p class="text-sm">{{ task.day }}</p>
    </div>
    <div>
      <i
      @click="$emit('delete-task', task.id)" 
      class="fas fa-times cursor-pointer text-red-500"></i>
    </div>
  </div>
</template>

<script>
export default ({
  name: 'Task-Component',
  props: {
    task: Object,
  },
})
</script>
