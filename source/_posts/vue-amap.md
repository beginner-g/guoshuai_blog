---
title: vue中引用高德地图amap
categories:
  - Vue
date: 2019-11-14 10:20:00
tags: [vue, vue-amap]
cover_picture: http://img1.imgtn.bdimg.com/it/u=80834248,2473924617&fm=27&gp=0.jpg
---
### vue中引用高德地图amap具体流程

#### 引入 高德，web-sdk
- 安装 vue-amap
```
	npm install vue-amap
```
- 在html中引入
在官网申请密钥: https://lbs.amap.com 申请密钥
```js
	<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.8&key = 你自己的Key"></script>
```
或者
```js
	<script type="text/javascript">
		// 初始化地图
		window.VueAMap.initAMapApiLoader({
			key: '你自己的Key',
			plugin: [
				'AMap.Autocomplete',
				'AMap.PlaceSearch',
				'AMap.Scale',
				'AMap.OverView',
				'AMap.ToolBar',
				'AMap.MapType',
				'AMap.PolyEditor',
				'AMap.CircleEditor',
				'AMap.Geolocation',
				'AMap.ElasticMarker',
				...
			],
			uiVersion: '1.0',
			v: '1.4.4',
		});
	</script>
```
#### 单纯获取当前位置信息
- 获取经纬度
	用的TypeScript写法，不懂的可以去[TypeScript](http://www.typescriptlang.org/docs/home.html)官网查询下
```js
private getMap() {
	let map: any;
	let geolocation: any;
	const self = this;
	map = new AMap.Map('container', {
		resizeEnable: true,
	});
	map.plugin('AMap.Geolocation', (o: any) => {
		geolocation = new AMap.Geolocation({
　　　　enableHighAccuracy: true, // 是否使用高精度定位，默认:true
　　　　timeout: 20000, // 超过10秒后停止定位，默认：无穷大
　　　　buttonPosition: 'RB',
		});
		geolocation.getCurrentPosition();
		// tslint:disable-next-line:no-unused-expression
		new AMap.event.addListener(geolocation, 'complete', function onComplete(data: any) {
			const getLongitude = data.position.getLng();
			const getLatitude = data.position.getLat();
			self.latitude = getLongitude;
			self.longitude = getLatitude;
			// self.getData();
		});
	});
}
```
最后在你需要用到的地方去调this.getMap()

#### 显示地图
- 引入地图标签
```html
<el-amap :zoom='zoom' :center='center' :plugin="plugin" :events="events"  class="amap-demo">
	<el-amap-marker
		v-for="(marker, index) in markers"
		:position="marker.position"
		:events="marker.events"
		:visible="marker.visible"
		:draggable="marker.draggable"
		:key="index"
		:clickable="true"
		vid="marker"
	/>
</el-amap>
```
- 定义变量
```js
private lng: any = 0;
private lat: any = 0;
private center: any = []; // 地图中心点
private loaded: boolean = true;
private zoom: any = '13'; // 地图放大限制
private markers: any = [];
private plugin: any = [];
private events: any = {};
```

- 配置地图
```js
const self = this;
self.plugin = [
	{
		enableHighAccuracy: true, //是否使用高精度定位，默认:true
		timeout: 100, //超过10秒后停止定位，默认：无穷大
		maximumAge: 0, //定位结果缓存0毫秒，默认：0
		convert: true, //自动偏移坐标，偏移后的坐标为高德坐标，默认：true
		showButton: true, //显示定位按钮，默认：true
		buttonPosition: 'RB', //定位按钮停靠位置，默认：'LB'，左下角
		showMarker: true, //定位成功后在定位到的位置显示点标记，默认：true
		showCircle: true, //定位成功后用圆圈表示定位精度范围，默认：true
		panToLocation: true, //定位成功后将定位到的位置作为地图中心点，默认：true
		zoomToAccuracy: true, //定位成功后调整地图视野范围使定位位置及精度范围视野内可见，默认：false
		extensions: 'all',
		pName: 'Geolocation',
		events: {
			init: (o: any) => {
				// o 是高德地图定位插件实例
				o.getCurrentPosition((status: any, result: any) => {
					if (result && result.position) {
						self.center = [result.position.lng, result.position.lat];
						self.loaded = true;
						self.lng = result.position.lng;
						self.lat = result.position.lat;
						self.markers[0].position = [self.lng, self.lat]; // 标记默认在定位处
					}
				});
			},
		},
	},
];
self.events = { //选点
	init: (o: any) => {
		self.lng = o.getCenter().lng;
		self.lat = o.getCenter().lat;
		o.getCity((result: any) => {});
	},
	click(e: any) {
		self.lng = e.lnglat.lng;
		self.lat = e.lnglat.lat;
		self.markers[0].position = [self.lng, self.lat];
	},
};
self.markers = [ // 标记点
	{
		position: self.center,
		anchor: 'center',
		events: {
			// 点击触发
			click: (e: any) => {
				self.lng = e.lnglat.lng;
				self.lat = e.lnglat.lat;
				self.loaded = true;
			},
			// 移动触发
			dragend: (e: any) => {
				self.markers[0].position = [e.lnglat.lng, e.lnglat.lat];
				self.lng = e.lnglat.lng;
				self.lat = e.lnglat.lat;
			},
		},
		visible: true,
		draggable: true,
	},
];
```