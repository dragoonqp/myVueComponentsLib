<!--  -->
<template>
  <div class="myheader2">
      <router-link to="/"><i class="iconfont icon-fanhui"></i></router-link>
      <div>
          <div :class="{active:!isactive}" @click="act(false)">问题详情</div>
          <div :class="{active:isactive}" @click="act(true)">处理进度</div>
      </div>
  </div>
</template>

<script>
export default {
    name:"myheader2",
    data () {
        return {
        }
    },
    props:["isactive"],
    components: {},

    computed: {},

    mounted(){
        
    },

    methods: {
        act(bool){
            if(bool==false){
                this.$router.push("/problemDetail");
                // this.isactive=false;
            }else{
                this.$router.push("/woProgress");
                // this.isactive=true;
            }
        }
    }
}

</script>
<style scoped>
*{
    margin: 0;
    padding:0;
}
.myheader2{
    width: 100%;
    height:3.8rem;
    background: #292929;
    color:white;
    display: flex;
    justify-content: center;
    align-items: center;
    font:1.4rem 微软雅黑;
    position:relative;
}
.myheader2 a{
    position:absolute;
    left:12px;
    font:1.6rem 微软雅黑;
    color:white;
    text-decoration: none;
}
.myheader2>a>i{
    font: 1.6rem 微软雅黑;
}
.myheader2>div{
    width: 60%;
    display: flex;
    justify-content: center;
    align-items: center;
}
.myheader2>div>div{
    width: 50%;
    height:2.4rem;
    background:#292929;
    border:1px solid white;
    color:white;
    font:1.1rem 微软雅黑;
    display: flex;
    justify-content: center;
    align-items: center;
}
.myheader2>div>div:first-child{
    border-radius: 1.2rem 0 0 1.2rem;

}
.myheader2>div>div:last-child{
    border-radius: 0 1.2rem 1.2rem 0;

}
.myheader2>div>div.active{
    color:#f06363;
    border-color:#f06363;
    background: white;
}
</style>