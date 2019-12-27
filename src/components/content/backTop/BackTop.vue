<template>
  <div class="back-top">
    <img src="~assets/img/common/top.png" alt="">
  </div>
</template>

<script>
export default {
  name: 'BackTop',
  data () {
    return {
      msg: ''
    }
  }
}
</script>
<style scoped>
.back-top{
	position: fixed;
	right: 35px;
	bottom: 70px;
}
.back-top img {
	width: 43px;
	height: 43px;
}
</style>
