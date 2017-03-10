<template>
    <div class="goods-body">
    	<div class="menu-wrap" ref="menuWrap">
    		<ul>
    			<li v-for="item in goods">
    				<span>{{item.name}}</span>
    			</li>
    			<li class="place-footer"></li>
    		</ul>
    	</div>
    	<div class="goods-wrap" ref="goodsWrap">
    		<ul class="goods-list">
    			<li v-for="foods_item in goods" class="goods-item">
	    			<p class="goods-title">{{foods_item.name}}</p>
	    			<ul class="foods-list">
	    				<li v-for="food in foods_item.foods" class="food-item">
	    					<img :src="food.image" class="food-img">
	    					<div class="text-info">
	    						<p class="name">{{food.name}}</p>
	    						<p class="descript" v-if="food.description">{{food.description}}</p>
	    						<p class="data">
	    							<span class="sellCount">月售{{food.sellCount}}份</span>
	    							<span class="rating">好评率{{food.rating}}%</span>
	    						</p>
	    						<p class="prices">
	    							<span class="price">￥{{food.price}}</span>
	    							<span class="oldPrice" v-if="food.oldPrice">￥{{food.oldPrice}}</span>
	    						</p>
	    					</div>
	    					<!-- <div class="add-sub-box">
	    						<span class="add icon-add_circle"></span>
	    						<span class="sub icon-remove_circle_outline"></span>
	    					</div> -->
	    				</li>
	    			</ul>
    			</li>
    			<li class="place-footer"></li>
    		</ul>
    	</div>
    </div>
</template>
<script>
	import BScroll from 'better-scroll'

	const ERR_OK = 0

	export default {
		data () {
			return {
				goods: [],
				goodsHeightList: []
			}
		},
		created () {
			this.$http.get('/api/goods').then((response) => {
				response = response.body
				if (response.errno === ERR_OK) {
					this.goods = response.data
					this.$nextTick(() => {
						this.initScroll()
					})
				}
			})
		},
		methods: {
			initScroll () {
				this.menuScroll = new BScroll(this.$refs.menuWrap)
				this.goodsScroll = new BScroll(this.$refs.goodsWrap)
				let height = 0
				let goodsDom = this.$refs.goodsWrap.getElementsByClassName('goods-item')

				this.goodsHeightList.push(height)
				for (let i = 0; i < goodsDom.length; i++) {
					height += dom.clientHeight
					this.goodsHeightList.push(height)
				}
			}
		}
	}
</script>
<style lang="stylus">
	@import '../../common/stylus/mixin.styl'
	@import '../../common/stylus/base.styl'
	
	.goods-body
		.menu-wrap
			width: 80px
			background-color: $color-silver
			position: absolute
			top: 176px
			bottom: 0px
			overflow: hidden
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
					border-bottom-1px($color-line)
					span
						display: table-cell
						vertical-align: middle
		.goods-wrap
			position: absolute
			left: 80px
			right: 0px
			top: 176px
			bottom: 0px
			overflow: hidden
			
			.goods-list
				.goods-title
					background-color: $color-silver
					font-size: 12px
					color: $color-font1
					line-height: 26px
					border-left: 2px solid #d9dde1
					padding: 0 14px
				.food-item
					display: flex
					margin: 18px 18px 0
					padding-bottom: 18px
					border-bottom: 1px solid $color-line
					&:last-child
						border-bottom: none
					.food-img
						height: 58px
						width: 58px
						flex: 0 0 58px
					.text-info
						flex: 1
						padding: 2px 0 0 10px
						width: 1px
						.name
							font-size: 14px
							line-height: 14px
							color: $color-font2
						.descript, .data
							font-size: 10px
							line-height: 12px
							color: $color-font1
							margin-top: 8px
						.descript
							white-space: nowrap
							overflow: hidden
							text-overflow: ellipsis
						.data
							.sellCount
								margin-right: 10px
						.prices
							margin-top: 8px
							line-height: 14px
							font-size: 14px
							font-weight: 700
							.price
								color: $color-red
								font-weight: inherit
								margin-right: 5px
							.oldPrice
								color: $color-font1
								text-decoration: line-through
		.place-footer
			height: $footer-height
</style>