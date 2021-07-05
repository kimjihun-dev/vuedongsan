<template>
    <nav class="menu">
        <ul class="gnb">
            <li v-for="(item, index) in menus" :key="index">
                <a href="#!">{{ item }}</a>
            </li>
        </ul>
    </nav>
    <!-- 애니메이션 주고 싶을때 트렌지션으로 감싸고 이름은 임의대로 -->
    <transition name="fadeModal"> 
        <Modal :products="products" :userSelect="userSelect" :modalStatus="modalStatus" @closeModal="modalStatus = false;" />
    </transition>

    <Discount v-if="showDiscount == true" />

    <button @click="priceSort()">가격순정렬</button>
    <button @click="sortBack()">되돌리기</button>

    <Card :products="products" @openModal="modalStatus = true; userSelect = $event" />

</template>

<script>

import roomData from './roomData'
import Discount from './components/Discount.vue'
import Modal from './components/Modal.vue'
import Card from './components/Card.vue'

export default {
  name: 'App',
  data() {
      return {
          showDiscount: true,
          oneRooms: [...roomData],
          userSelect: 0,
          modalStatus: false, 
          policeNums: [0, 0, 0],
          products: roomData,
          menus: ['Home', 'Products', 'Price'],
          
      }
  },
  methods: {
      priceSort(){
          this.products.sort(function(a, b){
              return a.price - b.price
          })
      },
      sortBack(){
          this.products = [...this.oneRooms]
      },
  },
  components: {
      Modal, Card, Discount,
  },

  created() {

  },
  mounted() {
    // 마운트 되고 나서 코드 실행
    // setTimeout(() => {
    //     this.showDiscount = false
    // }, 2000)
  },

  // 메인 페이지 로드 후 부터 discount 할인 문구 1초마다 1% 감소하게끔 
  // update 이용하여 모달창에서 input 특정값 입력시 알림 창 띄우기 

}
</script>

<style>
*, *::after, *::before { 
    box-sizing: border-box;
    padding: 0;
    margin: 0; 
}

html {
    font-size: 62.5%;
}

img { max-width: 100%; width: 100%; }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  font-size: 1.6rem;
}

.menu {
    background: darkslateblue;
    height: 50px;
    line-height: 50px;
}

.gnb {
    display: flex;
    justify-content: center;
}

.gnb li {
    list-style: none;
    padding-right: 10px;
    font-size: 1.8rem;
}

.menu a {
    color: #fff;
    text-decoration: none;
}

/* 모달창 시작 */
.fadeModal-enter-from { opacity: 0; }

.fadeModal-enter-active { transition: all 1s; }

/* 모달창 끝 */
.fadeModal-enter-to { opacity: 1; }

.fadeModal-leave-from { opacity: 1; }
.fadeModal-leave-active { transition: all 1s; }
.fadeModal-leave-to { opacity: 0; }

</style>
