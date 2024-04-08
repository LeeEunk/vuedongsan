<template>
  <div class="menu">
    <a v-for="header in menus" :key="header">{{ header }}</a>
  </div>

  <!-- 할인 배너 -->
  <DiscountBanner
    v-if="showDiscount == true"
    :할인률="할인률"
    v-bind="오브젝트"
    :이름="오브젝트.name"
    :나이="오브젝트.age"
  />

  <!-- 정렬 -->
  <button @click="priceSort">가격순 정렬</button>
  <button @click="priceReverse">가격역순 정렬</button>
  <button @click="titleSort">상품명 가나다순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <!-- 모달 -->
  <transition name="fade">
    <ModalView
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @closeModal="모달창열렸니 = false"
    />
  </transition>
  <!-- 모달창열렸니가 true일 때만 .end를 부착해보자 -->
  <!-- <div class="start" :class="{ end: 모달창열렸니 }">
    <ModalView
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
      @closeModal="모달창열렸니 = false"
    />
  </div> -->

  <!-- <div v-for="(btn, i) in number" :key="btn">
    <h4>{{ products[i] }}</h4>
    <p>50 만원</p>
    <button @click="number[i]++">허위매물신고</button>
    <span>신고수 : {{ number[i] }}</span>
  </div>

  <div>---------------</div> -->

  <CardView
    @openModal="
      모달창열렸니 = true;
      누른거 = $event;
    "
    v-for="(a, i) in 원룸들"
    :key="a"
    :원룸="원룸들[i]"
  />

  <!-- <CardView :원룸="원룸들[0]" />
  <CardView :원룸="원룸들[1]" />
  <CardView :원룸="원룸들[2]" />
  <CardView :원룸="원룸들[3]" />
  <CardView :원룸="원룸들[4]" />
  <CardView :원룸="원룸들[5]" /> -->

  <!-- <div>
    <img :src="원룸들[1].image" class="room-img" />
    <h4>{{ 원룸들[1].title }}</h4>
    <p>{{ 원룸들[1].price }}원</p>
  </div>
  <div>
    <img :src="원룸들[2].image" class="room-img" />
    <h4>{{ 원룸들[2].title }}</h4>
    <p>{{ 원룸들[2].price }}원</p>
  </div>
  <div>
    <img :src="원룸들[3].image" class="room-img" />
    <h4>{{ 원룸들[3].title }}</h4>
    <p>{{ 원룸들[3].price }}원</p>
  </div>
  <div>
    <img :src="원룸들[4].image" class="room-img" />
    <h4>{{ 원룸들[4].title }}</h4>
    <p>{{ 원룸들[4].price }}원</p>
  </div> -->

  <div>-----------------</div>

  <div>
    <img src="./assets/room0.jpg" class="room-img" />
    <h4 @click="모달창열렸니 = true">{{ products[0] }}</h4>
    <p>50 만원</p>
    <button @click="number[0]++">허위매물신고</button>
    <span>신고수 : {{ number[0] }}</span>
  </div>
  <div>
    <img src="./assets/room1.jpg" class="room-img" />
    <h4>{{ products[1] }}</h4>
    <p>70 만원</p>
    <button @click="number[1]++">허위매물신고</button>
    <span>신고수 : {{ number[1] }}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img" />
    <h4>{{ products[2] }}</h4>
    <p>90 만원</p>
    <button @click="number[2]++">허위매물신고</button>
    <span>신고수 : {{ number[2] }}</span>
  </div>
</template>

<script>
import data from "./assets/oneroom.js";
import Discount from "./DiscountBanner.vue";
import Modal from "./ModalView.vue";
import Card from "./CardView.vue";

export default {
  name: "App",
  data() {
    return {
      할인률: 20,
      showDiscount: true,
      원룸들오리지널: [...data],
      오브젝트: { name: "kim", age: 20 },
      누른거: 0,
      원룸들: data,
      모달창열렸니: false,
      number: [0, 0, 0],
      menus: ["Home", "Products", "About"],
      products: ["역삼동원룸", "천호동원룸", "마포구원룸"],
    };
  },
  methods: {
    increase() {
      this.number += 1;
    },
    priceSort() {
      this.원룸들.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceReverse() {
      this.원룸들.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    titleSort() {
      this.원룸들.sort(function (a, b) {
        if (a.title > b.title) return 1;
        if (a.title < b.title) return -1;
      });
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
  },
  components: {
    DiscountBanner: Discount,
    ModalView: Modal,
    CardView: Card,
  },
  // mount후에 뭔가 실행하고 싶으면 여기에
  mounted() {
    // 2초 뒤에 사라지기
    // setTimeout(() => {
    //   this.showDiscount = false;
    // }, 2000);

    //1초마다 1% 감소하기
    setInterval(() => {
      this.할인률--;
    }, 1000);
  },
};
</script>

<style>
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}

/* .start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
} */
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0, 5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.room-img {
  width: 30%;
  margin-top: 40px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 15px;
}
</style>
