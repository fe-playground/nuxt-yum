<template>
  <div class="popupWrap" v-show="popup">
    <div class="popupBody">
      <h2>{{title}}</h2>
      <p>{{text}}</p>
      <button @click="popup = false">{{btnText}}</button>
    </div>
    <div class="dim"></div>
  </div>
</template>

<script>
export default {
  name: 'popup',
  data () {
    return {
      title: 'sample title',
      text: 'smaple text',
      btnText: '123',
      popup: false
    }
  },
  created () {
    this.$EventBus.$on('SHOW_POPUP', props => {
      this.popup = true
      this.title = props.title
      this.text = props.text
      this.btnText = props.btnText
    })
  }
}
</script>

<style scoped>
.popupWrap {
  width: 100%;
  height: 100%;
}
.dim {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0,0,0,0.5);
}
.popupBody {
  width: 300px;
  height: 200px;
  background: #fff;
  position: absolute;
  top: 50%;
  right: 50%;
  margin-top: -100px;
  margin-right: -150px;
  z-index: 111;
  border-radius: 15px;
}
</style>
