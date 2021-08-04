<template>
	<view class="content">
		<view>
			<view id="svgContainer"></view>
		</view>
		<button class="btn" type="default" @click="test.startLottie">开始</button>
		<button class="btn" type="primary" @click="test.pauseLottie">暂停</button>
		<button class="btn" type="warn" @click="test.stopLottie">结束</button>
		<button class="btn" type="primary" @click="test.speed">加快</button>
		<button class="btn" type="primary" @click="test.speedCalc">放慢</button>
		<view style="text-align: center;">{{speedNum}}</view>
	</view>
</template>
<!-- <script src="../../static/js/lottie.min.js"></script> -->
<script module="test" lang="renderjs">
	import bodymovin from "../../static/js/lottie.min.js"
	
	export default {
		data() {
			return {
				speedNum: 1,
				anim: null,
				speedNum: 1,
				data: require('../../static/pig.json')
			}
		},
		mounted() {
			console.log(bodymovin)
			var svgContainer = document.getElementById('svgContainer');
			this.anim = bodymovin.loadAnimation({
				wrapper: svgContainer,
				animType: 'canvas',
				loop: true,
				// animationData: this.data
				// path: 'https://assets4.lottiefiles.com/packages/lf20_wq58gaht.json',
				// path: 'https://assets1.lottiefiles.com/packages/lf20_rzbrd9fg.json'
				path: 'https://assets10.lottiefiles.com/packages/lf20_xiwiffnd.json'
			})
			console.log(this.anim)
		},
		methods: {
			startLottie(){
				bodymovin.play()
			},
			pauseLottie(){
				bodymovin.pause()
			},
			stopLottie(){
				this.speedNum = 0
				bodymovin.stop()
			},
			speed(){
				this.speedNum ++
				bodymovin.setSpeed(this.speedNum)
			},
			speedCalc(){
				
				if(this.speedNum > 0 ) {
					this.speedNum -- ;
					bodymovin.setSpeed(this.speedNum)
				}else {
					uni.showToast({
						title: '速度不能再低了',
						icon: 'none',
						duration: 3000
					})
				}
				
			}
		}
		
	}
</script>

<style scoped>
	.content {
		width: 500rpx;
		height: 500rpx;
		margin: 0 auto;
		/* background: #666; */
	}

	#svgContainer {
		width: 100%;
		height: 100%;
	}

	.btn {
		width: 200rpx;
		margin: 20rpx auto;
	}
</style>
