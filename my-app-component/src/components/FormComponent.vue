<template>
  <form action="">
    <div class="form-control">
      <label for="emp-name">ชื่อพนักงาน</label>
      <input type="text" v-model.trim="employee.name" />
      <!-- v-model เพื่อผูกข้อมูลกับ input ที่เราสนใจ (employee.name) เมื่อ input เปลี่ยน จะส่งผลให้ data เปลี่ยนไปด้วยและในขณะเดียวกันถ้า data เปลี่ยนก็จะทำให้ input เปลี่ยน  -->
      <!-- .trim (ทำงานใน v-mode) เป็นการบอกว่าส่วนที่เราสนใจคือ employee.name ให้ทำการตัดช่องว่างทางด้านซ้ายและด้านขวาออกด้วย ตอนใส่ข้อความเข้ามาใน input -->
    </div>
    <div class="form-control">
      <label for="emp-salary">เงินเดือน</label>
      <input type="number" v-model="employee.salary" />
    </div>
    <div class="form-control">
      <label for="department">ตำแหน่งงาน</label>
      <select v-model="employee.department">
        <!-- อย่าลืมเอาข้อมูล employee.department มาผูกกับ v-model เพื่อให้มีการเก็บค่า และเปลี่ยนตามข้อมูลตัวที่เราเลือก-->
        <option value="ฝ่ายการตลาด">ฝ่ายการตลาด</option>
        <option value="ฝ่ายการเงิน">ฝ่ายการเงิน</option>
        <option value="ฝ่ายขาย">ฝ่ายขาย</option>
      </select>
    </div>
    <div class="form-control">
      <h2>เพศ</h2>
      <div>
        <input type="radio" value="ชาย" v-model="employee.gender"/>
        <label for="gender-name">ชาย</label>
        <input type="radio" value="หญิง" v-model="employee.gender"/>
        <label for="gender-name">หญิง</label>
      </div>
    </div>
    <div>
      <button>บันทึกข้อมูล</button>
    </div>
    <!-- ใช้เพื่อดีบัคดูข้อมูลอินพุทต่าง ๆ ที่เราใส่เข้าไปว่ามันเปลี่ยนตามเรียลไทม์ไหม -->
    {{ JSON.stringify(employee) }}
  </form>
</template>

<script>
export default {
  name: "FormComponent",
  data() {
    return {
      employee: {
        name: "",
        salary: 0,
        department: "ฝ่ายการตลาด",
        gender: "",
      },
    };
  },
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.25);
  padding: 2rem;
  background: #fff;
}
.form-control {
  margin: 0.5rem 0;
}
label {
  font-weight: bold;
}
input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}
button {
  font: inherit;
  background: orange;
  color: #fff;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 15px;
}
input[type="radio"] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}
input[type="radio"] + label {
  font-weight: normal;
}
h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}
</style>
