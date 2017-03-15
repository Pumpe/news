<template>
  <a :href="'http://m.360che.com/appvideo/VideoShare.aspx?Id=' + res.Id" class="video-item" :id="'achor_'+res.Id" @click.prevent="savePositon">
    <video-great v-if="res.SubType==1" :res="res" /> 
    <video-default v-else :res="res" />
  </a>
</template>

<script>
  import VideoDefault from './video-default.vue'
  import VideoGreat from './video-great.vue'
  import storage from '../util/storage'

  export default {
    components:{
      VideoDefault,
      VideoGreat
    },
    props:['res'],
    data () {
      return {
        loading:true
      }
    },
    methods:{
      savePositon(){
        storage.set('position',this.$el.offsetParent.scrollTop)
        location.href = this.$el.href;
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
  .video-item{
    position: relative;
    color:#333;
    padding:10px 15px 15px 0;
    display: block;
    &:after{
      position: absolute;
      bottom:0;
      left:0;
      content:"";
      height:1px;
      width: 200%;
      background-color:#E5E5E5;
      transform:translate(-25%,0) scale(.5);
    }
  } 
</style>
