<!--  -->
<template>
  <div class="mySelect">
      <input type="text" @focus="show" @blur="hide" v-model="myValue" placeholder="报事类型，点击显示下拉菜单">
      <div v-show="isShow">
          <ul>
              <li @click="choose($event)" @mousedown="click($event)">选项1</li>
              <li @click="choose($event)" @mousedown="click($event)">选项2</li>
              <li @click="choose($event)" @mousedown="click($event)">选项3</li>
              <li @click="choose($event)" @mousedown="click($event)">选项4</li>
          </ul>
      </div>
  </div>
</template>

<script>
export default {
    name:"mySelect",
    data () {
        return {
            isShow:false,
            myValue:""
        };
    },

    components: {},

    computed: {},

    mounted(){
    },

    methods: {
        show(){
            this.isShow=true;
        },
        hide(){

            this.isShow=false;
        },
        choose(e){
            this.myValue=e.target.innerHTML;
            
            this.isShow=false;
        },
        click(e){
            e.preventDefault();
        }
    }
}

</script>
<style scoped>
*{
    padding:0;
    margin:0;
}
.mySelect{
    position: relative;
}
.mySelect>div,.mySelect{
    width: 100%;
}
.mySelect>input{
    width: 100%;
    height:3rem;
    border:none;
    padding:0.5rem;
    color:#979797;
    font:0.9rem 微软雅黑;
    background: none;
    box-sizing: border-box;
    margin-bottom:1rem;
    border-bottom:1px solid #979797;
}
.mySelect>div{
    background: white;
    position:absolute;
    top:3rem;
    border:1px dashed #979797;
    box-sizing: border-box;
}
.mySelect>div>ul{
    list-style: none;
}
.mySelect>div>ul>li{
    height:3rem;
    width: 100%;
    border-bottom: 1px dashed #979797;
    display: flex;
    align-items: center;
    padding:0 0.5rem;
    box-sizing: border-box;
}
</style>