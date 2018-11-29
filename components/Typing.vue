<template>
  <div>
    <ul>
      <li v-for="(question, i) in questionDate" :key="i">
        <p>{{question}}</p>
        <input
          type="text"
          ref="questionText"
          :autofocus="active === i"
          :readonly="active !== i"
          @keyup.enter="handleCheck"
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TypingExercise',
  props: {
    questionDate: Array
  },
  data () {
    return {
      active: 0
    }
  },
  methods: {
    handleCheck(e) {
      if (this.questionDate[this.active] === e.target.value) {
        this.active++
        if ( this.active < this.questionDate.length) {
          this.$EventBus.$emit('SHOW_POPUP', {
            title: '굿',
            text: '잘쳤어요',
            btnText: '다음문장'
          })
          this.$refs.questionText[this.active].focus()
        } else {
          this.$EventBus.$emit('SHOW_POPUP', {
            title: '굿',
            text: '다쳤어요',
            btnText: '끝'
          })
        }
      } else {
        this.$EventBus.$emit('SHOW_POPUP', {
          title: '이런',
          text: '오타가있어요',
          btnText: '다시'
        })
      }
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
input {
  display: block;
  margin: 10px auto 20px;
  height: 40px;
  width: 600px;
  outline: 0;
  border: 1px solid #ddd;
  border-radius: 7px;
  padding: 3px 10px;
  font-size: 16px;
  text-align: center;
}
section {
  text-align: center;
  padding: 30px;
  background: #f9f9f9;
}
</style>
