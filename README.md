# uniapp——瀑布流组件
该组件采用了左右两个容器来布局瀑布流，而非使用绝对定位去实现，有效避免瀑布流排版失误导致页面重叠等情况。瀑布流图片可采用widthFix模式，不会因为再次加载的原因导致高度获取不精准等问题。该组件兼容了上拉刷新、触底加载等功能。

## 更新记录
### 1.0.1 (2021-06-18)
优化只显示单列的情况。

### 1.0.0 (2020-06-14)
开发该瀑布流组件。

## 效果图

### 微信小程序
![微信小程序](./static/微信小程序.jpeg)

### H5
![H5](./static/H5.png)

### APP
![Android](./static/APP_Android.jpeg)

![IOS](./static/APP_IOS.jpeg)

## 兼容平台
H5 APP 小程序

## 瀑布流样式
可在WaterfallsFlowItem修改样式。

## 组件属性
| 属性名        | 类型   |  说明  |
| --------  | :-----  | :----  |
| wfList        | Array   |   必填，瀑布流列表     |
| updateNum        |   Number   |  默认为10，每次更新的数量   |
| @itemTap        |    	EventHandle    |  点击事件，返回item整个object  |

## 使用方法

将`components`路径下的组件引入到你的项目，或者去[DCLOUD插件市场](https://ext.dcloud.net.cn/plugin?id=2060)下载安装。

```vue
<template>
	<view class="page">
		<WaterfallsFlow :wfList='list' @itemTap="itemTap" />
	</view>
</template>

<script>
	import WaterfallsFlow from '../../components/WaterfallsFlow/WaterfallsFlow.vue'
	
	export default {
		components:{
			WaterfallsFlow
		},
		data() {
			return {
				list:[],
				requiredData:[]   // 存放模拟加载的数据
			}
		},
		onLoad() {
			// 模拟请求数据
			setTimeout(()=>{
				this.list = this.requiredData;
			},500)
		},
		onReachBottom(){
			// 模拟触底刷新
			setTimeout(()=>{
				this.requiredData.push(...this.list);
			},500)
		},
		onPullDownRefresh(){
			// 模拟上拉刷新
			setTimeout(()=>{
				const newList = this.requiredData.reverse();
				this.list = newList;
				uni.stopPullDownRefresh();
			},500)
		},
		methods:{
			itemTap(item){
				console.log(item);
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.page{
		min-height: 100vh;
		background: #eee;
	}
</style>
```