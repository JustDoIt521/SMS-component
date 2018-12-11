<template>
    <div id="code">
      <input id="first" class="inputStyle" v-model="code[0]"
      style="border-top-left-radius: 12px; border-bottom-left-radius: 12px;"
      type="text"/>
      <input id="second" class="inputStyle" v-model="code[1]" style="border-left:1px solid #c6c6c6;" type="text"/>
      <input id="third" class="inputStyle" v-model="code[2]" style="border-left:1px solid #c6c6c6;" type="text"/>
      <input id="forth" class="inputStyle" v-model="code[3]" style="border-left:1px solid #c6c6c6;" type="text"/>
      <input id="fifth" class="inputStyle" v-model="code[4]"
      style="border-top-right-radius: 12px;border-bottom-right-radius: 12px;border-left:1px solid #c6c6c6;"
      maxlength="1"
      type="text"/>
    </div>
</template>
<script>
export default {
  name: 'phoneInput',
  data () {
    return {
      smsCode: '',
      code: new Array(5),
      codeId: ['first', 'second', 'third', 'forth', 'fifth']
    }
  },
  watch: {
    code: function (newValue, oldValue) {
      let tempValue = ''
      for (let i = 0; i < newValue.length; i++) {
        if (i === 5) {
          break
        }
        if (newValue[i]) {
          tempValue = tempValue + newValue[i]
        }
      }
      this.smsCode = tempValue
      let m = tempValue.split('')
      let location = 0
      for (let i = 0; i < newValue.length; i++) {
        if (m[i] && i < 5) {
          location++
          newValue[i] = m[i]
        } else {
          newValue[i] = ''
        }
      }
      if (location < 1) {
        location = 1
      } else if (location > 5) {
        location = 5
      }
      document.getElementById(this.codeId[location - 1]).focus()
    }
  }
}
</script>

<style>
#code {
  display: flex;
  width:500px;
  height: 30px;
  /* border-top:1px solid #DCDCDC !important;
  border-bottom:1px solid #DCDCDC !important; */
}
  .inputStyle{
    width:20%;
    height:100%;
    text-align: center;
    /* border:none; */
  }
</style>
