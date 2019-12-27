<template>
 <div class="detail" id="detail">
 	<detail-navbar class = 'detail-navbar'></detail-navbar>
 	<scroll class = 'content' ref = 'scroll'>
 	<detail-swiper :topImages ='topImages'></detail-swiper>
 	<detail-base-info :goods = 'goods'></detail-base-info>
 	<detail-shop-info :shop = 'shop'></detail-shop-info>
 	<detail-goods-info :detailInfo='detailInfo' @imageLoad = 'imageLoad'></detail-goods-info>
 	<detail-param-info :paramInfo = 'paramInfo'></detail-param-info>
 	<detail-comment-info :commentInfo = 'commentInfo'></detail-comment-info>
 	<good-list :lists = 'RecommendInfo'></good-list>
 	</scroll>
 </div>
</template>

<script>
	import Scroll from 'components/common/scroll/Scroll'
	
	import DetailNavbar from 'views/detail/childcomps/DetailNavbar'
	import DetailSwiper from 'views/detail/childcomps/DetailSwiper'
	import DetailBaseInfo from 'views/detail/childcomps/DetailBaseInfo'
	import DetailShopInfo from 'views/detail/childcomps/DetailShopInfo'
	import DetailGoodsInfo from 'views/detail/childcomps/DetailGoodsInfo'
	import DetailParamInfo from 'views/detail/childcomps/DetailParamInfo'
	import DetailCommentInfo from 'views/detail/childcomps/DetailCommentInfo'
	import GoodList from 'components/content/good/GoodList'
	
	import {getDetail,getRecommend,Goods,Shop,GoodsParam} from 'network/detail';
export default {
  name: 'Detail',
  components:{
  	DetailNavbar,
  	DetailSwiper,
  	DetailBaseInfo,
  	DetailShopInfo,
  	Scroll,
  	DetailGoodsInfo,
  	DetailParamInfo,
  	DetailCommentInfo,
  	GoodList
  },
  data () {
    return {
      iid: null,
      topImages:[],
      goods:{},
      shop:{},
      detailInfo:{},
      paramInfo:{},
      commentInfo:{},
      RecommendInfo:[]
    }
  },
  methods:{
  	imageLoad() {
  		this.$refs.scroll && this.$refs.scroll.scroll.refresh()
  	}
  },
  created(){
  	//1获得iid用于请求数据
  	this.iid = this.$route.params.iid
  	
  	
  	//2发送网络请求 详情数据
  	getDetail(this.iid).then(res =>{
  		console.log(res)
  		//1顶部图片数据
  		var data = res.result
  		this.topImages = data.itemInfo.topImages
  		//获取基本信息
  		this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)
  		
  		//获取商家信息
  		this.shop = new Shop(data.shopInfo)
  		//商品信息，穿戴效果
  		this.detailInfo = data.detailInfo
  		//商品参数 材质等 尺码
  		this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule)
  		//获取品论信息
  		if (data.rate.cRate!=0) {
  			this.commentInfo = data.rate.list[0]
  		}
  		
  	})
  
  	//推荐数据
    getRecommend().then(res =>{
    	console.log(res)
    	this.RecommendInfo = res.data.list
    })
  }
}
</script>
<style scoped>
#detail{
	position: relative;
	z-index: 9;
	background-color: #fff;
	height: 100vh;
}
 .detail-navbar{
	position: relative;
	z-index: 1000;
	background-color: #fff;
}
.content{
	height: calc(100% - 44px);
}
</style>
