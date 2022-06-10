<template>
  <div v-for="rooms in roomData" :key="rooms">
    <img :src="rooms.image" class="roomImg"/>
    <!-- <h4 @click="openModal = true; pressId = rooms.id">{{ rooms.title }}</h4> -->
    <p>{{ rooms.price }}원</p>
  </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Card",

    props: {
        roomData: Object, // 데이터의 자료형 형식 ( Object, Array, String, Number, Boolean etc etc)
        pressId: Number,
        openModal: Boolean,

    },

}
</script>

<style>

</style>