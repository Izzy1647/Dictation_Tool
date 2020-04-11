<template>
	<view>
		<cu-custom bgColor="bg-white" :isBack="true"><block slot="backText"></block><block slot="content">答题模式</block></cu-custom>
		
		<!-- 顶部导航栏 -->
		<scroll-view scroll-x class="bg-white nav">
			<view class="flex text-center">
				<view class="cu-item flex-sub" :class="index==TabCur?'text-orange cur':''" v-for="(item,index) in topList" :key="index" @tap="tabSelect" :data-id="index">
					{{item}}
				</view>
			</view>
		</scroll-view>
		
		
		
		
		
		<!-- 底部导航栏 -->
		<view class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="jump('index')" data-cur="words">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="PageCur=='words'?'cuIcon-lightfill':'cuIcon-light'"></text>
					<!-- <image :src="'/static/tabbar/basics' + [PageCur=='basics'?'_cur':''] + '.png'"></image> -->
				</view>
				
				<view :class="PageCur=='words'?'text-gray':'text-gray'">背单词</view>
			</view>
			<view class="action" @click="jump('quiz')" data-cur="component">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="PageCur=='quiz'?'cuIcon-creativefill':'cuIcon-creative'"></text>
					<!-- <image :src="'/static/tabbar/favor' + [PageCur == 'component'?'_cur':''] + '.png'"></image> -->
				</view>
				<view :class="PageCur=='component'?'text-gray':'text-gray'">答题</view>
			</view>
			<view class="action" @click="jump('my')" data-cur="plugin">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="PageCur=='my'?'cuIcon-peoplefill':'cuIcon-people'"></text>
					<!-- <image :src="'/static/tabbar/plugin' + [PageCur == 'plugin'?'_cur':''] + '.png'"></image> -->
				</view>
				<view :class="PageCur=='plugin'?'text-gray':'text-gray'">我的</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				PageCur:'quiz',
				topList:['上传文件','手动添加'],
				TabCur:0
				
			}
		},
		
		methods: {
			jump(pageName) {
				uni.navigateTo({
				    url: `../${pageName}/${pageName}`,
				    success: res => {},
				    fail: () => {},
				    complete: () => {}
			    })
			},
			
			tabSelect(e) {   // 记录顶部导航栏
				console.log("tabSelect.e:",e)
				this.TabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60
				console.log("tabcur:",this.TabCur)
			},
			
			
		},
		
		onShow(){
			this.PageCur = 'quiz'
		}
	}
</script>

<style>

</style>
