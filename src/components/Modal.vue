<template>
  <div class="blackBg" v-if="openModal == true">
    <div class="whiteBg">
      <img :src="roomData[pressId].image" style="width: 100%"/>
      <h4>{{ roomData[pressId].title }}</h4>
      <p>{{ roomData[pressId].content }}</p>
      <p>{{ roomData[pressId].price }}원</p>
      <!-- <button @click="openModal = false">닫기</button>       -->
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
            
        }
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