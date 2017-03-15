<template>
  <a :href="'http://m.360che.com/weixin/article.aspx?id=' + res.Url" class="news-item" :id="'achor_' + res.Url" @click.prevent="savePositon">
    <figure v-if="res.ImgSrc">
      <img :src="res.ImgSrc" alt="">
    </figure>
    <div class="content">
      <h3>{{res.Title}}</h3>
      <footer>
        <span class="total" v-if="res.CommentCount">
          <em>{{res.CommentCount}}</em>评论
        </span>
        <span class="tag">
          <img :src="res.SmallImg" width="30" height="14" v-if="res.SmallImg"/>
          <em v-if="res.Lable">#{{res.Lable}}</em>
        </span>
      </footer>
    </div>
  </a>
</template>

<script>
  import storage from '../util/storage'

  export default {
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
  .news-item{
    position: relative;
    display: flex;
    color:#333;
    text-decoration: none;
    flex-direction:row;
    padding:8px 15px 15px 0;
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
    .content{
      flex:1;
      h3{
        line-height: 24px;
        height:48px;
        overflow: hidden;
        font-weight: 700
      }
    }
    figure{
      margin:5px 15px 0 0;
      width: 90px;
      height:60px; 
      overflow: hidden;
      display: flex;
      flex-direction: column;
      flex-wrap: wrap;
      img{
          width: 100%;
          height: 100%;
          -webkit-object-fit: cover;
          object-fit: cover;
          display: block;
      }
    }
    footer{
      margin-top:5px;
      line-height:14px;
      overflow: hidden;
      font-size: 12px;
      .total{
        float: right;
        color:#999;
        em{
          margin-right:1px;
          font-size: 14px;
          color:#666
        }
      }
      .tag{
        color:#02BB00
      }
    }
  }  
</style>
