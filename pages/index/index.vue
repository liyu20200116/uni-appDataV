<template>
	<view class="content">
		<!-- <image class="logo" src="/static/logo.png"></image> -->
		<view class="text-area">
			<!-- <text class="title">{{title}}</text> -->
			<map :id="id" style="width:750rpx;height:1334rpx;" :markers = 'markers' @tap="tapMap"></map>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				markers: [],
				id: '2'
			}
		},
		onLoad() {
			this.getSite()
			uni.chooseLocation({
				success: function(res) {
					console.log(res, 'res')
				}
			})
		},
		methods: {
			// 获取站点
			getSite () {
				this.$api.site().then(res => {
				res.datas.forEach(item => {
					this.markers.push({
						latitude: item.positioningMsg.lat,
						longitude: item.positioningMsg.lng,
						iconPath: '/static/site.png',
						title: 'markers66'
					})
				});
				console.log(this.markers, 'this.markers')
				}).catch(res => {
				　　// 失败进行的操作
				})
			},
			tapMap(e) {
				console.log(e, 'e')
			}
		}
	}
</script>

<style>
	.content {
		/* display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center; */
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	/* .text-area {
		display: flex;
		justify-content: center;
	} */

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
