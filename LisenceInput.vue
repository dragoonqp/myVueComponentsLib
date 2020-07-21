<template>
  <div id="LisenceInput">
    <div class="carLisence">
      <InputBox ref="CNName" @onclick="focusClick('CNName')" defaultValue="粤"/>
      <InputBox ref="ENLetter" @onclick="focusClick('ENLetter')" defaultValue="A"/>
      <InputBox ref="NO1" @onclick="focusClick('NO1')" />
      <InputBox ref="NO2" @onclick="focusClick('NO2')" />
      <InputBox ref="NO3" @onclick="focusClick('NO3')" />
      <InputBox ref="NO4" @onclick="focusClick('NO4')" />
      <InputBox ref="NO5" @onclick="focusClick('NO5')" />
      <div @click="addBox" v-if="!hasSixthBox" class="addBox" >+</div>
      <InputBox ref="NO6" v-else @onclick="focusClick('NO6')" />
    </div>
    <transition name="slideIn">
      <section  style="width: 100%;position:fixed;bottom:0" v-if="editBox !== ''">
        <div style="text-align:right;font-size:0.4rem;height:1rem;line-height:1rem;padding:0 5px;background:#f2f2f2"><span @click="hideKeybord">关闭</span></div>
        <!-- <div style="padding-left:5px" v-show="editBox === 'CNName'">
          <div v-for="(keyList, listIndex) in keyButtons" :key="listIndex" class="keyListBox2">
            <button v-for="(item,index) in keyList" :key="index" @click="setValue(item)" class="keyButton">{{item}}</button>
            <button v-if="listIndex==keyButtons.length-1" class="keyButton" style="right:3px;position:absolute" @click="deleteValue('')">X</button>
          </div>
        </div>
        <div style="padding-left:5px" v-show="editBox === 'ENLetter' || editBox === 'NO1' || editBox === 'NO2' || editBox === 'NO3' || editBox === 'NO4' || editBox === 'NO5'  || editBox === 'NO6'">
          <div class="keyListBox">
            <button v-for="(item,index) in numButtons" :key="index" @click="setValue(item)" class="keyButton" :disabled="editBox === 'ENLetter' && (/[\d军警港澳]/.test(item)) || (editBox === 'NO6' || editBox === 'NO1' || editBox === 'NO2' || editBox === 'NO3' || editBox === 'NO4') && (/[O军警港澳]/i.test(item))" v-show="(editBox === 'NO5' && !(/[O]/.test(item))) || editBox !== 'NO5'" :style="{color: editBox === 'ENLetter' && (/\d/.test(item))} ? '#ffffff' : 'black'">
              {{item}}
            </button>
            <button @click="setValue('学')" class="keyButton" v-show="editBox === 'NO5'" :style="{color: editBox === 'ENLetter' ? '#ffffff' : 'black'}">
              学
            </button>
            <button class="keyButton"  @click="deleteValue('')">X</button>
          </div>
        </div> -->
        <div style="padding-left:5px" v-show="editBox === 'CNName' ? CNInputType : !CNInputType">
          <div v-for="(keyList, listIndex) in keyButtons" :key="listIndex" class="keyListBox">
            <button v-if="listIndex==keyButtons.length-1" class="keyButton" style="bottom:5px;left:8px;position:absolute" @click="CNInputType = !CNInputType">ABC</button>
            <button v-for="(item,index) in keyList" :key="index" @click="setValue(item)" class="keyButton">{{item}}</button>
            <button v-if="listIndex==keyButtons.length-1" class="keyButton iconfont icon-guanbi" style="right:3px;position:absolute;bottom:5px;" @click="deleteValue('')"></button>
          </div>
        </div>
        <div style="padding-left:5px" v-show="editBox === 'CNName' ? !CNInputType : CNInputType">
          <div v-for="(keyList, listIndex) in numButtons" :key="listIndex" class="keyListBox">
            <button v-if="listIndex==keyButtons.length-1" class="keyButton" style="left:6px;position:absolute" @click="CNInputType = !CNInputType">字</button>
            <button v-for="(item,index) in keyList" :key="index" @click="setValue(item)" class="keyButton" :disabled="editBox === 'ENLetter' && (/\d/.test(item)) && !/[OI]i/.test(item)" :style="{color: editBox === 'ENLetter' && (/\d/.test(item))} ? '#ffffff' : 'black'">
              {{item}}
            </button>
            <button v-if="listIndex==keyButtons.length-1" class="keyButton iconfont icon-guanbi" style="right:3px;position:absolute; bottom:5px;color:rgb(51, 136, 255);border-color:rgb(51, 136, 255)" @click="deleteValue('')"></button>
          </div>
        </div>
      </section>
    </transition>
  </div>
