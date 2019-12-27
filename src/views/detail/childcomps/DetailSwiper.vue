<template>
	<div class="swiper">
 	<swiper class = 'detail-swiper1'>
 		<swiperItem v-for ='(item,index) in topImages' :key='index'>
 			<a >
 				<img :src="item"/>
 			</a>
 		</swiperItem>
 	</swiper>
	</div>
</template>

<script>
	import {Swiper,SwiperItem} from 'components/common/swiper'
export default {
  name: 'DetailSwiper',
  components:{
  	Swiper,
  	SwiperItem
  },
  data () {
    return {
      msg: ''
    }
  },
  props:{
  	topImages:{
  		type:Array,
  		default(){
  			return []
  		}
  	}
  }
}
</script>
<style scoped>
.detail-swiper1{
	height: 300px;
	overflow: hidden;
}
</style>
