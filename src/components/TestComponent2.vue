<template>
    <div class="con">
      <h2 style="font-weight: bold; color: #9c634f;" >คำนวณแปลงหน่วยเบเกอรี่</h2>
  
      <form action="">
        <div class="container text-center mt-2">
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
          <div class="row mt-1" v-for="(form, index) in forms" :key="index">
            <div class="col">
              <input class="form-control" v-model="form.ingredient" type="text" placeholder="กรอกส่วนผสม" aria-label="ingredient input">
            </div>
            <div class="col">
              <input class="form-control" v-model="form.amount" type="number" placeholder="ปริมาณส่วนผสม" aria-label="amount input">
            </div>
            <div class="col">
              <select v-model="form.fromUnit">
                <option value="1">ถ้วยตวง(Cup)</option>
                <option value="2">ช้อนโต๊ะ(Tablespoon)</option>
                <option value="3">ช้อนชา(Teaspoon)</option>
                <option value="4">ออนซ์(oz)</option>
                <option value="5">มิลลิลิตร(ml)</option>
                <option value="6">กรัม(g)</option>
              </select>
            </div>
            <div class="col">
              <select v-model="form.toUnit">
                <option value="1">ถ้วยตวง(Cup)</option>
                <option value="2">ช้อนโต๊ะ(Tablespoon)</option>
                <option value="3">ช้อนชา(Teaspoon)</option>
                <option value="4">ออนซ์(oz)</option>
                <option value="5">มิลลิลิตร(ml)</option>
                <option value="6">กรัม(g)</option>
              </select>
            </div>
            <div class="col">
              <span>{{ calculateResult(form) }}</span>
            </div>
          </div>
  
          <!-- เพิ่มฟอร์มใหม่เมื่อคลิกปุ่ม + -->
          <button class="button mt-2" @click.prevent="addForm" >เพิ่มรายการ</button>
  
          <!-- ลบฟอร์มเมื่อคลิกปุ่ม - -->
          <button class="button-delate mt-2"  @click.prevent="removeForm(index)" v-if="forms.length > 1">ลบรายการ</button>
          <br />
        </div>
      </form>
    </div>

    <!-- สำหรับแสดงสูตร -->
    <div class="con">
      <div class="mb-3">
        <h2 style="font-weight: bold; color: #9c634f;" >คำนวณสูตรเบเกอรี่ต่อชิ้น</h2>
        <button class="button mt-1" @click.prevent="logFormData()">คำนวณปริมาณสูตร</button>
      </div>

      <form action="">

        <div class="row mb-3" style="align-items: center;">
            <!-- ช่องกรอกจำนวนสูตรเดิม -->
            <div class="col">
            <label for="inputPiece" class="col-form-label">จำนวนชิ้นจากสูตรเดิม</label>
            </div>
            <div class="col">
              <input type="number" id="inputPiece" placeholder="กรอกจำนวน" class="form-control" aria-describedby="passwordHelpInline" required>
            </div>
            <div class="col ">
              <span>ชิ้น</span>
            </div>

            <!-- ช่องกรอกจำนวนสูตรใหม่ -->
            <div class="col">
              <label for="inputPiece1" class="col-form-label">จำนวนชิ้นที่ต้องการ</label>
            </div>
            <div class="col">
              <input type="number" id="inputPiece1" placeholder="กรอกจำนวน" class="form-control" aria-describedby="passwordHelpInline" required>
            </div>
            <div class="col ">
              <span>ชิ้น</span>
            </div>

        </div>

        <div class="container text-center">


          <!-- ตารางสูตรเดิม -->
          <div id="formDataDisplay"></div>
        </div>
      </form>

      

      <form action="">
        <div class="container text-center">
          <!-- ตารางสูตรใหม่ -->
          <div class="row ">
            
            <div id="formDataDisplay1"></div>
          </div>
        </div>
      </form>

