<template>
	<view @tap="openGoodsDetail(item.id)" class="row p-2 border-bottom border-light-secondary animated fadeIn faster">
		<view class="span-6">
			<image :src="item.titlepic" mode="widthFix" class="w-100"></image>
		</view>
		<view class="span-14 pl-3 d-flex flex-column">
			<view class="font-md font-weight line-h-md">{{ item.title }}</view>
			<view class="font text-light-muted line-h-md mb-auto">{{ item.desc }}</view>
			<price>{{ item.pprice }}</price>
			<view class="font-sm text-light-muted d-flex flex-row j-sb">
				<text>{{ item.comment_num }} 条评论</text>
				<text>{{ item.post_time }}</text>
			</view>
		</view>
	</view>
</template>

<script>
	import price from '@/components/common/price.vue'
	
	export default {
		components: {
			price
		},
		props: {
			item: Object,
			index: Number
		},
		methods: {
			openGoodsDetail: function(id) {
				uni.navigateTo({
					url: "/pages/goods-info/goods-info?id=" + id
				})
			}
		}
	}
</script>

<style>
</style>
