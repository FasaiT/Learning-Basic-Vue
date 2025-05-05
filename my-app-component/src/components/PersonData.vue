<template>
  <li>
    <!-- prop ชื่อ name มีค่าแต่ละตัวคืออะไรบ้าง ก็เอามาใส่ที่ส่วนด้านล่างนี้ เพื่อแสดงผลที่หน้าจอ -->
    <h1>{{ name }}</h1>
    <button @click="showDescription(id)">ดูรายละเอียด</button> &nbsp;
    <button>ลบข้อมูล</button>
    <div v-show="isVisible">
      <p>เงินเดือน : {{ salary }} ตำแหน่งงาน : {{ department }}</p>
    </div>
  </li>
</template>

<script>
export default {
  name: "PersonData",
  // data() {
  //   return {
  //     message: "ข้อมูลพนักงานแต่ละคน",
  //   };
  // },
  // props: ["name", "salary"], //รับ prop ชื่อ name มาจากลูกคือ ListData และที่เราระบุเป็นแอเรย์เพราะมันสามารถรับมาได้หลายค่า

  //ด้านล่างเป็นการ validate prop เราจะเปลี่ยนเครื่องหมายเป็นการใช้ { } เพื่อให้สามารถใส่แอคชั่นได้
  // เราสามารถตรวจสอบข้อผิดพลาดได้ในหน้า f12 console in browser
  props: {
    id: {
      type: Number,
    },
    name: {
      type: String,
      required: true, //บังคับกรอกค่า
    },
    salary: {
      type: Number,
      default: 15000, //ถ้าไม่มีการกำหนดค่าให้ props salary ก็จะมีค่าตั้งต้นคือ 15000
    },
    department: {
      type: String,
      required: true,
    },
    isVisible: {
      type: Boolean,
    },
  },
  methods: {
    showDescription(id){
      // $emit คือการส่งสัญญาณจากตัวลูกไปหาแม่ในรูปแบบของอีเว้นท์ ในที่นี้กำหนดค่าเป็น "show" และส่งข้อมูลก็คือ id ไปด้วย 
      // ซึ่งข้อมูลพวกนี้จะส่งไปที่ไฟล์ LisData.vue
      this.$emit("show",id);
    }
  },
};
</script>

// เราใส่คำ scoped เข้าไปเพื่อให้ h1 ของเฉพาะ Component นี้มีการกำหนดค่าสี //
เพราะถ้าไม่ใส่ มันจะกลายเป็นแบบ global คือไม่ว่าจะจุดไหนก็ตามที่มีการเรียกใช้ h1
ในโปรเจ็กท์ มันจะกำหนดค่าสีให้ h1 ไปเลยทุกจุด
<style scoped>
/* h1 {
  color: red;
} */
 li {
  margin: 1rem 0;
  font-size: 1.25rem;
  font-weight: bold;
  background: #8ddba4;
  padding: 0.5rem;
  color: #1f1f1f;
  border-radius: 25px;
 }
 button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background: #ff0077;
  color: white;
  padding: 0.05rem 1rem ;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
 }
</style>
