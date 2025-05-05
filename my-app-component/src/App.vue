<template>
  <div>
    <header>
  <h1>ระบบจัดการข้อมูลพนักงาน</h1>
</header>
  <section class="employess-content">
    <h2>ข้อมูลพนักงาน</h2>
    <!-- <h1>App Companent</h1> -->

    <!-- เปรียบเสมือนการสร้างแท็กขึ้นมาใช้งานเอง -->
    <!-- <list-data></list-data>  -->
    <!-- แต่ส่วนมากตอนเรียกใช้ component จะทำแบบระบุชื่อตามด้านล่าง -->
    <!-- <FormComponent /> -->

    <!-- employees ตัวแรกคือชื่อ property ส่วน employees ตัวหลังคือData 
    ความหมายของโค้ดด้านล่างคือให้ตัว prop employees Bind data กับ data employees -->
    <!-- <ListData :employees="employees"/> คอมเม้นท์ทิ้ง เพราะมีการย้ายข้อมูล :employees="employees" ไปใช้ใน ListData.vue แล้ว-->
    
    <ListData /> 
  </section>
  </div>
</template>

<script>
// import FormComponent from "./components/FormComponent.vue";
//นำเข้า component ListData ที่เราสร้างขึ้นมา (อยู่ในโฟลเดอร์ components ชื่อไฟล์ ListData.vue)
import ListData from "./components/ListData.vue";
export default {
  name: "App",
  components: {
    ListData, //นำ component ListData มาใช้งาน
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
