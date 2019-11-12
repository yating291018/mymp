<template>
	<view class="content">
		<view class="swiperContainer">
			<swiper display-multiple-items='1' circular @change="currentchange">
				<block v-for="(item, index) in imgUrls" :key='index'>
					<swiper-item>
						<image :src='item' class="image"></image>
					</swiper-item>
				</block>
			</swiper>
			<view class="indicatorDots">
				<view class="item" :class="{itemSelected: current === 0}">1</view>
				<view class="item" :class="{itemSelected: current === 1}">2</view>
				<view class="item" :class="{itemSelected: current === 2}">3</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imgUrls: [
					'https://ss0.baidu.com/73t1bjeh1BF3odCf/it/u=2207070506,3504082286&fm=85&s=3462B60DB4B06B2E7798AAE30300B097',
					'https://ss0.baidu.com/73t1bjeh1BF3odCf/it/u=2207070506,3504082286&fm=85&s=3462B60DB4B06B2E7798AAE30300B097',
					'https://ss0.baidu.com/73t1bjeh1BF3odCf/it/u=2207070506,3504082286&fm=85&s=3462B60DB4B06B2E7798AAE30300B097'
				],
				current: 0
			}
		},
		onLoad() {

		},
		methods: {
			currentchange (e) {
				console.log(e.detail)
				let { current } = e.detail
				this.current = current
			}
		}
	}
</script>

<style lang="scss" scoped>
.swiperContainer {
	height: 400upx;
	position: relative;
	swiper {
		height: 100%;
	}
	.image {
		width: 100%;
		height: 100%;
	}
	.indicatorDots {
		position: absolute;
		bottom: 10px;
		left: 50%;
		transform: translateX(-50%);
		display: flex;
		.item {
			width: 40upx;
			height: 40upx;
			border-radius: 2px;
			text-align: center;
			line-height: 40upx;
			background: #fff;
			margin: 0 5px;
		}
		.itemSelected {
			transition: all .3s;
			background: #000;
			color: #fff;
		}
	}
}
</style>
