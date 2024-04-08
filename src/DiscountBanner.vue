<template>
  <div class="discount">
    <h4>지금 결제하면 {{ 할인률 }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountBanner",
  data() {
    return {};
  },
  props: {
    할인률: Number,
  },
};
</script>

<style>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
