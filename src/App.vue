<template>
  <!-- 
    동적인 UI 만드는 법 :
    1. UI의 현재 상태를 데이터로 저장해둔다.
    2. 데이터에 따라 UI가 어떻게 보일지 작성한다.

    v-if="조건식" => 조건식이 참일때만 HTML을 보여준다.
  -->
  <!-- <div class="blackBg" v-if="openModal == true">
    <div class="whiteBg">
      <img :src="roomData[pressId].image" style="width: 100%"/>
      <h4>{{ roomData[pressId].title }}</h4>
      <p>{{ roomData[pressId].content }}</p>
      <p>{{ roomData[pressId].price }}원</p>
      <button @click="openModal = false">닫기</button>      
    </div>
  </div> -->
  <transition name="fade">
  <!-- CSS로 애니메이션 주기 2번째는, vue의 transition 태그를 사용하기
  1. 애니메이션 주고싶은 요소를 <transition>으로 감싸기
  2. 아래 style의 다음 클래스명 3개가 있어야한다.
      fade-enter-from / fade-enter-active / fade-enter-to
      이 때, name이 fade이기 때문에 각 3개의 이름 시작이 fade인것이지, fade 이름은 작명이 가능하다.
      즉, name 명 따라서 변경이 가능하다.
  3. 

  -->
  <!-- <div class="startModal" :class="{ endModal: openModal }"> -->
    <!-- CSS로 애니메이션 주려면
    1. 시작전 class 명 => startModal
    2. 애니메이션 끝난 후 class 명 => endModal
    3. 그리고 원할 때 2번 class명 부착
    *** endModal가 실행될 때 style .endModal이 실행되기 때문에,
    openModal이 true일 때만 .endModal이 실행되도록 만든다.
    -->
    <Modal @openModal="openModal = false" :roomData="roomData" :pressId="pressId" :openModal="openModal"/>
  <!-- </div> -->
  </transition>
  <!-- props로 자식에게 데이터 보내는 법
  1. 데이터 보내고 :roomData="roomData" 이때 :roomData는 맘대로 작명가능 / "roomData"는 data의 실제 데이터이름
  2. 자식 component에 등록하고
  3. 자식 component에서 이들을 사용한다.
  *** 그럼 애초에 자식.vue 컴포넌트에 데이터를 생성해서 사용하면 되지 않을까 싶지만,
  이는 가능하지만 부모 컴포넌트에도 쓰는 데이터라면 부모 컴포넌트에 생성하는게 좀 더 올바르다.

  아래 data인 Object 형태인 roomObj에 있는 name, quanity, quanlity를
  roomObj.name / roomObj.quanity / roomObj.quanlity 형식으로 각각 props로 전송하려면
  v-bind="Object 데이터이름" 으로 만들어주고 똑같이 2번과 3번을 수행한다.
  -->



  <div class="menu">
    <!-- 반복적인 같은 태그를 효율적으로 돌리기 위해서는 v-for 반복문
    1. 원하는 태그에 v-for="작명 in 반복할횟수"
    2. 그리고 반복문에는 반드시 센스있게 :key="작명" 이것도 추가
    그럼 이 HTML 태그는 원하는 만큼 반복생성
    작명한 변수는 데이터안의 '자료'가 된다. -->
    <a v-for="menu in menuBar" :key="menu">{{ menu }}</a>
  </div>

  <!-- <Discount v-if="showDiscount === true"/> -->
  <Discount/>
  <!-- 컴포넌트 만드는 순서
  1. 사용할 컴포넌트를 생성해서 그 vue파일을 import하고
  2. 등록하고
  3. 사용한다. 
  *** 초보들의 특징이 온갖거 다 컴포넌트로 만들어두기 때문에 그러지말고, 반복적으로 출현할 부분만 컴포넌트화 할것을 권장.
  -->

  <button @click="priceSort">가격순 정렬</button>
  <button @click="priceResort">가격역순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <!-- <div v-for="(rooms, i) in roomData" :key="i">
    <img :src="rooms.image" class="roomImg"/>
    <h4 @click="openModal = true; pressId = i">{{ rooms.title }}</h4>
    <p>{{ rooms.price }}원</p>
  </div> -->

  <!-- <div v-for="rooms in roomData" :key="rooms">
    <img :src="rooms.image" class="roomImg"/>
    <h4 @click="openModal = true; pressId = rooms.id">{{ rooms.title }}</h4>
    <p>{{ rooms.price }}원</p>
  </div> -->

  <!-- <Card :roomData="roomData[i]" v-for="(rooms, i) in roomData" :key="rooms"/> -->

  <!-- Card.vue => 부모에게 메시지를 보낼 때는, $emit('작명', 데이터) ex) $emit('openModal', true) / $emit('openModal', null) / $emit('openModal') -->
  <!-- 그 후, App.vue => Card 컴포넌트에 @보내서 받은 작명="javascript 표기"
      ex) @openModal="openModal = true" -->
  <Card @openModal="openModal = true; pressId = $event" :roomData="roomData" :pressId="pressId" :openModal="openModal"
        v-bind="roomObj"/>

  <!--
    <div>
    원룸샵
    <hr>
    <img src="./assets/room0.jpg" class="roomImg"/>
    <img :src="roomData[0].image" class="roomImg"/>
    <h4 class="red" @click="openModal = true">{{ roomData[0].title }}</h4>
    속성을 나타낼때는 :을 명령어 앞에 붙여 :style로 만들어준다.
    <p>{{ roomData[0].price }}원</p>
    <button v-on:click = "reportCnt += 1">허위매물신고</button> <span>신고수 : {{reportCnt}}</span>
    버튼을 눌렀을 때 자바스크립트처럼 이벤트를 타게 하려면 v-on:click=""을 사용한다.
    또는 @click=""도 vue 방식으로써 역시 가능하다.
    *** reportCnt += 1을 사용하려면 "" 안에 넣어서 "reportCnt += 1"로 하던가, 아님 reportCnt++ 로 만들어준다.
    *** 혹은 함수(function())을 사용해서 타라WMS에서 했듯이 script 부분 아랫쪽으로 보내서 길게 코딩할 수도 있다.
        함수를 써서 script 부분 아랫쪽에 보내서 함수 선언할 때는 함수안에 data{} 부분들을 가져가기 위해 this.을 사용해서 데이터명을 완성해준다.
    원래 자바스크립트 방식은 onClick=""
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
  </div> -->
  

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
  </div>
  -->

