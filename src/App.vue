<template>
  <body>
    <transition name="fade">
      <Modal
        @closeModal="모달창 = false"
        :원룸들="원룸들"
        :누른거="누른거"
        :모달창="모달창"
      />
    </transition>
    <div class="menu">
      <a v-for="a in 메뉴들" :key="a">{{ a }}</a>
    </div>

    <discount v-if="showDiscount == true"></discount>

    <button @click="priceSort()">가격순정렬</button>
    <button @click="sortBack()">되돌리기</button>

    <card
      @openModal="
        모달창 = true;
        누른거 = $event;
      "
      :원룸="원룸들[i]"
      v-for="(작명, i) in 원룸들"
      :key="작명"
    />
    <!-- <card :원룸="원룸들[1]"/>
    <card :원룸="원룸들[2]"/>
    <card :원룸="원룸들[3]"/>
    <card :원룸="원룸들[4]"/>
    <card :원룸="원룸들[5]"/> -->

    <!-- <div v-for="(작명, i) in 원룸들" :key="i">
      <img :src="원룸들[i].image" class="room-img" />
      <h4
        @click="
          모달창 = true;
          누른거 = i;
        "
      >
        {{ 원룸들[i].title }}
      </h4>
      <p>{{ 원룸들[i].price }} 원</p>
    </div> -->
  </body>
</template>

<script>
import data from './oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      원룸들오리지널: [...data],
      오브젝트: { name: 'kim', age: 20 },
      누른거: 0,
      원룸들: [...data],
      모달창: false,
      신고수: [0, 0, 0],
      메뉴들: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸']
    };
  },
  methods: {
    increase() {
      this.신고수 += 1;
    },
    sortBack() {
      this.원룸들 = [...this.원룸들오리지널];
    },
    priceSort() {
      this.원룸들.sort(function(a, b) {
        return a.price - b.price;
      });
    }
  },

  mounted() {
    setTimeout(() => {
      this.showDiscount = false;
    }, 2000);
  },

  components: {
    Discount: Discount,
    Modal: Modal,
    Card: Card
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.fade-leave-from {
  opacity: 0;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 1;
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
</style>
