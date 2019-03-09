<!--  -->
<template>
  <div class="myTextarea">
      <div>
        <textarea name="" id="" cols="30" rows="10" maxlength="200" :placeholder="placeholder" @input="cal($event)"></textarea>
        <p>{{lengthLeft}}字</p>
      </div>
  </div>
</template>

<script>
export default {
    data () {
        return {
            lengthLeft:200,
        };
    },
    props:["placeholder"],
    components: {},

    computed: {},

    mounted(){},

    methods: {
        cal(e){
            this.lengthLeft=200-e.target.value.length;
        }
    }
}

</script>
<style scoped>
*{
    padding:0;
    margin:0;
}
.myTextarea>div{
    width: 100%;
}
.myTextarea>div>textarea{
    width: 100%;
    border:1px solid #d5d2d2;
    margin: 0 0.1rem;
    padding:0.5rem;
    box-sizing: border-box;
}
.myTextarea>div>p{
    text-align: right;
    color:#979797;
}
</style>