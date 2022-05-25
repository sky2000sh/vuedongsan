<template>
  <div class="menu">
    <!-- 반복적인 같은 태그를 효율적으로 돌리기 위해서는 v-for 반복문
    1. 원하는 태그에 v-for="작명 in 반복할횟수"
    2. 그리고 반복문에는 반드시 센스있게 :key="작명" 이것도 추가
    그럼 이 HTML 태그는 원하는 만큼 반복생성
    작명한 변수는 데이터안의 '자료'가 된다. -->
    <a v-for="menu in menuBar" :key="menu">{{ menu }}</a>
  </div>
  <div>
    원룸샵
    <h4 class="red" :style="스타일">{{ products[0] }}</h4>
    <!-- 속성을 나타낼때는 :을 명령어 앞에 붙여 :style로 만들어준다. -->
    <p>{{ price1 }} 만원</p>
  </div>
  <div>
    <h4>{{ products[1] }}</h4>
    <p>{{ price2 }} 만원</p>
  </div>
  <div>
    <h4>{{ products[2] }}</h4>
    <p>{{ price2 }} 만원</p>
  </div>
  <hr>
  <div>
    <h4 v-for="product in products" :key="product">{{ product }}</h4>
    <p v-for="price in prices" :key="price">{{price}}만원</p>
  </div>

</template>

<script>


export default {
  name: 'App',
  components: {

  },
  // data라는 데이터 보관함이 있어야 한다.
  // 데이터바인딩 : data의 변수명에 대한 값을 html안에 넣고 싶다면, {{ }} 안에 변수명을 넣어준다.
  // 데이터바인딩을 사용하는 이유 : 하드코딩을 해놓으면 변경하기에 어려움 / 가변적인 데이터를 보여줄때 사용 / Vue의 실시간 자동 렌더링을 하기 위해서
  // 자료이름 : 자료내용 => object 형식
  data() {
    return {
      //logo: '원룸샵',
      //price1: 60,
      //price2: 70,
      //스타일: 'color : blue',
      menuBar : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      prices : ['50', '60', '70'],

    }

  }
}
</script>

<style>
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
  padding: 10px;
}
</style>
