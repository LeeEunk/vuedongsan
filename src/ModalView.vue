<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <img :src="원룸들[누른거].image" class="room-img" />
      <!-- <p><input @input="month = $event.target.value" /></p> -->
      <p><input v-model.number="month" /></p>
      <p>{{ month }}개월 선택함 : {{ 원룸들[누른거].price * month }}원</p>
      <p>{{ 원룸들[누른거].content }}</p>
      <button @click="$emit('closeModal')">X</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalView",
  data() {
    return {
      month: 1,
    };
  },
  props: {
    원룸들: Array,
    누른거: Number,
    모달창열렸니: Boolean,
  },
  watch: {
    month(a) {
      // 사용자가 13보다 크면 경고문 띄우기
      // 사용자가 month를 글자로 입력 시, 경고문 띄우기
      if (isNaN(a) == true) {
        alert("문자 입력하지 마");
      }
    },
  },
  beforeUpdate() {
    // input에 2 입력 시 경고창
    if (this.month == 2) {
      alert("2개월은 안팜");
      // 3으로 자동 변경됨
      this.month = 3;
    }
  },
};
</script>

<style></style>
