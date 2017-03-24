<template>
	<div class="shopcart">
		<div class="shopcart-left">
			<div class="cart-wrap">
				<span class="icon icon-shopping_cart"></span>
			</div>
			<div class="price-wrap">
				<span class="price-goods">￥{{goodsPrice}}</span>
				<span class="price-delivery">另需配送费￥{{deliveryPrice}}</span>
			</div>
		</div>
		<div class="shopcart-right">￥{{minPrice}}起送</div>
	</div>
</template>
<script>
	export default {
		props: {
			deliveryPrice: {
				type: Number,
				default: 0
			},
			minPrice: {
				type: Number,
				default: 1
			},
			goods: {
				type: Array,
				default: []
			}
		},
		computed: {
			goodsPrice () {
				let sum = 0
				this.goods.forEach((item) => {
					sum += item.price * item.count
				})

				return sum
			}
		}
	}
</script>
<style lang="stylus">
	@import '../../common/stylus/base.styl'
	
	$bg-dark = rgba(20, 29, 39, 1)
	$bg-light = rgba(43, 51, 59, 1)
	$font-color = rgba(255, 255, 255, .4)
	.shopcart
		position: fixed
		bottom: 0
		height: $footer-height
		width: 100%
		display: flex
		.shopcart-left, .shopcart-right
			height: 100%
			color: $font-color
			line-height: $footer-height
		.shopcart-left
			flex: 1
			background-color: $bg-dark
			position: relative
			.cart-wrap
				background-color: $bg-dark
				width: $footer-height + 8px
				height: $footer-height + 8px
				border-radius: $footer-height + 8px
				padding: 6px
				position: absolute
				top: -8px
				left: 12px
				.icon
					font-size: 24px
					line-height: 24px
					padding: 10px
					background-color: rgba(132, 139, 146, 0.26)
					display: inline-block
					width: 44px
					height: 44px
					border-radius: 44px
			.price-wrap
				position: absolute
				top: 0
				left: 80px
				.price-goods, .price-delivery
					display: inline-block
					line-height: 24px
				.price-goods
					margin-right: 12px
					padding-right: 12px
					border-right: 1px solid $font-color
		.shopcart-right
			flex: 0 0 105px
			width: 105px
			background-color: $bg-light
			text-align: center
</style>