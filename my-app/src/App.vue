<template>
  <section>
     <!-- Interpolation ใช้ { { } } -->
    <h1>ชื่อ-นามสกุล : {{ firstName }} {{ lastName }}</h1>
    <h1>อายุ : {{ age }} ปี</h1>
    <!-- ด้านล่างเป็นการทดลองคำนวนตัวเลข -->
    <p>{{ 800+200 }}</p>
    <p>ที่อยู่ : <span v-html="address"></span> </p>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      firstName: "ก้อง",
      lastName: "รักสยาม",
      age: 25,
      address: "<i>กรุงเทพมหานคร</i>",
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
