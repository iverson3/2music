<template>
	<!-- 底部弹出框 -->
	<view class="_popup" :class="popupClass" :style="getPopupStyle">
		<view class="_mask" @tap.stop="$emit('hide')" @touchmove.stop.prevent="moveHandle"></view>
		<view class="_body" :style="getPopupStyle">
			<view class="position-absolute iconfont icon-shanchu1 rounded-circle bg-light-secondary" 
			@tap.stop="$emit('hide')"
			style="top: 24upx; right: 40upx;font-size: 16upx;padding: 6upx 12upx;"></view>
			<slot></slot>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			popupClass: {
				type: String,
				default: 'none'
			},
			popupHeight: {
				type: Number,
				default: 1035
			}
		},
		computed: {
			getPopupStyle() {
				return `height: ${this.popupHeight}upx;bottom: -${this.popupHeight}upx;`
			}
		},
		methods: {
			moveHandle: function() {
				// @touchmove.stop.prevent  解决蒙版状态下页面仍然可以滚动的问题
				// 啥也不用做   :catchtouchmove="false"
			}
		}
	}
</script>

<style scoped>
	._popup, ._mask {
		position: fixed;
		top: 0;
		width: 100%;
		height: 100%;
	}
	._popup {
		z-index: 2000;
		display: none;
	}
	._mask {
		z-index: 2002;
		background: rgba(0,0,0,0.5);
	}
	._popup ._body {
		position: fixed;
		/* 注意，这里bottom不能设置为0 要设置为跟弹出框body高度一样的负值 */
		/* bottom: -1035rpx;  */
		width: 92%;
		padding: 0 4%;
		/* height: 1035rpx; */
		border-radius: 20upx 20upx 0 0;
		background: #FFFFFF;
		z-index: 2003;
		display: flex;
		flex-direction: column;
	}
	._popup.show {  /* _popup和show这两个class是同级的关系 所以要注意写的连在一起  */
		display: block;
	}
	.show ._mask {
		animation: showPopupMask 0.2s linear both;
	}
	.show ._body {
		animation: showPopupBody 0.2s linear both;
	}
	._popup.hide {  /* _popup和hide这两个class是同级的关系 所以要注意写的连在一起  */
		display: block;
	}
	.hide ._mask {
		animation: hidePopupMask 0.2s linear both;
	}
	.hide ._body {
		animation: hidePopupBody 0.2s linear both;
	}
	._popup.none {  /* _popup和none这两个class是同级的关系 所以要注意写的连在一起  */
		display: none;
	}
	/* 定义动画效果 */
	@keyframes showPopupBody{
		0%{ transform: translateY(0); }
		100%{ transform: translateY(-100%); }
	}
	@keyframes hidePopupBody{
		0%{ transform: translateY(-100%); }
		100%{ transform: translateY(0); }
	}
	@keyframes showPopupMask{
		0%{ opacity: 0; }
		100%{ opacity: 1; }
	}
	@keyframes hidePopupMask{
		0%{ opacity: 1; }
		100%{ opacity: 0; }
	}
</style>
