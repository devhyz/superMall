<template>
 <div class="recommemd">
 	<div v-for="(item,index) in recommends" :key='index' class='recommend-item'>
 		<a :href="item.link">
 			<img :src="item.image"/>
 			<div >{{item.title}}</div>
 		</a>
 	</div>
 </div>
</template>

<script>
export default {
  name: 'RecommendView',
  data () {
    return {
      msg: ''
    }
  },
  props:{
  	recommends: {
      type: Array,
      default() {
          return []
        }
    }
  }
}
</script>

<style scoped>
	.recommemd {
		display: flex;
		width: 100%;
		text-align: center;
		border-bottom: 10px solid #eee;
		border-top: 10px solid #eee;
		font-size: 12px;
	}
	.recommemd .recommend-item {
		flex: 1;
	}
	.recommend-item img {
		width: 65px;
		height: 65px;
		margin: 3px 0 4px;
	}
</style>
