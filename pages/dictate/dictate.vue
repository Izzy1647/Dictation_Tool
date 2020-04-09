<template>
	<view>
        <cu-custom bgColor="bg-white" :isBack="true"><block slot="backText"></block><block slot="content">听写</block></cu-custom>
		
		<!-- 头部提示框 -->
		<view class="cu-chat" style="position: relative; top: 10px;">
			<view class="cu-item padding-top-xl">
				<view class="cu-avatar radius" style="background-image:url(../../static/tabbar/about_cur.png);"></view>
				<view class="main">
					<view class="content shadow">
						<text>听写中......答案写在答案区。</text>
					</view>
				</view>
			</view>
		</view>
		
		
		<!-- 用户输入框 -->
		<view class="cu-form-group align-start">
			<!-- <view class="title">答案区</view> -->
			<textarea maxlength="-1" :disabled="modalName!=null" @input="textareaBInput" placeholder="写下你的答案吧"></textarea>
		</view>
		
		<view class='cu-btn bg-red lg block shadow radius margin-xl' @tap="stopDictation" data-target="viewModal">
			停止听写
		</view>
		
		<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="showAnswer" data-target="viewModal">
			查看答案
		</view>
		
		<!-- 查看答案出现： -->
		<view  v-if="ifAnswer">	
			<view class="padding-sm">
				<view class="flex flex-wrap justify-around">
					<button class="margin-sm basis-sm shadow cu-btn" :class="['bg-' + item.color,toggleDelay?'animation-slide-bottom':'']"
					 :style="[{animationDelay: (index + 1)*0.1 + 's'}]" v-for="(item,index) in list" :key="index">0.{{index+1}}s</button>
				</view>
			</view>
			
			<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="hideAnswer" data-target="viewModal">
				隐藏答案
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
				PageCur: 'words',
				ifAnswer:false,     // true则显示答案
				toggleDelay: false,
				list: [{
						name: 'fade',
						color: 'red'
					},
					{
						name: 'scale-up',
						color: 'orange'
					},
					{
						name: 'scale-down',
						color: 'olive'
					},
					{
						name: 'slide-top',
						color: 'green'
					}, {
						name: 'slide-bottom',
						color: 'cyan'
					},
					{
						name: 'slide-left',
						color: 'blue'
					},
					{
						name: 'slide-right',
						color: 'purple'
					},
					{
						name: 'shake',
						color: 'mauve'
					}
				]
			}
		},
		methods: {
			showAnswer(){
				this.ifAnswer = true
			},
			
			hideAnswer(){
				this.ifAnswer = false
			},
			
			stopDictation(){
				console.log("Stop dictation...")
			}
		
			
		}
	}
</script>

<style>

</style>
