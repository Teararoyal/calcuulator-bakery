<template>
    <div>
      <h2>คำนวณแปลงหน่วยเบเกอรี่</h2>

      <form action="">
        <div class="container text-center">
          <!-- หัวข้อ -->
          <div class="row">
            <div class="col">
              <h5>ส่วนผสม</h5>
            </div>
            <div class="col">
              <h5>ปริมาณ</h5>
            </div>
            <div class="col">
              <h5>หน่วยเดิม</h5>
            </div>
            <div class="col">
              <h5>หน่วยที่ต้องการแปลง</h5>
            </div>
            <div class="col">
              <h5>แสดงผล</h5>
            </div>
          </div>

          <!-- ช่อง -->
          <div class="row">
            <div class="col">
              <input class="form-control" id="" type="text" placeholder="กรอกส่วนผสม" aria-label="default input example">
            </div>
            <div class="col">
              <input class="form-control" id="" type="number" placeholder="ปริมาณส่วนผสม" aria-label="default input example">
            </div>
            <div class="col">
              <select name="หน่วยเดิม" id="">
                <option selected>เลือกหน่วย</option>
                <option value="1">ถ้วยตวง(Cup)</option>
                <option value="2">ช้อนโต๊ะ(Tablespoon)</option>
                <option value="3">ช้อนชา(Teaspoon)</option>
                <option value="4">ออนซ์(oz)</option>
                <option value="5">มิลลิลิตร(ml)</option>
                <option value="6">กรัม(g)</option>
              </select>
            </div>
            <div class="col">
              <select name="หน่วยที่ต้องการแปลง" id="">
                <option selected>เลือกหน่วย</option>
                <option value="1">ถ้วยตวง(Cup)</option>
                <option value="2">ช้อนโต๊ะ(Tablespoon)</option>
                <option value="3">ช้อนชา(Teaspoon)</option>
                <option value="4">ออนซ์(oz)</option>
                <option value="5">มิลลิลิตร(ml)</option>
                <option value="6">กรัม(g)</option>
              </select>
            </div>
            <div class="col">
              <span id=""></span>
            </div>

          </div>


         </div>
       </form>
      <!-- <h2>{{ greeting }}</h2> -->
      <!-- <form @submit.prevent="convertToGrams">
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
      </form> -->
    </div>
  </template>
  
  <script>
  export default {
    name: "TestComponent2",
    data() {
      return {
        // greeting: 'Hello, Vue!',
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
