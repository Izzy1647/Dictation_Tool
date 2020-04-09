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
	
		
		<!-- 预设模版 开始听写 -->
		<view v-if="TabCur==0">	
			<view class='padding margin text-center'>
				
				<view class="cu-form-group margin-top">
					<view class="title">内置单词本</view>
					<picker @change="PickerChange" :value="index" :range="picker">
						<view class="picker">
							{{index>-1?picker[index]:'选择'}}
						</view>
					</picker>
				</view>
				
				<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="startDictation" data-target="viewModal">
					开始听写
				</view>
			</view>
		</view>
		
		<!-- 用户自定义单词表页面 -->
		<view v-if="TabCur==1">
			<view class='padding margin text-center'>		
				
				<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="startDictation" data-target="viewModal">
					开始听写
				</view>
			</view>
			
			

		</view>

		
		<!-- 底部导航栏 -->
		<view class="cu-bar tabbar bg-white shadow foot">
			<view class="action" @click="jump('')" data-cur="words">
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
			<view class="action" @click="jump('my')" data-cur="plugin">
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
				topList: ['内置模版','自定义'],
				TabCur: 0,   // 顶部导航栏选中的那一项
				PageCur: 'words',
				index:-1,
				picker: ['大学英语四级', '大学英语六级', '考研英语'],
				
			}
		},
		methods: {
			startDictation(){ 
				console.log("start dictation......")
				let listId = this.index
				console.log("listID:",listId)
				uni.navigateTo({
                    url: '../dictate/dictate?listId='+listId   // 跳转到听写页面
                    // success: res => {},
                    // fail: () => {},
                    // complete: () => {}
                })
			},
			tabSelect(e) {   // 记录顶部导航栏
				console.log("tabSelect.e:",e)
				this.TabCur = e.currentTarget.dataset.id;
				this.scrollLeft = (e.currentTarget.dataset.id - 1) * 60
				console.log("tabcur:",this.TabCur)
			},
			PickerChange(e) {  // 记录下拉选择栏
				this.index = e.detail.value
				console.log("this.index:",this.index)
			},
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
			console.log("Onshow")
			this.PageCur = 'words'
			this.index = -1
		}
	}
</script>

<style>

</style>
