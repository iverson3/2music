<template>
	<view class="container">
		<!-- 第一列 -->
		<view class="column" id="columnFirst">
			<view class="item item-left" v-for="(item, index) in columnFirst" :key="index">
				<view style="width: 356upx;" @tap="$emit('click', item)">
					<image :src="item.cover" mode="widthFix" lazy-load></image>
					<view class="p-2 pt-1">
						<view class="font-md line-h-sm">{{ item.title }}</view>
						<text class="d-block font text-light-muted">{{ item.desc }}</text>
						<view class="d-flex my-1">
							<price>{{ item.pprice }}</price>
							<view class="font-sm text-light-muted ml-1 a-self-end line-h">{{ item.post_time }}</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 第二列 -->
		<view class="column" id="columnSecond">
			<view class="item" v-for="(item, index) in columnSecond" :key="index">
				<view style="width: 364upx;" @tap="$emit('click', item)">
					<image :src="item.cover" mode="widthFix" lazy-load></image>
					<view class="p-2 pt-1">
						<view class="font-md line-h-sm">{{ item.title }}</view>
						<text class="d-block font text-light-muted">{{ item.desc }}</text>
						<view class="d-flex my-1">
							<price>{{ item.pprice }}</price>
							<view class="font-sm text-light-muted ml-1 a-self-end line-h">{{ item.post_time }}</view>
						</view>
					</view>
				</view>
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
		list: {
			type: Array,
			default: function() {
				return [];
			}
		}
	},
	data() {
		return {
			tempArray: [],
			columnFirst: [],
			columnSecond: [],
			columnFirstHeight: 0,
			columnSecondHeight: 0,
			switchInsert: true
		};
	},
	methods: {
		// 获取dom元素的高度
		async getDomHeight(selector) {
			return new Promise(resolve => {
				let query = uni.createSelectorQuery().in(this);
				query
					.select(selector)
					.fields(
						{
							size: true
						},
						data => {
							resolve(data.height);
						}
					)
					.exec();
			});
		},
		//新增数据
		async insert() {
			//只有数组内有数据才执行
			if (this.tempArray.length > 0) {
				this.switchInsert = false;
				//获取每一列的高度
				let columnFirstHeight = await this.getDomHeight('#columnFirst');
				let columnSecondHeight = await this.getDomHeight('#columnSecond');
				//获取加入的数据
				let data = this.tempArray.splice(0, 1);
				if (columnFirstHeight == columnSecondHeight || columnFirstHeight < columnSecondHeight) {
					//当高度相对,或第一列小于其他列,数据加入到第一列
					this.columnFirst.push(data[0]);
				} else {
					//数据加入到第二列
					this.columnSecond.push(data[0]);
				}
				this.$nextTick(() => {
					//当数据渲染完毕后,可以进行添加,知道临时数据被添加完毕
					this.insert();
				});
			} else {
				this.switchInsert = true;
			}
		},
		//清除数组
		clear() {
			this.columnFirst = [];
			this.columnSecond = [];
			this.tempArray = [];
		},
		//外部调用,添加数据
		insertData(data) {
			this.tempArray = this.tempArray.concat(data);
			//新增数据
			if (this.switchInsert) {
				this.insert();
			}
		}
	},
	watch: {
		list(newVal, oldVal) {
			//当监听到,数据有变化时
			if (newVal.length === 0) {
				//清空数据
				this.clear();
			} else if (newVal.length > 0) {
				//赋值给临时数组
				this.tempArray = this.tempArray.concat(newVal.slice(oldVal.length));
				//新增数据
				if (this.switchInsert) {
					this.insert();
				}
			}
		}
	},
	computed: {
		currentLength() {
			return this.columnFirst.length + this.columnSecond.length;
		}
	}
};
</script>

<style>
.container {
	width: 100%;
	display: flex;
	align-items: flex-start;
	/* margin-left: 10upx; */
	background-color: whitesmoke;
}
.container .column {
	flex: 1;
}
.container .column .item image {
	width: 100%;
}
.item {
	background-color: white;
	margin-bottom: 20upx;
}
.item-left {
	margin-right: 20upx;
}
</style>
