<template>
	<div class="default" v-else>
      <figure v-if="res.ImageUrl">
        <img :src="res.ImageUrl" alt="">
      </figure>
      <div class="content">
        <h3>{{res.Title}}</h3>
        <footer>
          <div class="total">
            <span>
              <em>{{res.ViewCount}}</em>播放
            </span>
            <span>
              <em>{{res.CommentCount}}</em>评论
            </span>
          </div>
          <span class="tag">视频</span>
        </footer>
      </div>
    </div>
</template>

<style lang="less" scoped>
	.default{
		@import url(../assets/video.less);
	    display: flex;
	    flex-direction:row;
	    .content{
	      flex:1;
	    }
	    figure{
	      margin:5px 15px 0 0;
	      width: 90px;
	      height:60px; 
	      &:after{
	        width: 30px;
	        height:30px;
	        border:1px solid #fff;
	        background-size: 10px 13px; 
	      }
	    }
	    footer{
	      margin-top:5px;
	      line-height:14px;
	      overflow: hidden;
	      .total{
	        float: right;
	        color:#999;
	        font-size: 0;
	        span{
	          font-size: 12px;
	          &:first-of-type{
	            margin-right:10px;
	            &:after{
	              margin-left:10px;
	              content:"|";
	              vertical-align: top;
	              color:#E5E5E5;
	              line-height: 12px;
	            }
	          }
	          em{
	            margin-right:1px;
	            font-size: 14px;
	            color:#666
	          }
	        }
	      }
	      .tag{
	        padding:0 3px;
	        font-size: 12px;
	        color:#F86B4F;
	        display: inline-block;
	        vertical-align: top;
	        border:1px solid #F86B4F;
	        border-radius: 2px;
	      }
	    }
	  } 
</style>

<script>
  export default {
    props:['res']
  }
</script>