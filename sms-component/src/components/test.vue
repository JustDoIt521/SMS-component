<template>
  <div id="testInput">
    <ul @click="focusFix()">
    <input id="realInput" type="text" v-model="realInputValue" :maxlength="lengths"/>
      <li v-for="(item,index) in inputList" :key="index">
        <span>{{item.value}}</span>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'testInput',
  props: {
    listLength: {
      default: 5
    }
  },
  data () {
    return {
      realInputValue: '',
      inputList: [],
      lengths: this.listLength
    }
  },
  watch: {
    realInputValue: function (newValue) {
      let tempValue = newValue.split('')
      console.log(tempValue.length)
      for (let i = 0;i < tempValue.length; i++) {
        this.inputList[i].value = tempValue[i]
      }
      for (let i = tempValue.length; i < this.listLength; i++) {
        this.inputList[i].value = ''
      }
    }
  },
  created () {
    for (let i = 0; i < this.listLength; i++) {
      this.inputList.push({'value': ''})
    }
  },
  methods: {
    // 光标固定
    focusFix () {
      const  ID = document.getElementById("realInput")
      // console.log(ID)
      ID.focus()
      // console.log(ID.focus())
    }
  }
}
</script>
<style lang="less">
  #testInput{
    position:relative;
    #realInput{
      width:1px;
      height:1px;
      position:absolute;
      z-index:1;
      border:none;
      color:#fff;
      outline:none;
    }
    ul{
      // position:relative;
      // z-index: 100;
      // width: 400px;
      li{
        position:relative;
        z-index: 100;
        list-style: none;
        width: 18%;
        height: 30px;
        border: 1px solid #DCDCDC;
        line-height: 30px;
        float: left;
        text-align: center;
        .cursorBorder{
          position:relative;
        }
        .cursor{
          width:1px;
          height:30px;
          position:fixed;
          background:#000;
        } 
      }
    }
  }
</style>