</div>



  </template>
  
  <script>
  export default {
    name: "TestComponent2",
    data() {
      return {
        forms: [
          { ingredient: '', amount: 0, fromUnit: '1', toUnit: '1' } // ฟอร์มแรก
        ],
      };
    },
    mounted() {
  this.logFormData();
},
    methods: {
      addForm() {
        // เพิ่มฟอร์มใหม่
        this.forms.push({ ingredient: '', amount: 0, fromUnit: '1', toUnit: '1' });
      },
      removeForm(index) {
        // ลบฟอร์ม
        this.forms.splice(index, 1);
      },
     
      logFormData() {
        const tableBody = this.forms.map((form, index) => `
          <tr>
            <th scope="row">${index + 1}</th>
            <td>${form.ingredient}</td>
            
            <td>${this.calculateResult(form)}</td>
          </tr>
        `).join('');

        const formDataDisplay = document.getElementById("formDataDisplay");
formDataDisplay.innerHTML = `
    <div class="mb-3">
        <h3 style="font-weight: bold; color: #c37960;">แสดงตารางสูตรเดิม</h3>
    </div>
    <table class="table" id="formDataTable" style="width: 100%; min-width: 900px;">
        <thead>
            <tr>
                <th scope="col">ลำดับ</th>
                <th scope="col">ส่วนผสม</th>
                <th scope="col">จำนวน</th>
            </tr>
        </thead>
        <tbody>
            ${tableBody}
        </tbody>
    </table>
`;
this.logFormData1();

        },
        
        logFormData1() {
          const inputPiece = parseFloat(document.getElementById("inputPiece").value);
          const inputPiece1 = parseFloat(document.getElementById("inputPiece1").value);
        const tableBody = this.forms.map((form, index) => `
          <tr>
            <th scope="row">${index + 1}</th>
            <td>${form.ingredient}</td>
            
            <td>${((this.calculateResult(form) / inputPiece ) * inputPiece1).toFixed(2) }</td>
          </tr>
        `).join('');
        
        const formDataDisplay1 = document.getElementById("formDataDisplay1");
          formDataDisplay1.innerHTML = `
          <div class="mb-3">
              <h3 style="font-weight: bold; color: #c37960;">แสดงตารางสูตรที่ต้องการ</h3>
            </div>
            <table class="table" id="formDataTable1" style="width: 100%; min-width: 900px;">
              <thead>
                <tr>
                  <th scope="col">ลำดับ</th>
                  <th scope="col">ส่วนผสม</th>
                  <th scope="col">จำนวน</th>
                </tr>
              </thead>
              <tbody>
                ${tableBody}
              </tbody>
            </table>
          `;
      },

      calculateResult(form) {
        const conversionFactors = {
          '1': 240, // ถ้วยตวง
          '2': 15, // ช้อนโต๊ะ
          '3': 5, // ช้อนชา
          '4': 28, // ออนซ์
          '5': 1, // มิลลิลิตร
          '6': 1, // กรัม
        };
  
        let unitLabel = ''; // ประกาศตัวแปรนอก if-else เพื่อให้เข้าถึงได้ทั้งที่
  
        if (form.toUnit === '1') {
          unitLabel = 'ถ้วยตวง';
        } else if (form.toUnit === '2') {
          unitLabel = 'ช้อนโต๊ะ';
        } else if (form.toUnit === '3') {
          unitLabel = 'ช้อนชา';
        } else if (form.toUnit === '4') {
          unitLabel = 'ออนซ์';
        } else if (form.toUnit === '5') {
          unitLabel = 'มิลลิลิตร';
        } else if (form.toUnit === '6') {
          unitLabel = 'กรัม';
        }
  
        const resultgram = (form.amount * conversionFactors[form.fromUnit]);
        const result = resultgram / conversionFactors[form.toUnit];
        // ส่งค่าที่ไม่ใช่ 'grams'
        return `${result.toFixed(2)} `;
      },
    },
    
  };
  </script>
  
  <style>
    .con {
  width: 100%;
  height: 100%;
  background-color: white;
  padding: 10px;
  margin: 10px auto; /* ใช้ margin: auto เพื่อให้อยู่ตรงกลาง */
  border: 1px solid black;
  border-radius: 10px;
  box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, 0.2);
  max-width: 1200px;
  display: flex; /* เพิ่ม Flexbox */
  flex-direction: column; /* จัดเรียงแนวตั้ง */
  align-items: center;
  
}

    .button{
        background-color: #f0d7a7;
        font-size: 15px;
        color: #894e3f;
        border: 1cm;
        border-radius: 10px;
        width: 300px;
        height: 30px;
        margin: 10px;
        
    }

    .button:hover{
        background-color: #eee1ba;
        
    }

    .button-delate{
        background-color: #894e3f;
        font-size: 15px;
        color: aliceblue;
        border: 1cm;
        border-radius: 10px;
        width: 300px;
        height: 30px;
        margin: 10px;
    }

    .button-delate:hover{
        background-color: #9c634f;
        color: aliceblue;
    }
</style>
