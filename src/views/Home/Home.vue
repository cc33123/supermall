<template>
  <div id="home" class="wrapper">
    <!--导航-->
    <nav-bar class="home-nav">
      <div slot="center">购物车</div>
    </nav-bar>

    <!--轮播图-->
    <home-swiper :banners="banners"/>
    <!--recommends,推荐信息展示-->
    <home-recommend-view :recommends="recommends"/>
    <!--特点-->
    <home-feature-view/>
    <!--选项卡-->
    <tab-control class="tab-control" :titles="['流行', '新款', '精选']"/>

    <!--商品列表-->
    <goods-list :goods="goods['pop'].list"/>
    <ul>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
      <li>列表</li>
    </ul>

  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar"
  import TabControl from "components/content/tabControl/TabControl";
  import GoodsList from "components/content/goods/GoodsList";

  import HomeSwiper from "./childComponents/HomeSwiper"
  import HomeRecommendView from "./childComponents/HomeRecommendView";
  import HomeFeatureView from "./childComponents/HomeFeatureView"

  import {getHomeMultidata,getHomeGoods} from "network/home"
  export default {
    name: "Home",
    components: {
      HomeFeatureView,
      NavBar,
      HomeSwiper,
      HomeRecommendView,
      TabControl,
      getHomeGoods,
      GoodsList
    },
    data(){
      return {
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page: 0,list:[]},
          'sell':{page:0,list:[]}
        }
      }
    },
    created() {
      //请求多个数据
      this.getHomeMultidata()

      //请求商品数据 流行
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods:{
      // 请求多个数据
      getHomeMultidata(){
        let t = this
        getHomeMultidata().then(res =>{
          t.banners = res.data.banner.list
          t.recommends = res.data.recommend.list
        })
      },
      // 请求商品数据
      getHomeGoods(type){
        let t = this
        let page = t.goods[type].page + 1
        getHomeGoods(type,page).then(res =>{
          //取出列表
          t.goods[type].list.push(...res.data.list)
          //取出页码
          t.goods[type].page += 1

          console.log(t.goods)
        })
      }
    }

  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
    /*height: 100vh;*/
    /*position: relative;*/
  }

  .home-nav{
    background-color: var(--color-tint);
    color: #ffffff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9;
  }

  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
