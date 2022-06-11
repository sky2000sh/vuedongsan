<template>
  <div class="blackBg" v-if="openModal == true">
    <div class="whiteBg">
      <img :src="roomData[pressId].image" style="width: 100%"/>
      <h4>{{ roomData[pressId].title }}</h4>
      <p>{{ roomData[pressId].content }}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <!-- $event.target.value => 사용자가 input 태그에 입력한 글자값 -->
      <!-- <input v-model.number="month"> -->
      <input v-model="month">
      <!-- <textarea v-model="month"></textarea> -->
      <!-- <select v-model="month">
        <option>123</option>
        <option>456</option>
        <option>789</option>
      </select> -->
      <!-- <input type="checkbox" v-model="month"> -->
      <!-- <input type="range" min="1" max="12"> -->
      <p> {{ month }}개월 : {{ roomData[pressId].price * month}}원</p>
      <!-- <button @click="openModal = false">닫기</button> -->      
      <button @click="$emit('openModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Modal',

    props: {
        roomData: Object, // 데이터의 자료형 형식 ( Object, Array, String, Number, Boolean etc etc)
        pressId: Number,
        openModal: Boolean,
    },

    data() {
        return {
            month: 1,
        }
    },

    watch: {
      // watch => 데이터 month가 변할 때마다 month() 함수의 코드가 실행된다.
      // 이 때, month() 함수 명은 data의 명과 같이 해줘야한다.
      // 또는 ₩ ₩로도 사용해보기
      month(data) {
        console.log('month의 data는 :', data)
        if( data === '') {
          return true
        }
        if(data >= 13) {
          let month = 1
          alert('개월 수는 12까지만 가능합니다.')
          return month
          //return false
        }
        if( data !== Number(data) ) {
          alert('숫자만 입력가능합니다.')
        }        
      },

    }

}
</script>

<style>
.blackBg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}

.whiteBg {
  width: 500px; height: 530px;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

</style>