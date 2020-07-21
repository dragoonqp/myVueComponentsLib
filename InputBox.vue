<template>
  <div class="inputBox" @click="$emit('onclick')">
    <div :class="{ focus: focus, default: true }" style="display:flex;justify-content:space-around;align-items:center; font-size:0.7rem">
      {{value}}
    </div>
  </div>
</template>




<script>
export default {
  name: "InputBox",
  data () {
    return {
      value:this.defaultValue,
      focus: false,
    };
  },
  props:{
    defaultValue: {
      type:String,
      default: '',
    },
  },
  methods: {
    onBlur(){
      this.focus = false;
    },
    onFocus(){
      this.focus = true;
    },
    setValue(value){
      this.value = value
    },
    getValue(){
      return this.value
    }
  },
  computed: {},
  components: {},
  
}
</script>
<style lang="css" scoped>
.inputBox{
  width: 1rem;
  height: 1rem;
  border: 1px solid gray;
  display: flex;
  justify-content: center;
  align-items: center;
}
.default{
  width: 0.6rem;
  height: 0.6rem;
}
.focus{
  color:#ff9900;
  border-bottom: 2px solid #ff9900;
}
</style>