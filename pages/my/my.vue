<template>
	<view class="d-flex flex-column bg-light-secondary" style="height: 100%;">
		<view class="d-flex py-3 pl-2" style="height: 180upx;background-color: #ff3815;padding-top: 120upx;">
			<image class="rounded-circle border-light" style="width: 120upx;height: 120upx;" :src="userinfo.pic" mode="aspectFit"></image>
			<view class="d-flex flex-column j-center ml-1 text-white" style="height: 126upx;">
				<text>{{ userinfo.nickname }}</text>
				<text>虽然没赚到钱，没事儿常来转转</text>
			</view>
		</view>
		
		<view class="position-relative d-flex a-center bg-white pt-1 pb-2" style="width: 680upx;height: 100upx;top:-46upx;left:35upx;border-radius: 16upx;">
			<view class="flex-1 d-flex flex-column j-center text-center">
				<text class="font-lg">0</text>
				<text class="font-sm line-h-sm">我发布的</text>
			</view>
			<view class="flex-1 d-flex flex-column j-center text-center">
				<text class="font-lg">0</text>
				<text class="font-sm line-h-sm">我收藏的</text>
			</view>
			<view class="flex-1 d-flex flex-column j-center text-center">
				<text class="font-lg">0</text>
				<text class="font-sm line-h-sm">我点赞的</text>
			</view>
		</view>
		
		<view class="d-flex flex-column m-2 px-3 py-1 bg-white position-relative" style="border-radius: 16upx;top:-44upx;">
			<view class="d-flex j-sb py-2">
				<text>联系方式</text>
				<view class="iconfont icon-you text-light-muted"></view>
			</view>
			<view class="d-flex j-sb py-2">
				<text>定位信息</text>
				<view class="iconfont icon-you text-light-muted"></view>
			</view>
			<view class="d-flex j-sb py-2">
				<text>意见反馈</text>
				<view class="iconfont icon-you text-light-muted"></view>
			</view>
			<view class="d-flex j-sb py-2">
				<text>设置</text>
				<view class="iconfont icon-you text-light-muted"></view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			userinfo: {
				nickname: '王小姐',
				pic: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1588241410842&di=77dd7182be7ec1b0176e577898f549b0&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201509%2F22%2F20150922180033_hV43u.jpeg',
				sex: 0,
				salenum: 5
			}
		}
	},
	methods: {
		
	}
}
</script>

<style>

</style>
