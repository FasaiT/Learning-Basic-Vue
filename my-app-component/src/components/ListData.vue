<template>
  <!-- <h1>{{ message }}</h1> -->
  <!-- name คือ prop -->
  <!-- <PersonData name="ก้อง" salary="30000" />
    <PersonData name="โจโจ้" salary="20000" />
    <PersonData name="ตั๊กแตน" salary="15000" />
    <PersonData name="แก้ม" salary="18000" /> -->
  <!-- แล้วส่ง prop ชื่อ name ไปที่ตัวแม่คือ PersonData โดยวิธีการข้างบนคือการกำหนดค่าลงไปเลย-->

  <ul>
    <!-- เราสามารถกำหนดเนื้อหา Card component ให้มีความแตกต่างกันได้ โดยที่เรามีต้นแบบ ใส่ดีไซน์อะไรต่าง ๆ ให้ในไฟล์ Card.vue  -->
    <!-- <Card> พนักงานคนที่ 1 </Card>
    <Card> พนักงานคนที่ 2 </Card>
    <Card> พนักงานคนที่ 3 </Card> -->
    <!-- ต่อมาเราทำการคอมเม้นท์ <Card> พนักงานคนที่ ... </Card> ทิ้ง เพราะที่ไฟล์ PersonData มีการนำ <Card> ไปใช้ แล้วให้ข้อมูลที่อยู่ในแท็ก <Card> นั้นแสดงผลแทน-->

    <!-- วิธีข้างล่างนี้เป็นการแสดงข้อมูลทั้งหมด **ห้ามลืมระบุ :key="index" ตอนเราใช้ v-forลูปข้อมูล
        -item คือสมาชิกแต่ละตัวที่อยู่ใน employees .name คือเราเอาค่าชื่อออกมา-->
    <!-- <PersonData
      v-for="(item, index) in employees"
      :key="index" 
      :name="item.name"
      :salary="item.salary"
    /> -->
    <!-- PersonData มี prop ที่ทำงาน 2 ค่าคือ 1.name 2.salary ซึ่งดึงมาจากสมาชิกใน employees 
        และเจ้าตัว employees นี้ก็ถูกส่งมาจากไฟล์ App。vue อีกที -->

    <!-- ต่อมาด้านล่าง เราเปลี่ยนเป็นมากำหนด key="item.id" แทนได้เพราะเป็นค่าที่ไม่ซ้ำ (มีการเพิ่มมาใหม่) 
ดานล่างทั้งหมดคือข้อมูล prop ที่ถูกเพิ่มเข้ามาโดยอ้างอิงจาก property / attribute ที่อยู่ใน object แต่ละตัวที่อยู่ในแอร์เรย์ employees อีกที-->
    <!-- <PersonData
      v-for="item in employees"
      :key="item.id"
      :name="item.name"
      :salary="item.salary"
      :department="item.department"
    /> -->
    <!-- @show="toggleVisible" คือรับอีเว้นท์ show มาจากลูก และเรียกใช้ methods toggleVisible ด้านล่าง-->
    <!-- ต่อมามีการลบ @show="toggleVisible" และ @delete="removeEmployee" :isVisible="item.isVisible" :id="item.id" ทิ้ง เพราะไม่ได้เอาไปใช้ 
    ทำการปรับโครงสร้างโค้ดเพื่อเรียนการบันทึกฟอร์ม-->

    <PersonData
      v-for="(item, index) in employees"
      :key="index"
      :name="item.name"
      :salary="item.salary"
      :department="item.department"
      :gender="item.gender"
      :skill="item.skill"
    />
    <!-- เราทำการวนลูปสร้างข้อมูลที่เอามาจาก props: ["employees"] มาสร้างเป็นข้อมูลของแต่ละคนโดยใช้การวนลูป 
    ต่อมาเราสร้าง prop gender และ skill ขึ้นมา ก็จะถูกส่งต่อไปที่ PersonData.vue เพื่อเอาไปแสดงผล-->
  </ul>
</template>

<script>
// import Person component มาใช้งาน
import PersonData from "./PersonData.vue";
//สร้าง Component และ export ไปใช้งานที่ root component
export default {
  name: "ListData",
  components: {
    PersonData,
  },
  props: ["employees"], //รับ props employees ที่ส่งมาจาก App.vue ในส่วนของ <ListData :employees="employees"
  // แล้วเอาไปวนลูปใน PersonData ด้านบน/>

  // data() {
  //   return {
  //     message: "แสดงรายชื่อพนักงานทุกคน",
  //   };
  // },

  // props: ["employees"], //รับ prop employees มาใช้งาน มีได้หลายค่า ต่อมาบรรทัดนี้คอมเม้นท์ทิ้ง เพราะมีการเอาข้อมูลพนักงานใน data ด้านล่างมาใส่แทน

  // data() {
  //   // return {
  //   //   // ส่งข้อมูลทั้ง 6 ค่านี้ไปทำงานที่ ListData ข้างบน โดยผ่าน prop employees
  //   //   employees: [
  //   //     {
  //   //       id: 1,
  //   //       name: "ก้อง รักสยาม",
  //   //       salary: 40000,
  //   //       department: "โปรแกรมเมอร์",
  //   //       isVisible: false,
  //   //     },
  //   //     {
  //   //       id: 2,
  //   //       name: "แก้ม เรียนดี",
  //   //       salary: 30000,
  //   //       department: "การตลาด",
  //   //       isVisible: false,
  //   //     },
  //   //     {
  //   //       id: 3,
  //   //       name: "โจโจ้ ขยันทำงาน",
  //   //       department: "โปรแกรมเมอร์",
  //   //       isVisible: false,
  //   //     },
  //   //     {
  //   //       id: 4,
  //   //       name: "ชาลี ยิ้มเก่ง",
  //   //       salary: 900,
  //   //       department: "กราฟฟิก",
  //   //       isVisible: false,
  //   //     },
  //   //     {
  //   //       id: 5,
  //   //       name: "ตั๊กแตน เรียนดี",
  //   //       salary: 900,
  //   //       department: "ฝ่ายขาย",
  //   //       isVisible: false,
  //   //     },
  //   //   ],
  //   // };
  // },
  // methods: {
  //   toggleVisible(id) {
  //     // console.log("Child ID = ", id);
  //     //map
  //     this.employees = this.employees.map((item) => {
  //       //ตรวจสอบว่า ถ้าไอดีที่ส่งมา มีค่าตรงกันกับไอดีที่รับมา
  //       if (item.id === id) {
  //         //ให้มีการเปลี่ยนแปลง isVisible ตามค่าไอดีตัวที่ส่งมา
  //         return { ...item, isVisible: !item.isVisible };
  //       }
  //       return item;
  //     });
  //   },
  //   removeEmployee(id) {
  //     this.employees = this.employees.filter((item) => {
  //       //ไอเทมที่มีไอดีไม่ตรงกันกับไอดีที่ส่งมา จะให้คงสภาพเอาไว้
  //       return item.id !== id;
  //     });
  //   },
  // },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
}
</style>
