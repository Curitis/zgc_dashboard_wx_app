<template>
	<view class="content">
		<view>
			<div id="myChart" style="width:500px;height:460px;"></div>
        </view>
	</view>
</template>

<script lang="ts" setup>
import Vue from 'vue';
import * as echarts from 'echarts';

export default Vue.extend({
	data() {
		return {
			title: 'Hello'
		}
	},
	mounted() {
		// setTimeout(()=>{
			this.initEchart()
		// },3000)
		console.log(22222)
	},
	methods: {
		initEchart(){
			// 基于准备好的dom，初始化echarts实例
			var myChart = echarts.init(document.getElementById('myChart'));
			// data2拿到真实数据后需要处理一下，加上%
			var data2 = ["45.9", "18.9", "50", "80.6", "65.2","39.6"];
			var data1 = [];
			for (var i = 0; i < data2.length; i++) {
				data1.push({
					value: 100,
					label: data2[i],
				});
			}
			var barWidth = 21;
			var option = {
				grid: {
					left: 30,
					right: 40,
					top: 20,
					bottom: 20,
					containLabel: true,
				},
				xAxis: {
					type: "value",
					axisLine: { show: false },
					axisTick: { show: false },
					splitLine: { show: false },
					axisLabel: {show: false },
					offset: 0,
					// data: ["规模以上单位数","资产总计","营业收入","利润总额","各项税金","从业人员"],
				},
				yAxis: {
					type: "category",
					name: "y轴",
					axisLine: { show: false },
					axisTick: { show: false },
					splitLine: { show: false },
					nameTextStyle: {
						color: "transparent",
					},
					axisLabel: {
						show: true,
						color: "#334365",
						fontSize: 10,
						// align: "left",
					},
					// position: "right",
					offset: 0,
					// formatter: (params, index) => {
					// 	return params + '%';
					// },
					data: ["规模以上单位数","资产总计","营业收入","利润总额","各项税金","从业人员"]
				},
				series: [
					{
						// 上半截柱子
						name: "上半截柱子",
						type: "bar",
						barWidth: barWidth,
						barGap: "-100%",
						z: 0,
						itemStyle: {
							color: "#C2DBFF",
							opacity: 0.6,
						},
						data: data1,
					},
					{
						//下半截柱子
						name: "下半截柱子",
						type: "bar",
						barWidth: barWidth,
						barGap: "-100%",
						itemStyle: {
							opacity: 1,
							color: function () {
								return new echarts.graphic.LinearGradient(0,0.6,0,0,
									[
										{
											offset: 0,
											color: "#3399FF", // 0% 处的颜色
										},
										{
											offset: 1,
											color: "#A6C7F2", // 100% 处的颜色
										},
									], false
								);
							},
						},
						data: data2,
					},
					{
						type: "bar",
						barWidth: barWidth,
						barGap: "-100%",
						itemStyle: {
							color: "transparent",
						},
						data: data2,
					},
					{
						//上半截柱子顶部圆片
						name: "上半截柱子顶部圆片",
						type: "pictorialBar",
						symbolSize: [6,barWidth],
						symbolOffset: [3,0],
						z: 12,
						symbolPosition: "end",
						itemStyle: {
							color: "#C2DBFF",
							opacity: 1,
						},
						label: {
							show: true,
							position: "insideTopRight",
							fontSize: 12,
							color: "#334365",
							formatter: function (params) {
								return params.data.label + "%";
							},
						},
						data: data1,
					},
					{
						//下半截柱子顶部圆片
						name: "下半截柱子顶部圆片",
						type: "pictorialBar",
						symbolSize: [6,barWidth],
						symbolOffset: [3,0],
						z: 12,
						itemStyle: {
							opacity: 1,
							color: "#107FEE",
						},
						label: {
							show: false,
							position: "left",
							fontSize: 12,
							color: "#fff",
						},
						symbolPosition: "end",
						data: data2,
					},
					{
						//下半截柱子底部圆片
						name: "",
						type: "pictorialBar",
						symbolSize: [5,barWidth],
						symbolOffset: [-2,0],
						z: 12,
						itemStyle: {
							opacity: 1,
							color: "#50A6FC",
						},
						data: [1,1,1,1,1,1],
					},
				],
			};

			// 绘制图表
			myChart.setOption(option);
		}

	}
});
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
		margin: 200rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
