<template>
  <div class="inputs">
    <div class="input-wrap" v-for="(pwd, index) of pwdLength" :key="index">
      <input :ref="refNames[index]" type="text" maxlength="1" :data-input-index="index + 1" @input="afterInput" @keydown="afterKeydown" :value="pwds[index]">
    </div>
  </div>
</template>

<script>
export default {
  name: 'PwdInputs',

  props: {
    pwdLength: {
      type: Number,
      default: 6
    },
    refNames: {
      type: Array,
      default () {
        return [
          'input1',
          'input2',
          'input3',
          'input4',
          'input5',
          'input6',
        ];
      }
    },
    pwds: {
      type: Array,
      default () {
        return ['', '', '', '', '', ''];
      }
    },
    pwdTexts: {
      type: Array,
      default () {
        return ['', '', '', '', '', ''];
      }
    },
    currentFocusIndex: {
      type: Number,
      default: 0
    },
  },

  data () {
    return {
    };
  },

  async mounted () {
  },

  methods: {
    focusInStart () {
      try {
        this.$refs[this.refNames[0]][0].focus();
      } catch (err) {
        throw err;
      }
    },

    focusInEnd () {
      try {
        this.$refs[this.refNames[this.pwdLength - 1]][0].focus();
      } catch (err) {
        throw err;
      }
    },

    focusTargetInput (target) {
      try {
        this.$refs[this.refNames[target]][0].focus();
      } catch (err) {
        throw err;
      }
    },

    afterInput (event) {
      // console.log('afterInput event', event);
      if (event.target.dataset && event.target.value !== undefined && event.target.value !== null && event.target.value.trim() !== '') {
        const index = Number(event.target.dataset.inputIndex);
        this.$emit('pwdTextsChange', { index: index - 1, value: event.target.value });
        this.$emit('pwdsChange', { index: index - 1, value: '*' });
        event.target.value = '*';
        if (index === this.pwdLength) {
          return;
        }
        this.$nextTick(() => {
          this.$refs[this.refNames[index]][0].focus();
          this.$emit('currentFocusIndexChange', index);
        });
      }
    },

    afterKeydown (event) {
      // console.log('afterKeydown event', event);
      if (event.key === 'Backspace') {
        const index = Number(event.target.dataset.inputIndex);
        this.$emit('pwdTextsChange', { index: index - 1, value: '' });
        this.$emit('pwdsChange', { index: index - 1, value: '' });
        if (index > 1) {
          this.$nextTick(() => {
            this.$refs[this.refNames[index - 2]][0].focus();
            this.$emit('currentFocusIndexChange', index - 2);
          });
        }
      }
    },
  },
}
</script>

<style lang="less" scoped>
  .inputs {
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: space-around;

    > .input-wrap {
      height: 40px;
      width: 40px;
      font-size: 16px;
      text-align: center;
      flex-grow: 0;
      flex-shrink: 1;
      border: 1px solid #be9f79;
      // border-radius: 16px;
      box-sizing: border-box;
      display: flex;
      align-items: center;

      input {
        outline: none;
        border: none;
        height: 20px;
        font-size: 16px;
        width: 100%;
        text-align: center;
        background-color: transparent;
      }
    }
  }
</style>
