<template>
  <button @click="$emit('toggle-add-task')" class="border border-blue-100 px-3 py-2 rounded text-blue-100 text-sm">{{ text }}</button>
</template>


<script>
  export default ({
    name: 'Button-Component',
    props: {
      text: String,
    },
    methods: {
      
    }
  })
</script>
