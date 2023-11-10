<template>
    <div>
      <h2>{{ greeting }}</h2>
      <button @click="changeGreeting">Change Greeting</button>
    </div>
  </template>
  
  <script>
  export default {
    name: "TestComponent2",
    data() {
      return {
        greeting: 'Hello, Vue!',
      };
    },
    methods: {
      // เมทอดที่ใช้เปลี่ยนค่า greeting
      changeGreeting() {
        this.greeting = 'Hola, Vue!';
      },
      // เมทอดที่รับค่าและแสดงใน console
      logMessage(message) {
        console.log(message);
      },
    },
  };
  </script>
  
  <style>
  /* สไตล์ตามต้องการ */
  </style>
  