<template>
	<view class="content d-flex flex-column">
		<view class="w-100 d-flex flex-row position-fixed top-0 bg-white py-1" style="z-index: 1000;">
			<view class="search-input border mx-2 text-light-muted d-flex flex-row" @tap="toSearch">
				<text class="iconfont icon-sousuo mx-2"></text>
			    <text>吉他 / 尤克里里 / 小提琴</text>
			</view>
		</view>
		<view :style="'height: 90rpx;background: white;'"></view>
		
		<divider></divider>
		<view class="adv-container w-100">
			<three-adv :resdata="advData"></three-adv>
		</view>
		<divider></divider>
		
		<view class="goods-list w-100">
			<waterfall :list="goodsList"></waterfall>
		</view>
		
		
		<view :style="'height: 50px;background: white;'"></view>
	</view>
</template>

<script>
	import threeAdv from '@/components/common/three-adv.vue';
	import waterfall from '@/components/common/xi-waterfall/xi-waterfall.vue';
	
	export default {
		components: {
			threeAdv,
			waterfall
		},
		data() {
			return {
				title: '',
				goodsList: [],
				
				
				advData: [
					{
						id: 1,
						src: "/static/fake/index/ti.jpg",
						link: ""
					},
					{
						id: 1,
						src: "/static/fake/index/piano.jpg",
						link: ""
					},
					{
						id: 1,
						src: "/static/fake/index/ele.jpg",
						link: ""
					}
				],
				fakeGoodsData: [
					{
						id: 1,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 2,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ele.jpg",
						cover: "/static/fake/index/ele.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 3,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/piano.jpg",
						cover: "/static/fake/index/piano.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 4,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 5,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ele.jpg",
						cover: "/static/fake/index/ele.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 6,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 7,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 8,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 9,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 1,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/piano.jpg",
						cover: "/static/fake/index/piano.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 2,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/piano.jpg",
						cover: "/static/fake/index/piano.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 3,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 4,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 5,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 6,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ele.jpg",
						cover: "/static/fake/index/ele.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 7,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 8,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 9,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/index/ti.jpg",
						cover: "/static/fake/index/ti.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
				]
			}
		},
		onLoad() {
			this.$nextTick(() => {
				this.goodsList = this.fakeGoodsData
			})
		},
		onReachBottom() {
			this.goodsList = this.goodsList.concat(this.fakeGoodsData)
		},
		methods: {
			toSearch: function() {
				uni.navigateTo({url: "/pages/search/search"})
			}
		}
	}
</script>

<style scoped>
	.search-input {
		width: 100%;
		height: 56rpx;
		padding-top: 6rpx;
		border-radius: 8rpx;
	}
</style>
