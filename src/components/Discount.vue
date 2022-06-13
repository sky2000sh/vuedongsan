<template>
<!-- 컴포넌트 만드는 순서
  1. 사용할 컴포넌트를 생성해서 그 vue파일을 import하고
  2. 등록하고
  3. 사용한다. -->
  <div class="discount">
    <h4>지금 결제하면 {{countNumber}}% 할인</h4> 
  </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Discount',

    mounted() {
    setInterval(() => {
      this.countNumber--

      if(Number(this.countNumber) === 0) {
        return 0
      }

      
    }, 1000)

    // clearTimeout(() => {
    //   Number(this.countNumber) === 0
    // })
  },

    data() {
      return {
        countNumber: 30
      }
    }

}
</script>

<style>
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>