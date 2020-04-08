<template>
	<view>
		<cu-custom bgColor="bg-white" :isBack="true"><block slot="backText"></block><block slot="content">背单词</block></cu-custom>
		
		<!-- 顶部导航栏 -->
		<scroll-view scroll-x class="bg-white nav">
			<view class="flex text-center">
				<view class="cu-item flex-sub" :class="index==TabCur?'text-orange cur':''" v-for="(item,index) in topList" :key="index" @tap="tabSelect" :data-id="index">
					{{item}}
				</view>
			</view>
		</scroll-view>
		
		<view class='padding margin text-center'>
			<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="startDictation" data-target="viewModal">
				开始听写
			</view>
		</view>
		

		
		<!-- 底部导航栏 -->
		<view class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="NavChange" data-cur="words">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="PageCur=='words'?'cuIcon-lightfill':'cuIcon-light'"></text>
					<!-- <image :src="'/static/tabbar/basics' + [PageCur=='basics'?'_cur':''] + '.png'"></image> -->
				</view>
				
				<view :class="PageCur=='words'?'text-gray':'text-gray'">背单词</view>
			</view>
			<view class="action" @click="NavChange" data-cur="component">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="'cuIcon-read'"></text>
					<!-- <image :src="'/static/tabbar/favor' + [PageCur == 'component'?'_cur':''] + '.png'"></image> -->
				</view>
				<view :class="PageCur=='component'?'text-gray':'text-gray'">答题</view>
			</view>
			<view class="action" @click="NavChange" data-cur="plugin">
				<view class='cuIcon-cu-image'>
					<text class="lg text-gray" :class="PageCur=='plugin'?'cuIcon-peoplefill':'cuIcon-people'"></text>
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
				topList: ['预设模版','自定义'],
				TabCur: 0,   // 顶部导航栏选中的那一项
				PageCur: 'words'
				
			}
		},
		methods: {
			tabSelect(){
				console.log("tab select")
			},
			startDictation(){
				console.log("start dictation")
			}
		},
		onShow(){
			console.log("Onshow")
			this.PageCur = 'words'
			console.log(this.PageCur)
		}
	}
</script>

<style>

</style>
