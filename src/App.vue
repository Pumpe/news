<template>
  <div id="app">
    <transition name="fade">
      <cover v-if="!newsList.length"></cover>
    </transition>
    <div class="container" @scroll="scrollHandle">
      <ul class="news-list" v-if="newsList.length" id="news_list">
        <li v-for="(item,index) in newsList">
          <article-item :res="item" v-if="item.Type == 0"></article-item> 
          <video-item :res="item" v-else-if="item.Type=7"></video-item>
        </li>
      </ul>
      <transition name="fade">
        <div class="loading" v-if="loading">
          <loading />
        </div>
      </transition>
    </div>
    <go-top @click.native="goTop" :status="gotopStatus" />
  </div>
  <!--  -->
</template>

<script>
  import axios from 'axios'
  import storage from './util/storage'
  import Cover from './components/cover'
  import ArticleItem from './components/index/article-item'
  import VideoItem from './components/index/video-item'
  import GalleryItem from './components/index/gallery-item'
  import Loading from './components/loading'
  import GoTop from './components/go-top'

  export default {
    name: 'app',
    components: {
      ArticleItem,
      VideoItem,
      Cover,
      Loading,
      GoTop
    },
    data (){
      return {
        page:1,
        loading:false,
        newsList:[],
        gotopStatus:false,
        Container:null,
        List:null,
        scrollAnimation:null
      }
    },
    methods:{
      stream (){
        let that = this;
        axios.get('https://apis.360che.com/IndexRecommend/app/IndexList.aspx',{
          params: {
            page:this.page
          }
        }).then(function(res){
          that.fetch(res.data);
        }).catch(function(error){
        })
      },
      fetch (o){
        this.newsList = this.newsList.concat(o.data);
        this.page += 1;
        this.loading = false;
        let cache = {
          page:this.page - 1,
          data:this.newsList
        };
        storage.set('newsListCache',cache);
      },
      scrollHandle (e){
        if(!this.Container){
          this.Container = e.target;
          this.List = this.Container.firstElementChild 
        }
        this.toggleGoTop();
        this.loadMore();
      },
      loadMore (e){
        if(this.List.getBoundingClientRect().bottom <= this.Container.offsetHeight + 100 && !this.loading){
          this.loading = true;
          this.stream();
        }
      },
      toggleGoTop (){
        this.gotopStatus = this.Container.scrollTop >= this.Container.offsetHeight*2 ? true : false;
      },
      goTop (){
        if(!navigator.userAgent.match(/iphone/i) && this.Container.scrollTop > 500) 
        this.Container.scrollTop = 500;
        this.moving(0);
      },
      moving (n){
        let that = this;
        if(this.Container.scrollTop == n){
            this.scrollAnimation && cancelAnimationFrame(this.scrollAnimation);  
            return;
        }else{
            var speed = (n - this.Container.scrollTop)/8;
            speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
            this.Container.scrollTop = this.Container.scrollTop + speed;
            this.scrollAnimation = requestAnimationFrame(function(){
                that.moving(n);
            });   
        }
      },
      rePosition (){
        let p = storage.get('position');
        if(p){
          this.$el.firstElementChild.scrollTop = p
          storage.remove('position');
        }
      }
    },
    created(){
      let cache = storage.get('newsListCache');
      if(!cache){
        this.stream();
      }else{
        cache = JSON.parse(cache);
        this.page = cache.page;
        this.fetch(cache); 
      }
    },
    mounted(){
      this.rePosition();  
    }
  }
</script>

<style lang="less" scoped>
  .news-list{
    padding-left:15px;
    overflow: auto;
  }
  .loading{
    overflow: hidden;
    background: #f9f9f9
  }
</style>
