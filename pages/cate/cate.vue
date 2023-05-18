<template>
	<view>
		<view class="scroll-view-container">
			<scroll-view class="left-cate" scroll-y="true" :style="{height: vh + 'px'}">
				<view class="aside-item" v-for="(item, index) in AsideList" :key="index">
					{{item.name}}
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				vh: 0,
				AsideList: []
			}
		},
		onLoad() {
			this.vh = uni.getSystemInfoSync().windowHeight 
			this.getAsideList()
		},
		methods: {
			async getAsideList() {
				const { data: res } = await uni.$http.get('api/public/v1/categories')
				if(res.meta.status != 200) return uni.$showMsg()
				this.AsideList = res.message
			}
		}
	}
</script>

<style lang="less">
.scroll-view-container {
	display: flex;
	.left-cate {
		width: 120px;
		.aside-item {
			font-size: 12px;
			background-color: #f7f7f7;
			line-height: 60px;
			text-align: center;
			&.active {
				position: relative;
				color: #c00000;
				&::before {
					position: absolute;
					content: '|';
					top: 50%;
					left: 0;
					transform: translateY(-50%);
				}
			}
		}
	}
}
</style>
