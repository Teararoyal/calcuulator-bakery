<template>
    <div>
      <h2>{{ greeting }}</h2>
      <form @submit.prevent="convertToGrams">
        <label for="tspInput">Teaspoon:</label>
        <input type="number" id="tspInput" v-model="TSpoonTo_g" />
        <br />
  
        <label for="tbspInput">Tablespoon:</label>
        <input type="number" id="tbspInput" v-model="TableSpoonTo_g" />
        <br />
  
        <label for="cupInput">Cup:</label>
        <input type="number" id="cupInput" v-model="CupTo_g" />
        <br />
  
        <label for="ozInput">Ounce:</label>
        <input type="number" id="ozInput" v-model="OZTo_g" />
        <br />
  
        <button type="submit">Convert to Grams</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: "TestComponent2",
    data() {
      return {
        greeting: 'Hello, Vue!',
        TSpoonTo_g: 5,
        TableSpoonTo_g: 24,
        CupTo_g: 240,
        OZTo_g: 28,
      };
    },
    methods: {
      changeGreeting() {
        this.greeting = 'Hola, Vue!';
      },
      logMessage(message) {
        console.log(message);
      },
      convertToGrams() {
        // ทำการคำนวณและแสดงผลลัพธ์ใน console
        const tspInGrams = this.TSpoonTo_g * 5; // 1 ช้อนชา = 5 กรัม
        const tbspInGrams = this.TableSpoonTo_g * 15; // 1 ช้อนโต๊ะ = 15 กรัม
        const cupInGrams = this.CupTo_g * 240; // 1 ถ้วย = 240 กรัม
        const ozInGrams = this.OZTo_g * 28.35; // 1 ออนซ์ = 28.35 กรัม
  
        console.log(`Teaspoon in grams: ${tspInGrams}`);
        console.log(`Tablespoon in grams: ${tbspInGrams}`);
        console.log(`Cup in grams: ${cupInGrams}`);
        console.log(`Ounce in grams: ${ozInGrams}`);
      },
    },
  };
  </script>
  

<style>
  /* สไตล์ตามต้องการ */
</style>
