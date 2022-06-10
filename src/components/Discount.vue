<template>
<!-- 컴포넌트 만드는 순서
  1. 사용할 컴포넌트를 생성해서 그 vue파일을 import하고
  2. 등록하고
  3. 사용한다. -->
  <div class="discount">
    <h4>지금 결제하면 20% 할인</h4> 
  </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Discount',

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