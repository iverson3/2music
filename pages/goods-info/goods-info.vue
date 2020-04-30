<template>
	<view>
		<view class="d-flex j-sb mx-2 my-3">
			<view class="d-flex">
				<price priceSize="font-lg" unitSize="font-md">{{ info.price }}</price>
				<view class="font-sm text-light-muted line-through ml-1 a-self-end line-h">￥{{ info.oprice }}</view>
			</view>
			
			<text class="wants-views text-light-muted">{{ info.wants }}人想要 | {{ info.views }}人看过</text>
		</view>
		<view class="m-2 d-flex flex-column">
			<text>{{ info.content }}</text>
			<view class="d-flex flex-column mt-2">
				<template v-for="(item,index) in info.images">
					<image @tap="previewImageList(index)" class="mb" :key="index" :src="item" mode="widthFix"></image>
				</template>
			</view>
		</view>
		
		<divider></divider>
		<view class="user-info d-flex mx-2 py-2">
			<view class="d-flex flex-column" style="flex: 4;">
				<view class="d-flex">
					<view class="mr-3 font-md">{{ info.userinfo.nickname }}</view>
					<view><text class="iconfont icon-dingwei"></text><text>{{ info.city }}</text></view>
				</view>
				<view>该用户共有{{ info.userinfo.salenum }}个乐器在卖</view>
			</view>
			<view class="flex-1">
				<image class="rounded" style="height: 100upx;" :src="info.userinfo.pic" mode="aspectFit"></image>
			</view>
		</view>
		
		<divider></divider>
		<view class="comment-list d-flex flex-column">
			<view class="border-bottom border-light-secondary p-2 font-weight">全部留言 ({{ info.comments.length }})</view>
			<view class="d-flex flex-column px-2">
				<view class="d-flex flex-column mt-2 pb-2 border-bottom border-light-secondary" v-for="(item,index) in info.comments" :key="index">
					<view class="text-dark">{{ item.nickname }} <text class="text-light-muted font-sm ml-2">{{ item.ctime }}</text></view>
					<view>{{ item.content }}</view>
				</view>
			</view>
		</view>
		
		<divider></divider>
		<view class="my-2">
			<view class="position-relative d-flex j-center a-center text-secondary pb-5 pt-3 bg-white">
				<view class="px-2 position-absolute" style="background: white;z-index: 2;">猜你喜欢</view>
				<view class="position-absolute" style="background: #DDDDDD;height: 1upx;left: 0;right: 0;"></view>
			</view>
			<!-- 列表 -->
			<view class="row j-sb bg-white">
				<common-list-full v-for="(item,index) in info.hotList" :key="index" :item="item" :index="index"></common-list-full>
			</view>
		</view>
		
		<common-popup :popupClass="popup.contact" :popupHeight="500" @hide="hidePopup('contact')">
			<view class="d-flex a-center j-center font-md border-bottom border-light-secondary" style="height: 100upx;">
				卖家联系方式
			</view>
			 
			<!-- 服务说明列表 h300 -->
			<scroll-view scroll-y class="w-100" style="height: 300upx;">
			 	<view class="py-1">
			 		<view class="d-flex a-center">
						<view class="iconfont icon-finish main-text-color mr-1"></view>
						电话
					</view>
					<view class="text-light-muted font pl-4">{{ info.phone }}</view>
			 	</view>
				<view class="py-1">
					<view class="d-flex a-center">
						<view class="iconfont icon-finish main-text-color mr-1"></view>
						微信
					</view>
					<view class="text-light-muted font pl-4">{{ info.wechat }}</view>
				</view>
			</scroll-view>
			 
			<!-- 按钮 h100 -->
			<view class="main-bg-color text-white font-md d-flex j-center a-center"
			hover-class="main-bg-hover-color"
			@tap.stop="hidePopup('contact')"
			style="height: 100upx;margin-left: -30upx;margin-right: -30upx;">
				确定
			</view>
		</common-popup>
		
		
		<!-- 占位 -->
		<view class="bg-white" style="height: 100upx;"></view>
		<view class="position-fixed bottom-0 left-0 right-0 d-flex j-sb bg-white border-top border-light-secondary px-2" style="height: 100upx;">
			<view class="d-flex">
				<view class="d-flex flex-column mt-1 mr-4">
					<view class="iconfont icon-dianzan font-md text-light-muted line-h pl-1"></view>
					<text class="font-sm">超赞</text>
				</view>
				<view class="d-flex flex-column mt-1 mr-4">
					<view class="iconfont icon-shoucang font-md text-light-muted line-h pl-1"></view>
					<text class="font-sm">收藏</text>
				</view>
				<view class="d-flex flex-column mt-1">
					<view class="iconfont icon-pinglun font-md text-light-muted line-h pl-1"></view>
					<text class="font-sm">评论</text>
				</view>
			</view>
			<view @tap="showPopup('contact')" class="d-flex flex-column j-center p-1 button-contact">
				查看联系方式
			</view>
		</view>
	</view>
</template>

<script>
import price from '@/components/common/price.vue'
import commonPopup from '@/components/common/common-popup.vue'
import commonListFull from '@/components/common/common-list-full.vue'

export default {
	components: {
		price,
		commonPopup,
		commonListFull
	},
	data() {
		return {
			goodsid: 0,
			info: {
				content: '99新的古典吉他 雅马哈吉他 现在亏本出 可小刀\n有琴包 非常厚实\n寻找有缘人',
				images: ['https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=50023082,2349397126&fm=15&gp=0.jpg', 'https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1788858818,2309021488&fm=15&gp=0.jpg'],
				price: 126,
				oprice: 255,
				city: '深圳',
				over_freight: true,
				type: 2,
				tags: '全新,可小刀,仅自提',
				wants: 5,
				views: 103,
				
				userinfo: {
					nickname: '王小姐',
					pic: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1588241410842&di=77dd7182be7ec1b0176e577898f549b0&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201509%2F22%2F20150922180033_hV43u.jpeg',
					sex: 0,
					salenum: 5
				},
				
				comments: [
					{
						nickname: '张三',
						content: '不错哦 这琴挺好的，赞',
						ctime: '2020-03-18'
					},
					{
						nickname: '李四',
						content: '不错哦 这琴挺好的，赞',
						ctime: '2020-03-10'
					}
				],
				like: false,
				collection: false,
				
				hotList: [
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
					}
				],
				
				phone: '13396095889',
				wechat: 'xxxxxxxxx',
				qq: '252556310'
			},
			
			popup: {
				contact: "none"
			},
		}
	},
	onLoad: function(e) {
		if (e.id) {
			this.goodsid = e.id
			console.log(this.goodsid)
		}
	},
	methods: {
		showPopup: function(key) {
			this.popup[key] = "show"
		},
		hidePopup: function(key) {
			this.popup[key] = "hide"
			setTimeout(() => {
				this.popup[key] = "none"
			}, 200)
		},
		previewImageList: function(index) {
			uni.previewImage({
				urls: this.info.images,
				current: index
			})
		}
	}
}
</script>

<style>
.wants-views {
	font-size: 20upx;
}
.button-contact {
	margin: 16upx 0;
	border-radius: 36upx;
	padding: 0px 30upx;
	background-color: #ff3815;
	color: white;
}
</style>
