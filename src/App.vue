<template>
  <div id="app"></div>
</template>

<script>
import AMap from 'AMap'
export default {
  name: 'App',
  components: {},
  data() {
    return {
      map: null, // 地图实例
      position: [121.670629, 31.247346], // 初始的经纬度
      markerPosition: [
        {
          position: [121.670629, 31.247346],
          custId: "1",
          custName: "上海银行",
          url: ""
        },
        {
          position: [121.667373, 31.249433],
          custId: "2",
          custName: "上海银行财神庙",
          url: ""
        },
        {
          position: [121.678253, 31.247538],
          custId: "3",
          custName: "招商银行",
          url: ""
        }
      ],
    }
  },
  mounted() {
    this.initMap()
    this.getCurrentAddress(this.position)
  },
  methods: {
    // 1.初始化地图
    initMap() {
      this.map = new AMap.Map('app', {
        resizeEnable: true, //是否监控地图容器尺寸变化
        zoom: 16, //初始化地图层级
        center: [121.670629, 31.247346] //初始化地图中心点
      });
      this.addMarker()
    },
    // 2.实例化地图的点标记
    addMarker() {
      this.markerPosition.forEach(item => {
        let marker = new AMap.Marker({
          icon: "https://a.amap.com/jsapi_demos/static/demo-center/icons/poi-marker-default.png",
          position: item.position,
          offset: new AMap.Pixel(-13, -30)
        })
        marker.setMap(this.map)
      })
    },
    // 3.查询当前地址的数据
    getCurrentAddress(position) {
      let geo = new AMap.Geocoder({
        city: "上海市"
      });
      geo.getAddress(position, function (status, result) {
        if (status === 'complete' && result.regeocode) {
          console.log('获取到的地址是', result.regeocode.formattedAddress)
        } else {
          console.log('查询地址失败')
        }
      })

    }
  }
}
</script>

<style>
#app {
  width: 100%;
  height: 500px;
  border: 1px solid pink;
}
.amap-icon img,
.amap-marker-content img {
  width: 25px;
  height: 34px;
}

.marker {
  position: absolute;
  top: -20px;
  right: -118px;
  color: #fff;
  padding: 4px 10px;
  box-shadow: 1px 1px 1px rgba(10, 10, 10, 0.2);
  white-space: nowrap;
  font-size: 12px;
  font-family: "";
  background-color: #25a5f7;
  border-radius: 3px;
}
</style>


