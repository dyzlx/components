<template lang="pug">
div.infoModel
    div.direction(contenteditable="plaintext-only" @focus="getFocus()" @blur="getBlur()" @input="changeInfo") {{infoContent}}
        div.tip
            p#tip.hidden click here to input teaching direction...
</template>

<script>
export default {
  name: 'infoModel',
  data() {
    return {
    };
  },
  computed: {

  },
  methods: {
    _moveEnd(obj) {
      obj.focus();
      const len = obj.innerText.length;
      let sel;
      if (document.selection) {
        sel = document.selection.createRange();
        sel.moveStart('character', len);
        sel.collapse();
        sel.select();
      } else {
        sel = window.getSelection();
        const range = document.createRange();
        range.selectNodeContents(obj);
        range.collapse(false);
        sel.removeAllRanges();
        sel.addRange(range);
      }
    },
    getFocus() {
      document.querySelector('p#tip').className = 'hidden';
    },
    getBlur() {
      if (this.infoContent.length === 0 || !this.infoContent) {
        document.querySelector('p#tip').className = 'show';
      }
    },
    changeInfo(val) {
      const element = document.querySelector('div.direction');
      this.infoContent = val.target.innerText;
      this._moveEnd(element);
    },
  },
};
</script>

<style lang="css">
    div.infoModel{
        position: relative;
        width: 100%;
        padding: 0 10px 10px 0;
    & > div.direction{
          border: var(--borderWidth) solid var(--borderColor);
          border-radius: 5px;
          height: 130px;
          overflow-y: scroll;
          word-wrap: break-word;
          outline: none;
          padding: 8px 15px;
    & > p{
          margin: 5px 0 !important;
      }
    }
    & > div.tip{
          position: absolute;
          top: 10px;
          left: 12px;
    & > p#tip{
          margin: 0;
          color: #606060;
    &.hidden{
         display: none;
     }
    &.show{
         display: block;
     }
    }
    }
    }
</style>
