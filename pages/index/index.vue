<template>
	<view class="content">
		<view class="showList" >
			<scroll-view scroll-y="true"  :scroll-into-view="currentKey" style="height: 1200upx;" >
				<view v-for="(item,key) in cityList" :id="key">
						<view class="letter">{{key}}</view>
						<view class="cityList">
							<view v-for="(val,index) in item">{{val.name}}</view>
						</view>
				</view>
				
			</scroll-view>
			<view class="rightBar" @touchstart="scrollStart" @touchmove="scrollmove">
				<view v-for="(item,key) in cityList" :data-key="key" :key="key">
					{{key}}
				</view>
			</view>
		</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '选择城市',
				cityList:{},
				currentKey:""
			}
		},
		onLoad() {
				this.init();
		},
		methods: {
			init(){
				uni.request({
					url:"https://api.wanghongplatform.com/mobile/app/city/list",
					data:{
						accessToken:'CD4460BCA9AFFE002DA4324DB87F8E86',
						token:'CD4460BCA9AFFE002DA4324DB87F8E86',
						cityName:'上海',
						userId:'1007198',
						latitude:'31.24916171',
						longitude:'121.48789949',
						vno:'1.0.1',
						source:'mobile',
						celebrityId:'',
						cityId:'10035'
					},
					method:'GET',
					success:(res)=>{
						let _this = this;
						console.log(res);
						let list = res.data.data;
						let newList={},newLetter=[];
						for (let val of list) {
							if(val.status=='Y'&&newList["Host"]){
								newList["Host"].push(val)
							}else if(val.status=='Y'&&!newList["Host"]){
								newList["Host"]=[];
								newList["Host"].push(val)
							}else if(newList[val.sorts]){
								newList[val.sorts].push(val)
							}else{
								newList[val.sorts]=[];
								newList[val.sorts].push(val)
							}
						}
						let finellyObj={Host:newList.Host,
													  A:newList.A,
														B:newList.B,
														C:newList.C,
														D:newList.D,
														E:newList.E,
														F:newList.F,
														G:newList.G,
														H:newList.H,
														I:newList.I,
														J:newList.J,
														K:newList.K,
														L:newList.L,
														M:newList.M,
														N:newList.N,
														O:newList.O,
														P:newList.P,
														Q:newList.Q,
														R:newList.R,
														S:newList.S,
														T:newList.T,
														U:newList.U,
														V:newList.V,
														W:newList.W,
														X:newList.X,
														Y:newList.Y,
														Z:newList.Z};
						console.log(finellyObj)
						_this.cityList=finellyObj
					}
				})
			},
			scrollStart(e){
				let currentKey = e.target.dataset.key;
				this.currentKey=currentKey;
			},
			scrollmove(e){
				// console.log(e.target.dataset.key)
				let currentKey = e.target.dataset.key;
				this.currentKey=currentKey;
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
	.rightBar{
		width: 40upx;
		height: 80%;
		position: fixed;
		top: 60upx;
		bottom: 0;
		right: 10upx;
		margin: auto;
		border-radius: 20upx;
		background-color: #ccc;
		font-size: 20upx;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		align-items: center;
		padding: 20upx 0;
		z-index: 99999;
	}
	.showList{
		width: 100%;
		padding: 10upx  20upx;
		box-sizing: border-box;
	}
	.showList .letter{
		width: 100%;
		background-color: #ddd;
		font-size: 24upx;
		padding-left: 20upx;
		height: 50upx;
		line-height: 50upx;
	}
	.showList .cityList>view{
		height: 80upx;
		line-height: 80upx;
		font-size: 30upx;
		border-bottom: 1upx solid #f5f5f5;
		padding-left: 20upx;
		box-sizing: border-box;
	}
</style>
