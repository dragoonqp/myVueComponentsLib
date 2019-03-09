<!--  -->
<template>
  <div class="zoomPic">
      <div class="midPicHolder" @mousemove="move($event)" @mouseover="showMagnifier" @mouseout="hideMagnifier" :style="{width:size+'px',height:size+'px'}">
          <img :src="midPic" alt="">
          <div class="cover" ></div>
          <div id="magnifier" class="magnifier" :style="{left:magnifierLeft+'px',top:magnifierTop+'px',display:magIsShow}"></div>
      </div>
      <div class="smallPicHolder" :style="{width:size+'px',height:size/5+'px'}">
          <a href="javascript:;" class="prev" @click="prev">&lt;</a>
          <ul :style="{left:n*20+'%',width:this.sPiclist.length/5*100+'%'}">
              <li v-for="(url,index) in sPiclist" :key="index"><img :src="url" alt="" @mouseover="getSrc($event)"></li>
          </ul>
          <a href="javascript:;" class="next" @click="next">&gt;</a>
      </div>
      <div class="bigPicHolder" :style="{display:magIsShow,left:bigLeft+'px',top:0,width:size*1.2+'px',height:size*1.2+'px'}">
          <img :src="bigPic" alt="" :style="{left:bigPicLeft+'px', top:bigPicTop+'px'}">
      </div>
  </div>
</template>

<script>
export default {
    data () {
        return {
            magnifierLeft:0,
            magnifierTop:0,
            magnifierWidth:this.size/6,
            magnifierHeight:this.size/6,
            magIsShow:"none",
            midPic:"",
            bigPic:"",
            bigLeft:this.size,
            bigPicLeft:0,
            bigPicTop:0,
            n:0
        };
    },
    props:["sPiclist","size"],
    components: {},

    computed: {},

    mounted(){
        console.log(this.sPiclist.length)
    },

    methods: {
        getSrc(e){
            this.midPic=e.target.src;
            this.bigPic=e.target.src;
        },
        showMagnifier(){
            this.magIsShow="block";
        },
        hideMagnifier(){
            this.magIsShow="none"
        },
        move(e){
            console.log(this.magnifierWidth)
            this.magnifierLeft=e.offsetX-this.magnifierWidth;
            if(e.offsetX<this.size/6){
                this.magnifierLeft=0;
            }else if(e.offsetX>this.size-this.size/6){
                this.magnifierLeft=this.size-this.size/3;
            }
            this.magnifierTop=e.offsetY-this.magnifierHeight;
            if(e.offsetY<this.size/6){
                this.magnifierTop=0;
            }else if(e.offsetY>this.size-this.size/6){
                this.magnifierTop=this.size-this.size/3;
            }
            this.bigPicLeft=-(this.magnifierLeft)*3.6;
            this.bigPicTop=-(this.magnifierTop)*3.6;
        },
        prev(){
            if(this.n<0){this.n++}
        },
        next(){
            if(this.n>-(this.sPiclist.length-5)&&this.sPiclist.length>5){
                this.n--;
            }
        }
    }
}

</script>
<style scoped>
*{
    padding:0;
    margin:0;
}
.zoomPic{
    position: relative;
}
.midPicHolder{
    width:25rem;
    height:25rem;
    position: relative;
    border:1px solid black;
    border-bottom:none;
}
.midPicHolder>.magnifier{
    width:33.3333%;
    height: 33.3333%;
    background: rgba(255,255,255,0.4);
    position: absolute;
    z-index: 1;
}
.midPicHolder>.cover{
    position: absolute;
    width: 100%;
    height:100%;
    top:0;
    left:0;
    background: transparent;
    z-index: 10;
}
.midPicHolder>img{
    width:100%;
    height:100%;
}
.smallPicHolder{
    width:25rem;
    height:5rem;
    border:1px solid black;
    overflow: hidden;
    position:relative;
}
.smallPicHolder>ul{
    position:absolute;
    list-style: none;
    height:100%;
    display: flex;
    justify-content: flex-start;
    z-index: 1;
    transition: all 0.3s linear;
}
.smallPicHolder>ul>li{
    height:100%;
    width:20%;
}
.smallPicHolder>ul>li>img{
    width: 100%;
}
.prev,.next{
    position:absolute;
    display: flex;
    height:100%;
    width:6%;
    background:rgba(255,255,255,0.5);
    top:0;
    justify-content: center;
    align-items: center;
    z-index: 10;
}
.prev{
    left:0;
}
.next{
    right:0;
}
.bigPicHolder{
    position:absolute;
    overflow: hidden;
}
.bigPicHolder>img{
    position:absolute;
    width: 300%;
    height: 300%;
}
</style>