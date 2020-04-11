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
	
	
	
		<!-- 主体内容 -->
		<view class="container">
			<!-- 预设模版 开始听写 -->
			<view v-if="TabCur==0">	
				<view class='padding margin text-center'>
					
					<view class="cu-form-group margin-top">
						<view class="title">内置单词本</view>
						<picker @change="wordListChange" :value="index" :range="picker">
							<view class="picker">
								{{index>-1?picker[index]:'选择'}}
							</view>
						</picker>
					</view>
					
					<view class="cu-form-group ">
						<view class="title">本次听写个数</view>
						<picker @change="wordAmountChange" :value="wordsindex" :range="wordAmount">
							<view class="picker">
								{{wordsindex>-1?wordAmount[wordsindex]:'选择'}}
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
				
				<view class="cu-list menu">
					<view class="cu-item" :class="modalName=='move-box-'+ index?'move-cur':''" 
					 v-for="(item,index) in wordList" :key="index"
					 @touchstart="ListTouchStart" @touchmove="ListTouchMove" @touchend="ListTouchEnd" 
					 :data-target="'move-box-' + index">
					 
						<!-- <view class="cu-avatar round lg" :style="[{backgroundImage:'url(https://ossweb-img.qq.com/images/lol/web201310/skin/big2100'+ (index+2) +'.jpg)'}]"></view> -->
						<view class="content">
							<view class="text-grey">{{item}}</view>
						</view>
			
						<view class="move">
							<view class="bg-red">删除</view>
						</view>
					</view>
				</view>
				
				<!-- 添加新单词 -->
				<form @submit="addWord">
					<view class="cu-form-group">
						<input placeholder="输入单词" name="input" v-model="input"></input>
						<button form-type="submit" class='cu-btn bg-green shadow'>添加</button>
					</view>
				</form>
				
				
				<view class='padding margin text-center'>
					<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="saveList" data-target="viewModal">
						保存该组
					</view>
					<view class='cu-btn bg-green lg block shadow radius margin-xl' @tap="startDictation" data-target="viewModal">
						开始听写
					</view>
				</view>
			</view>	
		</view>
		
		<!-- 解决导航栏遮住底部内容问题 撑一个空白div-->
		<div class="blank"></div>
		
		
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
				topList: ['内置模版','自定义'],
				TabCur: 0,   // 顶部导航栏选中的哪一项
				PageCur: 'words',
				index:-1,  // 选中哪一本词汇书
				picker: ['大学英语四级', '大学英语六级', '考研英语'],
				wordAmount: ['10','20','30'],
				wordsindex:-1,
				wordsSum:0,    // 听写多少个单词  
				input:'',
				
				// 单词列表左滑删除用：
				listTouchStart: 0,
				listTouchDirection: null,
				modalName: null,
				
				//单词列表：
				wordList:['test','test','test']
				

			}
		},
		methods: {
			saveList(){   // 保存该组单词列表
				
			},
			
			startDictation(){ 
				console.log("start dictation......")
				let listId = this.index
				let wordNum = this.wordsSum
				console.log("listID:",listId)
				uni.navigateTo({
                    url: '../dictate/dictate?listId='+listId+'&&wordNum='+wordNum   // 跳转到听写页面
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
			
			wordListChange(e) {  // 记录词汇表的index
				this.index = e.detail.value
				console.log("this.index:",this.index)
			},
			
			wordAmountChange(e) {  // 记录词汇量的wordsindex
				this.wordsindex = e.detail.value
				this.wordsSum = this.wordAmount[e.detail.value]
				console.log("this.wordsSum:",this.wordsSum)
			},
			
			jump(pageName) {
				uni.navigateTo({
				    url: `../${pageName}/${pageName}`,
				    success: res => {},
				    fail: () => {},
				    complete: () => {}
			    })
			},
			
			// 添加新单词	
			addWord(e){
				let word = e.detail.value.input
				console.log("added word:",word)
				this.wordList.push(word)
				this.input = ''   // 输入后清空输入框
				console.log("Current wordlist:",this.wordList)
				
			},
			
			// ListTouch触摸开始
			ListTouchStart(e) {
				this.listTouchStart = e.touches[0].pageX
			},
			
			// ListTouch计算方向
			ListTouchMove(e) {
				this.listTouchDirection = e.touches[0].pageX - this.listTouchStart > 0 ? 'right' : 'left'
			},
			
			// ListTouch计算滚动
			ListTouchEnd(e) {
				if (this.listTouchDirection == 'left') {
					this.modalName = e.currentTarget.dataset.target
				} else {
					this.modalName = null
				}
				this.listTouchDirection = null
			}
			
			
			
		},
		onShow(){
			console.log("Onshow")
			this.PageCur = 'words'
			this.index = -1
		}
	}
</script>

<style>
	/* .container{
		margin-bottom: 50px;
	} */
	.blank{
		height: 50px;
	}
	
	
</style>
