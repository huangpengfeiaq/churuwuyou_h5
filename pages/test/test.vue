<template>
	<view>
		<inputs :inputsArray="inputsArray" activeName="登录" :ruleSet="ruleSet"   @chaildOpenEvent="openWin"
		 @activeFc="activeFc" :onLoadData="onLoadData" animationType="slide-fade-right" :animationDuration=".3"
		 submitReSet :buttonStyle="buttonStyle"/>
		 <button type="primary" @tap="add">加一个</button>
	</view>
</template>

<script>
	import inputs from "@/components/QuShe-inputs/inputs.vue";
	var input_inedex = 0;
	export default {
		data() {
			return {
				"buttonStyle": { //按钮样式
					"activeButton": "background-color: #c0ebd7;border-radius: 30px;box-shadow: 2px 2px 1px 1px #c0ebd7;", //主按钮样式
					"changeButton": "background-color: #c0ebd7;border-radius: 30px;box-shadow: 2px 2px 1px 1px #c0ebd7;", //picker类型更改按钮样式
					"selectButton": "background-color: #c0ebd7;border-radius: 30px;box-shadow: 2px 2px 1px 1px #c0ebd7;", //picker类型选择按钮样式
					"confirmButton": "background-color: #c0ebd7;border-radius: 30px;box-shadow: 2px 2px 1px 1px #c0ebd7;", //picker类型弹出框中确定按钮样式
					"getcodeButton": "background-color: #c0ebd7;border-radius: 30px;box-shadow: 2px 2px 1px 1px #c0ebd7;" //获取验证码按钮样式
				},
				"inputsArray": [],
				"ruleSet": {
					"color": "#c0ebd7",
					"checkbox_color": "#c0ebd7",
					"itemArray": [{
						"name": "用户协议",
						"value": "用户协议"
					},{
						"name": "隐私政策",
						"value": "隐私政策"
					}],
				},
				"contentSet": {
					"width": 80,
					"layout": "left"
				},
				"onLoadData": "data_",
			}
		},
		created() {
			console.log('启动了')
			// 初始值根据后端提供值赋值示例
			let inputsArray = [
				{
					title: '告警灯是否正常',
					type: 'radio',
					itemArray: [
						{
							name: '是',
							value: '1'
						},{
							name: '否',
							value: '0'
						}
					]
				}
			]
			//访问接口
			setTimeout(()=>{
				//获取数据
				let defaultValue = '1';
				inputsArray[0].itemArray.find((item)=>{
					return defaultValue === item.value
				}).defaultValue = true;
				// console.log(JSON.stringify(inputsArray));
				this.inputsArray = inputsArray;
			},200)
		},
		methods: {
			openWin(value) {
				//打开规则或协议页
				//若有一个以上的rule，则根据value打开规则页面
				console.log(value);
			},
			activeFc(res) {
				uni.showToast({
					title: "获取输入成功"
				})
				console.log(JSON.stringify(res));
			},
			add() {		// 动态改变inputsArray示例 （inputs中watch监听的是inputsArray的内存地址，所以要改变inputsArray要改变他的内存地址，要重新赋值）
				let i = input_inedex++;
				this.inputsArray = this.inputsArray.concat({
					title: 'input' + i,
					type: 'input' + i
				})
			}
		},
		components: {
			inputs
		}
	}
</script>

<style>
</style>
