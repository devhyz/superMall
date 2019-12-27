<template>
 <div class="home">
  <nav-bar class = 'home-nav'><div slot = 'center'>购物街</div></nav-bar>
    <tab-control :titles = "['流行','新款','经典']" 
  	class='tab-control1'
  	 @tabClick = 'tabClick'
  	 ref = 'tabcontrol1'
  	 v-show = 'istabcontrolFixe'
  	 ></tab-control>
  <scroll class = 'bscroll' 
  	ref = 'scroll' 
  	:probeType='3'
  	 @scroll='contentScroll'
  	 @pullingUp='loadMore'
  	 :pullUpLoad= 'true'>
  <home-swiper :banners ='banners'
  	 class = 'home-swiper' 
  	 @swiperImgLoad = 'swiperImgLoad'
  	 ></home-swiper>
  <recommend-view :recommends='recommends'></recommend-view>
  <feature-view></feature-view>
  <tab-control :titles = "['流行','新款','经典']" 
  	class='tab-control'
  	 @tabClick = 'tabClick'
  	 ref = 'tabcontrol2'
  	 ></tab-control>
  <good-list :lists = 'showGoods'></good-list>
  </scroll>
  <back-top @click.native = 'backTopClick' v-show = 'backFlag'></back-top>
 </div>
</template>

<script>
	import NavBar from 'components/common/navbar/NavBar'
	import TabControl from 'components/content/tabControl/TabControl'
	import Scroll from 'components/common/scroll/Scroll'
	
	
	import HomeSwiper from 'views/home/childComps/HomeSwiper'
	import RecommendView from 'views/home/childComps/RecommendView'
	import FeatureView from "views/home/childComps/FeatureView"
	import GoodList from 'components/content/good/GoodList'
	import BackTop from 'components/content/backTop/BackTop'
	
	
	
	import {getMuiltMessage,getHomeGoods} from 'network/home'
	
	
	
  export default {
    name: "Home",
    components:{
    	NavBar,
    	HomeSwiper,
    	RecommendView,
    	FeatureView,
    	TabControl,
    	GoodList,
    	Scroll,
    	BackTop
    	
    },
    data() {
    	return{
    		banners:[],
    		recommends:[],
    		goods:{
    			'pop':{page:0,list:[]},
    			'new':{page:0,list:[]},
    			'sell':{page:0,list:[]},
    		},
    		currentType:'pop',
    		backFlag:false,
    		tabOffsetTop:0,
    		istabcontrolFixe:false
    	}
    },
    methods:{
    	/**
    	 * 事件监听
    	 */
    	tabClick(index) {
    		switch (index){
    			case 0:
    				this.currentType = 'pop'
    				break;
    			case 1:
    			this.currentType = 'new'
    				break;
   			    case 2:
   			    this.currentType = 'sell'
    				break;
    			default:
    				break;
    		}
    		
    		this.$refs.tabcontrol1.current = index
    		this.$refs.tabcontrol2.current = index
    	},
    	backTopClick() {
    		this.$refs.scroll.scrollTop(0,0,500)
    	},
    	
    	contentScroll(position) {
    		//判断backTop是否显示
    		if (position.y < -1000) {
    			this.backFlag = true
    		} else{
    			this.backFlag = false
    		}
    		
    		//判断tabcontrol是否吸顶------position是一个对象
    		if (this.tabOffsetTop > 0&&(-position.y) > this.tabOffsetTop) {
    		this.istabcontrolFixe = true
    		}else{
    			this.istabcontrolFixe = false
    		}
    	},
    	loadMore() {
    		this.getHomeGoods(this.currentType)
    		this.$refs.scroll.scroll.refresh()
    	},
    	swiperImgLoad() {
    		this.tabOffsetTop = this.$refs.tabcontrol2.$el.offsetTop +44
    	},
    	/**
    	 * 网络请求
    	 */
    	getMuiltMessage() {
    	getMuiltMessage().then(res =>{
    		this.banners = res.data.banner.list
    		this.recommends = res.data.recommend.list
    	})
    	},
    	getHomeGoods(type) {
    	var page = this.goods[type].page + 1
    	getHomeGoods(type,page).then(res =>{
    		this.goods[type].list.push(...res.data.list)
    		this.goods[type].page+=1
    		
    		this.$refs.scroll.finishPullupLoad()
    	})
    	}
    },
    computed:{
    	showGoods() {
    		return this.goods[this.currentType].list
    	}
    },
    created() {
		this.getMuiltMessage()
		this.getHomeGoods('pop')
		this.getHomeGoods('new')
		this.getHomeGoods('sell')
    },
    mounted() {
    }
  }
</script>

<style scoped>
	.home{
		height: calc(100vh - 93px);
		position: relative;
	}
	.home-nav{
		background-color: var(--color-tint);
		color: #fff;
		border-bottom: 1px solid #eee;
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1000;
	}
	.home-swiper{
		margin-top: 44px;
	}
	.tab-control1{
		position: relative;
		top: 42px;
		border-top: 0px solid #eee;
		margin-top: 1px;
	}
	.bscroll {
		position: absolute;
		top: 44px;
		bottom: 49px;
	}

</style>
