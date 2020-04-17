<template>
	<view>
		<cu-custom bgColor="bg-white" :isBack="true"><block slot="backText"></block><block slot="content">我的</block></cu-custom>
		
		
		<!-- 头像框 -->
		<view class="cu-list menu-avatar">
			<view class="cu-item">
				<view class="cu-avatar round lg" :style=" 'background-image:url('+userInfo.wxProfile.avatarUrl+');'"></view>
				<view class="content" style="width: calc(100% - 200upx)">
						<text class="text-cut margin-top-sm">username</text>
				</view>
			</view>
		</view>
		
		
		
		<!-- 列表栏 -->
		<view class="cu-list menu" :class="[menuBorder?'sm-border':'',menuCard?'card-menu margin-top':'']">
		  <view class="cu-item arrow" @tap="jump('record')">
		   <navigator class="content" hover-class="none" open-type="redirect" url="">
		    <text class="cuIcon-sort text-black"></text>
		    <text class="text-grey">学习记录</text>
		   </navigator>
		  </view>


		  <view class="cu-item arrow">
		   <navigator class="content" hover-class="none" @tap="jump('mylist')">
		    <text class="cuIcon-copy text-black"></text>
		    <text class="text-grey">我的词库</text>
		   </navigator>
		  </view>
		  
		  <view class="cu-item arrow">
		   <navigator class="content" hover-class="none" @tap="jump('myquiz')">
		    <text class="cuIcon-voice text-black"></text>
		    <text class="text-grey">我的问答</text>
		   </navigator>
		  </view>

		
		  <view class="cu-item arrow">
		   <navigator class="content" hover-class="none" @tap="jump('')">
		    <text class="cuIcon-service text-black"></text>
		    <text class="text-grey">联系客服</text>
		   </navigator>
		  </view>
		
		  <view class="cu-item arrow">
		   <navigator class="content" hover-class="none" @tap="jump('about')">
		    <text class="cuIcon-mail text-black"></text>
		    <text class="text-grey">关于我们</text>
		   </navigator>
		  </view>
		  
		 </view>
		 
		 
		 
		 
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
				PageCur:'my'	
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
			
		},
		onShow(){
			this.PageCur = 'my'
		}
	}
</script>

<style>

</style>
