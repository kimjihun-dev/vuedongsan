<template>
    <div id="modal" class="black-bg" v-if="modalStatus == true">
        <div class="white-bg">
            <h4>{{ products[userSelect].title }}</h4>
            <img :src="products[userSelect].image" :alt="products[userSelect].title">
            <input type="text" v-model="month">
            <p> {{ month }}개월 선택함 <br> 가격 : {{ products[userSelect].price * month }}</p>
            <hr>
            <p>{{ products[userSelect].content }}</p>
            <button @click="$emit('closeModal');">닫기</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        products: Array,
        userSelect: Number,
        modalStatus: Boolean,
    },
    data() {
        return {
            month: 1,
        }
    },
    // 데이터 감시할때 사용 (input 받을 때 검증용)
    watch: {
        month(e) {
            if (e >= 13) {
                alert('13개월 이상은 불가능합니다.')
                this.month = 1
            }
            if (isNaN(e)) {
                alert('숫자만 입력 가능합니다')
                this.month = 1
            }
        },
    },
}
</script>

<style>
.black-bg { position: fixed; padding: 20px; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.5);  }
.white-bg { width: 100%; background: #fff; border-radius: 8px; padding: 20px; }
</style>