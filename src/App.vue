<template>
  <!-- 
    동적인 UI 만드는 법 :
    1. UI의 현재 상태를 데이터로 저장해둔다.
    2. 데이터에 따라 UI가 어떻게 보일지 작성한다.

    v-if="조건식" => 조건식이 참일때만 HTML을 보여준다.
  -->
  <div class="blackBg" v-if="openModal == true">
    <div class="whiteBg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
      <button @click="openModal = false">닫기</button>      
    </div>
  </div>



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
    <hr>
    <!-- <img src="./assets/room0.jpg" class="roomImg"/> -->
    <img :src="roomData[0].image" class="roomImg"/>
    <h4 class="red" @click="openModal = true">{{ roomData[0].title }}</h4>
    <!-- 속성을 나타낼때는 :을 명령어 앞에 붙여 :style로 만들어준다. -->
    <p>{{ roomData[0].price }}원</p>
    <button v-on:click = "reportCnt += 1">허위매물신고</button> <span>신고수 : {{reportCnt}}</span>
    <!-- 버튼을 눌렀을 때 자바스크립트처럼 이벤트를 타게 하려면 v-on:click=""을 사용한다.
    또는 @click=""도 vue 방식으로써 역시 가능하다.
    *** reportCnt += 1을 사용하려면 "" 안에 넣어서 "reportCnt += 1"로 하던가, 아님 reportCnt++ 로 만들어준다.
    *** 혹은 함수(function())을 사용해서 타라WMS에서 했듯이 script 부분 아랫쪽으로 보내서 길게 코딩할 수도 있다.
        함수를 써서 script 부분 아랫쪽에 보내서 함수 선언할 때는 함수안에 data{} 부분들을 가져가기 위해 this.을 사용해서 데이터명을 완성해준다.
    원래 자바스크립트 방식은 onClick="" -->
  </div>
  <div>
    <img :src="roomData[1].image" class="roomImg"/>
    <h4>{{ roomData[1].title }}</h4>
    <p>{{ roomData[1].price }}원</p>
    <button v-on:click = reportCntArr[1]++>허위매물신고</button> <span>신고수 : {{reportCntArr[1]}}</span>
  </div>
  <div>
    <img :src="roomData[2].image" class="roomImg"/>
    <h4>{{ roomData[2].title }}</h4>
    <p>{{ roomData[2].price }}원</p>
    <button v-on:click = "reportCntArr[2] += 1">허위매물신고</button> <span>신고수 : {{reportCntArr[2]}}</span>
  </div>
  <div>
    <img :src="roomData[3].image" class="roomImg"/>
    <h4>{{ roomData[3].title }}</h4>
    <p>{{ roomData[3].price }}원</p>
  </div>
  <div>
    <img :src="roomData[4].image" class="roomImg"/>
    <h4>{{ roomData[4].title }}</h4>
    <p>{{ roomData[4].price }}원</p>
  </div>
  <div>
    <img :src="roomData[5].image" class="roomImg"/>
    <h4>{{ roomData[5].title }}</h4>
    <p>{{ roomData[5].price }}원</p>
  </div>
  

  <!--  div 태그에 반복문을 달아 똑같이 반복 제목을 만들기
  <hr> -->
  <!-- <div v-for="(product, i) in products" :key="i">
    <h4>{{ products[i] }}</h4>
    <p>50만원</p>
  </div> -->

  <!-- div 태그에 반복문을 달아 똑같이 상품목록을 만들기 -->
  <!-- <div v-for="rooms in roomData" :key="rooms">
    <img :src="rooms.image" class="roomImg"/>
    <h4>{{ rooms.title }}</h4>
    <p>{{ rooms.price }}원</p>
  </div> -->

</template>

<script>
import roomData from './assets/oneroom'

export default {
  name: 'App',
  components: {

  },
  // data라는 데이터 보관함이 있어야 한다.
  // 데이터바인딩 : data의 변수명에 대한 값을 html안에 넣고 싶다면, {{ }} 안에 변수명을 넣어준다.
  // 데이터바인딩을 사용하는 이유 : 하드코딩을 해놓으면 변경하기에 어려움 / 가변적인 데이터를 보여줄때 사용 / Vue의 실시간 자동 렌더링을 하기 위해서
  // 자료이름 : 자료내용 => object 형식
  data() {
    // data들을 "state"라고 부르기도 한다.
    return {
      //logo: '원룸샵',
      //price1: 60,
      //price2: 70,
      //스타일: 'color : blue',
      menuBar : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
      roomData,
      prices : ['50', '60', '70'],
      reportCnt : 0,
      reportCntArr : [0, 0, 0],
      openModal : false,

    }

  },

  methods: {
    
  },
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

.blackBg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}

.whiteBg {
  width: 500px; height: 250px;
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

.roomImg {
  width: 300px;
  margin-top: 40px;

}
</style>
