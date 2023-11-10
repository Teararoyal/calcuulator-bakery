<!-- src/components/SampleComponent.vue -->

<template>
    <div>
      <h2>{{ title }}</h2>
      <p>{{ content }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TestComponent',
    data() {
      return {
        title: 'Sample Component',
        content: 'This is a sample Vue.js component.',
      };
    },
  };
  </script>
  
  <style scoped>
  /* Add component-specific styles here if needed */
  </style>
  