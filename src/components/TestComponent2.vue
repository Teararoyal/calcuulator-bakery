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
          <div class="row" v-for="(form, index) in forms" :key="index">
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
          <button @click.prevent="addForm">+</button>
  
          <!-- ลบฟอร์มเมื่อคลิกปุ่ม - -->
          <button @click.prevent="removeForm(index)" v-if="forms.length > 1">-</button>
          <br />
        </div>
        <!-- ปุ่มแสดงค่าในฟอร์ม -->
        <button @click.prevent="logFormData()">Log Form Data</button>
      </form>
    </div>

    <!-- สำหรับแสดงสูตร -->
    <div>
      <div class="mb-3">
        <h2>คำนวณสูตรเบเกอรี่ต่อชิ้น</h2>
      </div>

      <form action="">

        <div class="container text-center">
          <div class="row mb-3" style="align-items: center;">
            <!-- ช่องกรอกจำนวนสูตรเดิม -->
            <div class="col">
            <label for="inputPiece" class="col-form-label">จำนวนชิ้นจากสูตรเดิม</label>
            </div>
            <div class="col">
              <input type="number" id="inputPiece" placeholder="กรอกจำนวน" class="form-control" aria-describedby="passwordHelpInline">
            </div>
            <div class="col ">
              <span>ชิ้น</span>
            </div>

            <!-- ช่องกรอกจำนวนสูตรใหม่ -->
            <div class="col">
              <label for="inputPiece" class="col-form-label">จำนวนชิ้นที่ต้องการ</label>
            </div>
            <div class="col">
              <input type="number" id="inputPiece" placeholder="กรอกจำนวน" class="form-control" aria-describedby="passwordHelpInline">
            </div>
            <div class="col ">
              <span>ชิ้น</span>
            </div>

          </div>


          <!-- ตารางสูตรเดิม -->
          <div class="row mb-3">
            <div class="mb-3">
              <h3>แสดงตารางสูตรเดิม</h3>
            </div>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">ลำดับ</th>
                  <th scope="col">ส่วนผสม</th>
                  <th scope="col">จำนวน</th>
                  <th scope="col">หน่วย</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th scope="row">1</th>
                  <td>Mark</td>
                  <td>Otto</td>
                  <td>@mdo</td>
                </tr>
                <tr>
                  <th scope="row">2</th>
                  <td>Jacob</td>
                  <td>Thornton</td>
                  <td>@fat</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </form>

      <form action="">
        <div class="container text-center">
          <!-- <div class="row mb-3">
            <div class="col-auto">
              <label for="inputPiece" class="col-form-label">จำนวนชิ้นที่ต้องการ</label>
            </div>
            <div class="col-auto">
              <input type="number" id="inputPiece" placeholder="กรอกจำนวน" class="form-control" aria-describedby="passwordHelpInline">
            </div>
            <div class="col-auto ">
              <h5>ชิ้น</h5>
            </div>
          </div> -->

          <!-- ตารางสูตรใหม่ -->
          <div class="row ">
            <div class="mb-3">
              <h3>แสดงตารางสูตรที่ต้องการ</h3>
            </div>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">ลำดับ</th>
                  <th scope="col">ส่วนผสม</th>
                  <th scope="col">จำนวน</th>
                  <th scope="col">หน่วย</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th scope="row">1</th>
                  <td>Mark</td>
                  <td>Otto</td>
                  <td>@mdo</td>
                </tr>
                <tr>
                  <th scope="row">2</th>
                  <td>Jacob</td>
                  <td>Thornton</td>
                  <td>@fat</td>
                </tr>
              </tbody>
            </table>
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
        this.forms.forEach((form, index) => {
          console.log(`Form ${index + 1} Data:`, form);
        });
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
        return `${result.toFixed(2)} ${unitLabel}`;
      },
    },
  };
  </script>
  
  <style>
    /* สไตล์ตามต้องการ */
  </style>
  