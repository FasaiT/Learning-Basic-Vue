<template>
  <li>
    <img
      src="https://cdn2.iconfinder.com/data/icons/avatars-60/5985/8-Employee-256.png"
    />
    <hr />
    <!-- <slot> คือตัวแทนของเนื้อหาที่เราแทรกเข้าไปในพื้นที่ของ <Card > มาจากไฟล์ ListData.vue จะเป็นตัวที่แตกต่างกัน-->
    <!-- <slot></slot> -->

    <!-- Named slot เป็นกำหนดพื้นที่ทำงานเป็นส่วน ๆ แล้วจะนำไปใช้ทำงานต่อใน PersonData.vue (ตั้งชื่อให้มันก่อนเอาไปใช้)-->
    <slot name="card-header"></slot>
    <slot name="card-button"></slot>
    <slot name="card-content"></slot>
  </li>
</template>

<script>
export default {};
</script>

<style scoped>
li {
  margin: 1rem 0;
  font-size: 1.25rem;
  font-weight: bold;
  background: plum;
  padding: 0.5rem;
  color: #fff;
  border-radius: 25px;
}
img {
  width: 100px;
  height: 100px;
}
</style>
