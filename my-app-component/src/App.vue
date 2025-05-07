<template>
  <div>
    <header>
      <h1>ระบบจัดการข้อมูลพนักงาน</h1>
    </header>
    <FormComponent @save="insertEmployee" />
    <!-- FormComponent รับค่าอีเว้นท์ save มาจาก FormComponent.vue และเรียกใช้ method ที่มีชื่อว่า insertEmployee-->
    <section class="employess-content" v-if="employees.length > 0">
      <h2>ข้อมูลพนักงาน</h2>
      <!-- <h1>App Companent</h1> -->

      <!-- เปรียบเสมือนการสร้างแท็กขึ้นมาใช้งานเอง -->
      <!-- <list-data></list-data>  -->
      <!-- แต่ส่วนมากตอนเรียกใช้ component จะทำแบบระบุชื่อตามด้านล่าง -->
      <!-- <FormComponent /> -->

      <!-- employees ตัวแรกคือชื่อ property ส่วน employees ตัวหลังคือData 
    ความหมายของโค้ดด้านล่างคือให้ตัว prop employees Bind data กับ data employees -->
      <!-- <ListData :employees="employees"/> คอมเม้นท์ทิ้ง เพราะมีการย้ายข้อมูล :employees="employees" ไปใช้ใน ListData.vue แล้ว-->

      <ListData :employees="employees" /> 
    </section>
  </div>
</template>

<script>
import FormComponent from "./components/FormComponent.vue";
// import FormComponent from "./components/FormComponent.vue";
//นำเข้า component ListData ที่เราสร้างขึ้นมา (อยู่ในโฟลเดอร์ components ชื่อไฟล์ ListData.vue)
import ListData from "./components/ListData.vue";

export default {
  name: "App",
  components: {
    ListData, //นำ component ListData มาใช้งาน
    FormComponent,
  },
  data() {
    return {
      employees: [], //เตรียมพื้นที่เพื่อรับข้อมูลที่จะส่งมาจากฟอร์ม
    };
  },
  methods: {
    insertEmployee(data) {
      // data คือข้อมูลที่ส่งมาจาก FormComponent
      // console.log("รับข้อมูลพนักงาน = ", data);

      this.employees.push(data);
      // push ใส่ข้อมูลลงไป
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
}
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem;
  border-radius: 1rem;
  padding: 2rem;
  background-color: purple;
  color: #fff;
  text-align: center;
}
.employess-content {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
}
.employess-content h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: purple;
  margin: 0 0 1rem 0;
}
</style>
