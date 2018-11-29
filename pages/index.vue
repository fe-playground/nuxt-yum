<template>
  <div id="app">
    <div v-show="!start">
      <h2>사용자 이름 입력</h2>
      <input 
        type="text"
        :value="name"
        @input="updateName"
        placeholder="이름을 입력하세요"
        @keyup.enter="SET_START(true)"
      >
      <button @click="SET_START(true)">시작</button>
    </div>
    <div v-if="start">
      <p>{{name}}님 타이핑 화이팅!</p>
      <button @click="SET_START(false)">다시시작</button>
    </div>
    <Typing 
      v-if="start"
      :questionDate="questionDate"
    />
    <Popup/>
  </div>
</template>


<script>
import { mapState, mapMutations } from 'vuex'
import Typing from '../components/Typing.vue'
import Popup from '../components/Popup.vue'

export default {
  name: 'app',
  data () {
    return {
      questionDate: [
        '안녕하세요',
        '반갑습니다',
        '뷰는 처음이지?',
        '타이핑 화이팅'
      ]
    }
  },
  components: {
    Typing,
    Popup
  },
  computed: {
    ...mapState([
      'name',
      'start'
    ])
  },
  methods: {
    ...mapMutations([
      'SET_START',
      'UPDATE_NAME'
    ]),
    updateName(e) {
      this.$store.commit('UPDATE_NAME', e.target.value)
    },
    handleStop() {
      this.start = false
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
