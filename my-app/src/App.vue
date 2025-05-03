<template>
  <section>
    <!-- การใช้ v-bind เราเขียนอ้างอิงตัว Property ตัวที่เราต้องการอ้างอิงตามปกติ โดยไม่ต้องเขียนแบบ Interpolation -->
    <!-- <img v-bind:src="picture" v-bind:width="size" v-bind:height="size" /> -->
    <!-- เขียนแบบข้างบน ถ้ายาวไป เราลดรูปได้ตามด้านล่าง -->
    <img :src="picture" :width="size" :height="size" ref="imageURLEl" />

    <form @submit.prevent="submitForm">
      <!-- .prevent ด้านบนใส่ .prevent เพื่อเป็นการบังคับให้อินพุทไม่หายตอนกดรีเฟรช ถือเป็นอีกวิธีการที่เรากำหนดค่าไม่ให้อินพุทหายหลังรีเฟรชหน้าได้ -->

      <label for="">กรอกชื่อเล่น : </label>
      <!-- ด้านล่างเป็นการตรวจจับอีเว้นท์ที่เกิดจากช่องอินพุท -->
      <!-- <input type="text" v-on:input="setNickName" ref="nickNameEl" /> -->
      <!-- แบบลดรูป>> กรอกชื่อเล่น : <input type="text" @input="setNickName" /> -->

      <!-- ข้างล่างคือเมื่อเราต้องการให้ เมื่อผู้ใช้ป้อนชื่อเข้ามา แล้วกดบันทึก ค่อยแสดงชื่อขึ้นมา -->
      <input type="text" ref="nickNameEl" />

      <button type="submit">บันทึก</button>
    </form>

    <!-- แสดงผล Interpolation ใช้ { { } } -->
    <!-- ด้านล่างคือการอ้างอิงจาก data เราจะอ้างอิงค่า Property ที่เราสนใจได้โดยตรงแบบโค้ดด้านล่าง-->
    <!-- <h1>ชื่อ-นามสกุล : {{ firstName }} {{ lastName }}</h1> -->

    <!-- ด้านล่างนี้คือการเอา methods getFullname()ที่เราสร้างมาใช้ -->
    <!-- <h1>ชื่อ-นามสกุล : {{ getFullname() }}</h1> -->

    <!-- เมื่อเราต้องการใช้ getFullname ในบล็อก computed (ย้ายจาก method มา) -->
    <h1>ชื่อ-นามสกุล : {{ getFullname }}</h1>

    <!-- <h2>ชื่อเล่น : {{ nickName }}</h2> -->
    <h1>อายุ : {{ age }} ปี</h1>

    <h1>เงินเดือน: {{ salary }} บาท</h1>
    <!-- การคำนวน เขียนแบบนี้ไม่เหมาะ ให้ไปเขียนในบล็อก computed แทนจะดีกว่า -->
    <!-- <h1>รายได้ต่อปี : {{ salary * 12 }} บาท</h1> -->
    <h1>รายได้ต่อปี : {{ getIncome }} บาท</h1>

    <!-- แต่ในพื้นที่ของเทมเพลท มีไว้เพื่อแสดงผล จึงไม่นิยมเขียนลอจิกหรือการคำนวนต่าง ๆ ลงไป แบบด้านล่าง
    <h1>
      ตำแหน่งงาน : {{ salary >= 35000 ? "Project Manager" : "Programmer" }}
    </h1> 
    จึงทำแบบด้านล่างแทน-->

    <h1>ตำแหน่งงาน : {{ getDepartment }}</h1>

    <button @click="addSalary(5000)">เพิ่มเงินเดือน</button>

    <!-- Method ทำงานแยกกัน แม้ใช้ฟังก์ชันเดียวกัน ได้ตัวเลขต่างกัน มีการรันใหม่ของใครของมัน-->
    <h2>Method1 : {{ getRandomByMethod() }}</h2>
    <h2>Method2 : {{ getRandomByMethod() }}</h2>
    <h2>Method3 : {{ getRandomByMethod() }}</h2>
    <hr />
    <!-- Computed ทำงานเหมือนกัน ได้ตัวเลขเหมือนกัน ตราบเท่าที่ตัวเลขที่สุ่มได้อันแรก ไม่มีการเปลี่ยนแปลงข้อมูล เป็นการเอาข้อมูลชุดเดิมมาแสดงผล -->
    <h2>Computed1 : {{ getRandomByComputed }}</h2>
    <h2>Computed2 : {{ getRandomByComputed }}</h2>
    <h2>Computed3 : {{ getRandomByComputed }}</h2>

    <!-- ด้านล่างเป็นการทดลองคำนวนตัวเลข -->
    <!-- <p>{{ 800 + 200 }}</p> -->

    {{ isVisible }}
    <button @click="toggleVisible">
      {{ isVisible ? "ซ่อน" : "แสดง" }}More information
    </button>
    <article v-show="isVisible">
      <p>ที่อยู่ : <span v-html="address"></span></p>
      <p><a :href="social" target="_blank">My Github</a></p>
      <!-- ถ้า hobby เป็นค่าว่าง ให้แสดงคำ "ไม่มีงานอดิเรก" ถ้าไม่ว่าง ให้ใส่งานอดิเรก -->
      <p v-if="hobby.length === 0">ไม่มีงานอดิเรก</p>
      <div v-else>
        <p>งานอดิเรก:</p>
        <ul>
          <!-- เรากำหนดการเข้าถึงแบบตัว ๆ -->
          <!-- <li>{{ hobby[0] }}</li>
        <li>{{ hobby[1] }}</li>
        <li>{{ hobby[2] }}</li> -->

          <!-- แต่เราสามารถวน for ในการเข้าถึงแอเรย์แต่ละตัวโดยการใช้ v-for 
        มี item เป็นชื่อตัวแปรที่เราตั้งขึ้นมา item เป็นสมาชิกของแต่ละรายการที่เป็นสมาชิกในแอร์เรย์ hobby, 
        {{ item }} พื้นที่ให้ข้อมูลแอเรย์มันแสดงผล, 
        index เป็น index ของแต่ละรายการ),
        :key="index" ถือเป็นค่าคีย์(ไม่ซ้ำ เพื่อนำมาอ้างอิง) -->
          <li v-for="(item, index) in hobby" :key="index">
            {{ index }} - {{ item }}
          </li>
        </ul>
      </div>
      <p>ข้อมูลพื้นฐาน</p>
      <ul>
        <!-- <li>เพศ: {{ general.gender }}</li>
      <li>น้ำหนัก: {{ general.weight }}</li>
      <li>ส่วนสูง: {{ general.height }}</li>
      <li>โรคประจำตัว: {{ general.congenitalDisease }}</li> -->

        <!-- เราสามารถใช้ v-for กับ Object ได้เช่นกัน โดยไม่ต้องกำหนดค่าแบบข้างบน 
      โดย item คือข้อมูล ส่วน key คือชื่อ porperty-->
        <li v-for="(item, key) in general" :key="key">{{ key }} -{{ item }}</li>
      </ul>

      <!-- <button v-on:click//ตามด้วยอีเว้นท์ที่ต้องการให้ทำฟังก์ชัน="showData">คลิกเพื่อดูข้อมูล</button> -->
      <!-- เราสามารถลดรูป v-on ได้เช่นกัน  -->
      <!-- <button @click="showData">คลิกเพื่อดูข้อมูล</button> -->
      <!-- เราจะระบุ()หรือไม่ก็ได้ ถ้าระบุ จะเป็นการส่งพารามิเตอร์เข้าไปทำงานข้างใน แต่ถ้าไม่มีส่งพารามิเตอร์อะไร ่ก็ไม่ต้องใส่ก็ได้-->
      <!-- เติม .ctrl เพื่อกำหนดการทำงานว่าถ้าคลิกตรงเม้าส์ซ้ายปกติ และต้องมีการกดปุ่ม ctrl ถึงจะยอมเพิ่มจำนวน เป็นเรื่องของ Event Modifier -->
      <!-- <button @click.ctrl="increment(10)">เพิ่ม</button> -->
      <!-- เติม .middle เพื่อกำหนดการทำงานว่าถ้าคลิกตรงเม้าส์กลาง(เม้าส์สกอร์) ถึงจะมีการลดจำนวน เป็นเรื่องของ Event Modifier -->
      <!-- <button @click.middle="decrement">ลด</button> -->
    </article>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      firstName: "Fasai",
      lastName: "Tuntisaneepong",
      // nickName: "",
      age: 25,
      address: "<i>กรุงเทพมหานคร</i>",
      picture:
        "https://cdn0.iconfinder.com/data/icons/female-styles/500/woman-pretty-bg-256.png",
      size: 50,
      social: "https://github.com/FasaiT",
      hobby: [
        "Reading books",
        "Listenning to podcasts",
        "Learning new language",
      ],
      // hobby: [] ,
      general: {
        gender: "Female",
        weight: 47.0,
        height: 157,
        congenitalDisease: false,
      },
      isVisible: false,
      salary: 20000,
    };
  },
  //ในกรณีของการเอา methods ไปใช้ เราจะต้องมีการอ้างอิง Property ที่เราสนใจ โดยใช้คีย์เวิร์ด this นำหน้า Property ที่เราสนใจ
  methods: {
    showData() {
      alert(this.firstName);
    },
    // พารามิเตอร์ value เราเอามาจากตรง increment(10) ซึ่งเรากำหนดพารามิเตอร์ไว้คือ 10
    increment(value) {
      this.age += value;
    },
    decrement() {
      this.age--;
    },
    setNickName(event) {
      // console.log(event.target.value);
      this.nickName = event.target.value;
    },
    submitForm() {
      // ถ้าใช้อันนี้ ตรงพารามิเตอร์ของฟังก์ชันนี้ต้องใส่ e ด้วย e.preventDefault();
      // ใส่เพื่อให้ข้อมูลอยู่ในช่องอินพุท ไม่รีเฟรชหน้าแล้วข้อมูลหายหลังกดบันทึก หรือว่าเราจะไปใส่ตรง <form @submit.prevent="submitForm"> ก็ได้
      // alert("บันทึกชื่อเล่นเรียบร้อย");

      // imageURLEl มีการเก็บโครงสร้างข้อมูลรูปภาพเอาไว้ ก็คือพวก propertｙ ต่าง ๆ ในแท็ก เพื่อให้เข้าถึงข้อมูลพวกนั้นได้ จึงใช้ $refs.ชื่อ El ที่เราทำการอ้างอิงไว้
      // เป็นการอ้างอิงแท็กข้อมูลที่เราสนใจ เมื่อทำฟังก์ชัน submitForm()
      // console.log(this.$refs.imageURLEl);
      // console.log(this.$refs.nickNameEl);

      //  ข้างล่างคือเมื่อเราต้องการให้ เมื่อผู้ใช้ป้อนชื่อเข้ามา แล้วกดบันทึก ค่อยแสดงชื่อขึ้นมา ต้องมีการเก็บค่าใน nickName เพื่อให้มันเอาไปแสดงผลได้ โดยใช้ .value
      this.nickName = this.$refs.nickNameEl.value;
    },
    toggleVisible() {
      this.isVisible = !this.isVisible;
    },
    getRandomByMethod() {
      return Math.random();
    },
    addSalary(value) {
      this.salary += value;
    },
  },
  computed: {
    getFullname() {
      //เราสามารถแสดงผลได้ตามด้านล่าง
      // return this.firstName + this.lastName;
      // return `${this.firstName + " " + this.lastName} ที่อยู่: ${this.address}`;
      return `${this.firstName} ${this.lastName}`;
    },
    getRandomByComputed() {
      return Math.random();
    },
    getIncome() {
      return this.salary * 12;
    },
    getDepartment() {
      return this.salary >= 35000 ? "Project Manager" : "Programmer";
    },
  },
  // ตัว watch ใช้ใการติดตามค่า
  watch: {
    salary(value) {
      if (value > 50000) {
        alert("เงินเดือนไม่ควรเกิน 50000 บาท");
        setTimeout(() => {
          this.salary = 50000;
        }, 1000);
      }
    },
  },
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
