<template>
    <div class="goods-body">
    	<div class="menu-wrap">
    		<ul>
    			<li v-for="item in goods">
    				<span>{{item.name}}</span>
    			</li>
    		</ul>
    	</div>
    	<div class="goods-wrap">
    		<div class="goods-box" v-for="foods_item in goods">
    			<p class="goods-title"></p>
    			<ul>
    				<li v-for="food in foods_item.foods">
    					<img :src="food.image" alt="">
    					{{food.name}}
    				</li>
    			</ul>
    		</div>
    	</div>
    </div>
</template>
<script>
	const ERR_OK = 0

	export default {
		data () {
			return {
				goods: []
			}
		},
		created () {
			this.$http.get('/api/goods').then((response) => {
				response = response.body
				if (response.errno === ERR_OK) {
					this.goods = response.data
				}
			})
		}
	}
</script>
<style lang="stylus">
	@import '../../common/stylus/mixin.styl'

	.goods-body
		display: flex
		.menu-wrap
			flex: 0 0 80px
			width: 80px
			background-color: #f3f5f7
			padding-bottom: 46px
			position: absolute
			top: 176px
			bottom: 0px
			overflow: auto
			ul
				font-size: 12px
				line-height: 14px
				color: rgb(20, 20, 20)
				width: 56px
				margin: 0 auto
				li
					height: 54px
					display: table
					width: 100%
					border-bottom-1px(rgba(7, 17, 27, 0.1))
					span
						display: table-cell
						vertical-align: middle
		.goods-wrap
			flex: 1
			padding-left: 80px
</style>