<template>
  <a :href="'http://m.360che.com/weixin/article.aspx?id=' + res.Url" class="news-item">
    <div class="content">
      <h3>{{res.Title}}</h3>
      <footer>
        <span class="total" v-if="res.CommentCount">{{res.CommentCount}}评论</span>
        <span class="tag" v-if="res.SmallImg">
          <img :src="res.SmallImg" width="30" height="14" />
        </span>
      </footer>
    </div>
    <figure v-if="res.ImgSrc">
      <img :src="res.ImgSrc" alt="">
    </figure>
  </a>
</template>

<script>
  export default {
    props:['info'],
    data () {
      return {
        loading:true
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
  .news-item{
    display: flex;
    color:#333;
    text-decoration: none;
    flex-direction:row;
    padding:10px 15px 15px 0;
    .content{
      flex:1;
      h3{
        line-height: 24px;
        height:48px;
        font-weight: 700
      }
    }
    figure{
      margin:5px 0 0 15px;
      width: 90px;
      height:60px; 
      overflow: hidden;
      img{
        max-width: 100%;
      }
    }
  }  
</style>
