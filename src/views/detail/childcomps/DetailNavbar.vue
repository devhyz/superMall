<template>
 <div class="detailnavbar">
 	<nav-bar>
 	<div class="back" slot = 'left' @click="backClick">
 		<img src="~assets/img/common/back.svg" alt="">
 	</div>	
 	<div slot = 'center' class="items">
 		<div v-for="(item,index) in title"
 			 class="item"
 			 @click="itemClick(index)"
 			 :class="{active:index == currentIndex}"
 			 >
 			 {{item}}
 		</div>
 	</div>
 	</nav-bar>
 </div>
</template>

<script>
	import NavBar from 'components/common/navbar/NavBar' 
export default {
  name: 'DetailNavbar',
  components:{
  	NavBar
  },
  data () {
    return {
      title: ['商品','参数','评论','推荐'],
      currentIndex:0
    }
  },
  methods:{
  	itemClick(index) {
  		this.currentIndex = index
  	},
  	backClick() {
  		this.$router.back()
  	}
  }
}
</script>
<style scoped>
.items{
	display: flex;
	font-size: 13px;
}
.items .item{
	flex: 1;
}
.active{
	color: red;
}
.back{
	margin-top: 5px;
}
</style>
