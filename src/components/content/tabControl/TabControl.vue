<template>
 <div class="tab-control">
 	<div v-for="(item,index) in titles" :key = 'index' class="tab-control-item"
 		:class='{activic: index === current}' 
 		@click="tabBtn(index)"> 
 		<span >{{item}}</span>
 	</div>
 </div>
</template>

<script>
export default {
  name: 'TabControl',
  data () {
    return {
      current:0
    }
  },
  methods:{
  	tabBtn(index) {
  		this.current = index
  		this.$emit('tabClick',index)
  	}
  },
  props:{
  	titles:{
  		type:Array,
  		default() {
  			return []
  		}
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.tab-control  {
		display: flex;
		height: 40px;
		line-height: 40px;
		font-size: 15px;
		text-align: center;
		border-top: 10px solid #eee;
		background-color: #fff;
		margin-bottom: 10px;
		z-index: 10000;
	}
	.tab-control-item{
		flex: 1;
	}
	.activic{
		color: red;
		
	}
	.activic span{
		padding: -5px;
		border-bottom: 2px solid red;
	}
</style>