</template>

<script>
import roomData from './assets/oneroom'
// import discount from './components/Discount.vue'
import Discount from './components/Discount.vue'
import Modal from './components/Modal.vue'
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    //Discount : discount
    Discount,
    Modal,
    Card,

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
      roomDataCopy: '',
      prices : ['50', '60', '70'],
      reportCnt : 0,
      reportCntArr : [0, 0, 0],
      openModal : false,
      pressId : 0,
      roomObj : {
        name: '',
        quantity: '',
        quanlity: '',
      },
      showDiscount: true,
      Discount,

    }

  },

  created() {

  },

  beforeMounted() {

  },

  mounted() {
    // mounted에서 this를 쓸 일이 있다면 ()=> arrow함수를 잘 사용하도록 하자
    // 밖에서 mounted안으로 끌어다 쓰겠다라는 공식 함수이기 때문에.
    setTimeout(() => {
      this.showDiscount = false
    }, 2000)

  },

  methods: {

    priceSort() {
      // .sort() => 객체.sort()를 사용하면 객체의 오름순으로 정렬이 된다.
      this.roomData.sort(function(a, b) {
        return a.price - b.price
      })
    },

    priceResort() {
      this.roomData.sort(function(a, b) {
        return b.price - a.price
      })
    },

    titleSort() {
      this.roomData.sort(function(a, b) {
        return a.title - b.title
      })
    },

    sortBack() {
      // array / Object 데이터의 각각 별개의 사본을 만들려면 [...array자료] 라고 입력한다.
      this.roomDataCopy = [...roomData]
      this.roomData = [...this.roomDataCopy]

      // 깊은 복사
      // this.roomDataCopy = Object.assign({}, roomData);
    },
    
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

body {
  margin: 0;
}

div {
  box-sizing: border-box;
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

.startModal {
  opacity: 0;
  transition: all 1s;
}

.endModal {
  opacity: 1;
}

/* 입장 애니메이션 */
.fade-enter-from {
  /* 시작 시 스타일 */
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  /* 끝날 시 스타일 */
  opacity: 1;
}

/* 퇴장 애니메이션 */
.fade-leave-from {
  /* Y축으로 솟구치게 한다. 즉, 위로 올라가게 한다. */
  transform: translateY(-1000px);   
  /* 시작 시 스타일 */
  /* opacity: 0; */
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  /* 끝날 시 스타일 */
  opacity: 1;
}

</style>
