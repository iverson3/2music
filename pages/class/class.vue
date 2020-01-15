<template>
	<view class="d-flex flex-column" style="height: 100vh;">
		<!-- #ifdef MP -->
		<!-- 顶部的自定义导航栏 -->
		<view class="w-100 d-flex a-center" style="height: 90upx;">
			<view class="flex-1 bg-light rounded d-flex a-center text-light-muted ml-2" 
			@click="openSearch" style="height: 65upx;">
				<text class="iconfont icon-sousuo mx-2"></text>
				尤克里里
			</view>
			<view style="width: 85upx;" class="d-flex a-center j-center" @click="openMessage">
				<text class="iconfont icon-xiaoxi" style="font-size: 40upx;"></text>
			</view>
		</view>
		<!-- #endif -->
		
		
		<view class="d-flex border-top border-light-secondary animated fadeIn faster" style="height: 100%; box-sizing: border-box;">
			
			<!-- <loading-plus v-if="beforeReady"></loading-plus> -->
			<!-- <loading :show="showLoading"></loading> -->
			
			<template v-if="!beforeReady && (cate.length === 0)">
				<view class="w-100 j-center a-center text-center" style="padding-top: 300upx;" @tap="reloadData">
					<text class="font-md text-light-muted">获取数据失败，请检查网络</text>
				</view>
			</template>
			
			<template v-if="!beforeReady">
				<!-- 左边 分类列表 -->
				<scroll-view id="leftScroll" scroll-y 
				:scroll-top="leftScrollTop"
				style="flex: 1;height: 100%;" 
				class="border-right border-light-secondary">
					<view v-for="(item,index) in cate" :key="index" 
					@tap="changeCate(index)"
					hover-class="bg-light-secondary"
					class="border-bottom border-light-secondary py-1 left-scroll-item">
						<view :class="activeIndex===index?'class-active':''" class="py-1 font-md text-muted text-center">{{ item.name }}</view>
					</view>
				</scroll-view>
				
				<!-- 右边 对应分类下的商品列表 -->
				<scroll-view scroll-y style="flex: 3.5;height: 100%;" 
				:scroll-with-animation="true">
					<view class="row j-sb bg-white px-1">
						<common-list v-for="(item,index) in list" :key="index" :item="item" :index="index"></common-list>
					</view>
				</scroll-view>
			</template>
			
			<view v-if="beforeReady" class="w-100 d-flex flex-column">
				<mi-skeleton
					:loading="beforeReady"
					:showTitle="true">
				</mi-skeleton>
				<mi-skeleton
					:loading="beforeReady"
					:showTitle="true">
				</mi-skeleton>
				<mi-skeleton
					:loading="beforeReady"
					:showTitle="true">
				</mi-skeleton>
				<mi-skeleton
					:loading="beforeReady"
					:showTitle="true">
				</mi-skeleton>
			</view>
			
		</view>
	</view>
</template>

<script>
	import loading from '@/common/mixin/loading.js';
	import miSkeleton from '@/components/common/skeleton/mi-skeleton.vue'
	import commonList from '@/components/common/common-list.vue'
	
	export default {
		mixins: [loading],
		components: {
			miSkeleton,
			commonList
		},
		data() {
			return {
				activeIndex: 0,
				cate: [],
				list: [],
				beforeReady: true,
				
				leftScrollTop: 0,
				
				fakeCate: [
					{
						id: 1,
						name: "吉他"
					},
					{
						id: 2,
						name: "尤克里里"
					},
					{
						id: 3,
						name: "小提琴"
					},
					{
						id: 4,
						name: "钢琴"
					},
					{
						id: 5,
						name: "电子琴"
					},
					{
						id: 6,
						name: "古典吉他"
					},
					{
						id: 7,
						name: "二胡"
					},
					{
						id: 8,
						name: "卡洪鼓"
					},
					{
						id: 9,
						name: "非洲鼓"
					},
					{
						id: 10,
						name: "贝斯"
					},
					{
						id: 11,
						name: "电吉他"
					},
					{
						id: 12,
						name: "古筝"
					},
					{
						id: 13,
						name: "扬琴"
					},
					{
						id: 14,
						name: "斯卡萨"
					},
					{
						id: 15,
						name: "手风琴"
					},
					{
						id: 16,
						name: "管风琴"
					},
					{
						id: 17,
						name: "三角铁"
					},
					{
						id: 18,
						name: "架子鼓"
					},
					{
						id: 19,
						name: "大提琴"
					},
				],
				
				fakeData: [
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 3,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
					{
						id: 3,
						title: "99新的古典吉他 雅马哈吉他 现在亏本出 可小刀",
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
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
						titlepic: "/static/fake/search/uku.jpg",
						cover: "/static/fake/search/uku.jpg",
						desc: "描述信息",
						pprice: 1000,
						comment_num: 10,
						post_time: "2019-08-12"
					},
				]
			}
		},
		watch: {
			
		},
		// 监听导航栏searchinput搜索框点击事件
		onNavigationBarSearchInputClicked: function() {
			uni.navigateTo({
				url: '/pages/search/search'
			})
		},
		onNavigationBarButtonTap: function(e) {
			if (e.index === 0) {
				uni.navigateTo({
					url: "/pages/msg-list/msg-list"
				})
			}
		},
		onLoad: function() {
			// #ifdef MP
			this.customNavBarH = 45
			// #endif
			
			this.getData()
		},
		onReady: function() {
			
		},
		methods: {
			// 分类数据加载失败的情况下 用户点击页面再次尝试请求并加载数据
			reloadData: function() {
				this.beforeReady = true
				this.getData()
			},
			
			getData() {
				this.cate = this.fakeCate
				this.list = this.fakeData
				return
				
				this.$api.get('/category/app_category').then(res => {
					let cate = []
					let list = []
					res.forEach(v => {
						cate.push({
							id: v.id,
							name: v.name
						})
						list.push({
							list: v.app_category_items
						})
					})
					this.cate = cate
					this.list = list
					
					this.beforeReady = false
					
					// 将回调函数延迟到下次DOM更新循环之后执行
					this.$nextTick(() => {
						// this.getAllDomInfo()
					})
				}).catch(err => {
					this.beforeReady = false
				})
			},
			
			// 左边分类点击事件
			changeCate: function(index) {
				this.activeIndex = index
			},

			openDetail: function(id) {
				uni.navigateTo({
					url: '/pages/detail/detail?goods_id=' + id
				});
			},
			openMessage: function() {
				uni.navigateTo({
					url: "/pages/msg-list/msg-list"
				})
			},
			openSearch: function() {
				uni.navigateTo({
					url: '/pages/search/search'
				})
			}
		}
	}
</script>

<style>
.class-active {
	border-left: 8upx solid #FD6801;
	color: #FD6801!important;
}
</style>
