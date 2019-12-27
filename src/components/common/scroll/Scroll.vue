<template>
 <div class="wrapper" ref = 'wrapper'>
 	<div class="content">
 		<slot></slot>
 	</div>
 </div>
</template>

<script>
	import BScroll from 'better-scroll'
export default {
  name: 'Scroll',
  data () {
    return {
      scroll: null,
      message:'meg'
    }
  },
  props:{
  	probeType:{
  		type:Number,
  		default:	0
  	},
  	pullUpLoad:{
  		type:Boolean,
  		default:false
  	}
  },
  mounted() {
  	this.scroll = new BScroll(this.$refs.wrapper,{
  		click:true,
  		probeType:this.probeType,
  		pullUpLoad:this.pullUpLoad
  	})
  	this.scroll.on('scroll',(position) =>{
  		this.$emit("scroll",position)
  	})
  	this.scroll.on('pullingUp',() =>{
  		this.$emit("pullingUp")
  	})
  },
  methods:{
  	scrollTop(x,y,time) {
  		this.scroll.scrollTo(x,y,time)
  	},
  	finishPullupLoad() {
  		this.scroll.finishPullUp()
  	}
  }
}
</script>
<style scoped>

</style>