</template>

<script>
// @ is an alias to /src
import InputBox from '@/components/InputBox.vue'

export default {
  name: 'LisenceInput',
  data(){
    return {
      editBox: '',
      CNInputType: true,
      hasSixthBox: false,
      keyButtons:[
        // ['京','津','渝','沪','冀','晋','辽','吉','黑'],
        // ['浙','皖','闽','赣','鲁','豫','鄂','湘','粤'],
        // ['川','贵','云','陕','甘','青','蒙','桂'],
        // ['藏', 'W','苏','琼','宁','新']
        ['京','津','渝','沪','冀','晋','辽','吉','黑','苏'],
        ['浙','皖','闽','赣','鲁','豫','鄂','湘','粤','琼'],
        ['川','贵','云','陕','甘','青','蒙','桂','宁','新'],
        ['藏','使','领','警','学','港','澳','挂']
      ],
      numButtons:[
        // '1','2','3','4','5','6','7','8','9','0',
        // 'Q','W','E','R','T','Y','U','O','P', '军',
        // 'A','S','D','F','G','H','J','K','L','警',
        // 'Z','X','C','V','B','N','M', '港','澳'
        ['1','2','3','4','5','6','7','8','9','0'],
        ['Q','W','E','R','T','Y','U','I','O','P'],
        ['A','S','D','F','G','H','J','K','L'],
        ['Z','X','C','V','B','N','M']
      ],
    }
  },
  methods:{
    addBox(){
      this.hasSixthBox = true
    },
    hideKeybord(){
      this.editBox = '';
      Object.keys(this.$refs).forEach((item) => {
        this.$refs[item].onBlur()
      })
    },
    focusClick(refText){
      Object.keys(this.$refs).forEach((item) => {
        this.$refs[item].onBlur()
      })
      this.$refs[refText].onFocus()
      this.editBox = refText
    },
    setValue(value){
      let arr = Object.keys(this.$refs)
      let index = arr.indexOf(this.editBox)
      if(this.editBox !== ""){
        this.$refs[this.editBox].setValue(value)
        this.$refs[this.editBox].onBlur()
        this.editBox = ''
        if(index < arr.length -1){
          this.editBox = arr[index+1]
          this.$refs[this.editBox].onFocus()
        }
      }
    },
    deleteValue(value){
      let arr = Object.keys(this.$refs)
      let index = arr.indexOf(this.editBox)
      if(this.editBox !== ""){
        this.$refs[this.editBox].setValue(value)
        this.$refs[this.editBox].onBlur()
        this.editBox = ''
        if(index > 0){
          this.editBox = arr[index-1]
          this.$refs[this.editBox].onFocus()
        }
      }
    },
    getLisence(){
      let carLisence = '';
      Object.keys(this.$refs).forEach((item) => {
        carLisence += this.$refs[item].getValue()
      })
      return carLisence
    }
  },
  components: {
    InputBox
  }
}
</script>
<style scoped>
.addBox{
  width: 1rem;
  height: 1rem;
  border: 1px solid gray;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size:0.6rem;
  color:gray;
}
.carLisence{
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding:0 0.5rem;
}
.slideIn-enter,.slideIn-leave-to{
  transform: translateY(30vh);
}
.slideIn-enter-active, .slideIn-leave-active {
  transition: all .3s;
}
/* .keybord{
  position: fixed;
  bottom: -30vh;
  left:0;
  transition: all 0.2s linear;
  background: gray;
}
.Active{
  bottom: 0;
} */
.keyButton{
  width:  calc( 10vw - 6px);
  height: calc( 10vw - 6px);
  margin: 2px 5px 2px 0;
  background: white;
  border-radius: 4px;
  outline: none;
  border: 1px solid gray;
  font-size: 0.45rem;
}
.keyListBox{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap ;
  margin: 5px 0;
}
.keyListBox2{
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2px 0;
}
</style>
