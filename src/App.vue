<template>
  <div id="app">
    <pwd-inputs
      class="inputs-style"
      ref="inputs"
      :pwdTexts="pwdTexts"
      :pwds="pwds"
      :currentFocusIndex="currentFocusIndex"
      @pwdTextsChange="pwdTextsChange"
      @pwdsChange="pwdsChange"
      @currentFocusIndexChange="currentFocusIndexChange">
    </pwd-inputs>
  </div>
</template>

<script>
import PwdInputs from './components/pwd-inputs';

export default {
  name: 'App',

  components: {
    PwdInputs
  },

  data () {
    return {
      refNames: [
        'input1',
        'input2',
        'input3',
        'input4',
        'input5',
        'input6',
      ],
      pwdTexts: ['', '', '', '', '', ''],
      pwds: ['', '', '', '', '', ''],
      currentFocusIndex: 0,
    };
  },

  computed: {
  },

  methods: {
    pwdTextsChange ({ index, value }) {
      this.pwdTexts[index] = value;
    },

    pwdsChange ({ index, value }) {
      this.pwds.splice(index, 1, value);
    },

    currentFocusIndexChange (index) {
      this.currentFocusIndex = index;
    },
  },

  async created () {
  },

  async mounted () {
  },
}
</script>

<style lang="less">
#app {
  font-family: "PingFangSC-Regular","PingFang SC","Helvetica Neue",Helvetica,"Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-overflow-scrolling: touch;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
  -ms-backface-visibility: hidden;
  backface-visibility: hidden;
  -webkit-perspective: 1000;
  -moz-perspective: 1000;
  -ms-perspective: 1000;
  perspective: 1000;
  -webkit-transform: translateZ(0);
  -moz-transform: translateZ(0);
  -ms-transform: translateZ(0);
  -o-transform: translateZ(0);
  transform: translateZ(0);
  margin: 0 auto;
  width: 100%;
  height: 100%;
  max-width: 470px;
  max-height: 850px;
  display: block;
  background: #eeeeee;
  overflow: hidden;
  font-size: 0.12rem;
  position: relative;

  .inputs-style {
    width: 88%;
    margin: .28rem auto 0;
  }
}

</style>
