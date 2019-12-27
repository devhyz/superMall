<template>
 <div class="goods">
 	<good-list-item v-for = "(item,index) in lists" :list = 'item' :key = 'index'></good-list-item>
 </div>
</template>

<script>
	import GoodListItem from 'components/content/good/GoodListItem'
export default {
  name: 'GoodList',
  data () {
    return {
      msg: ''
    }
  },
  components:{
  	GoodListItem
  },
  props:{
  	lists:{
  		type:Array,
  		default() {
  			return []
  		}
  	}
  }
}
</script>
<style scoped>
.goods{
	display: flex;
	flex-wrap: wrap;
	justify-content: space-around;
}
</style>
