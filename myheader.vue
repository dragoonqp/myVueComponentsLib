<!--  -->
<template>
  <div class="myheader">
      <span class="back" @click="$router.back(-1)"><i class="iconfont icon-fanhui"></i></span>
      <span>{{title}}</span>
  </div>
</template>

<script>
export default {
    name:"myheader",
    data () {
        return {
        }
    },
    props:["title"],
    components: {},

    computed: {},

    mounted(){},

    methods: {}
}

</script>
<style scoped>
*{
    margin: 0;
    padding:0;
}
.myheader{
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
.myheader span.back{
    position:absolute;
    left:12px;
    font:1.6rem 微软雅黑;
    color:white;
    text-decoration: none;
}
.myheader>span.back>i{
    font: 1.6rem 微软雅黑;
}

</style>