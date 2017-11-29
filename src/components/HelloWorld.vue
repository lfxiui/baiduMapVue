<template>
  <div>
    <div id="map" class="map"></div>
    <button v-on:click="hidePolygon()">隐藏多边形</button>
    <button v-on:click="showPolygon()">显示多边形</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        map:null,
        point:null,
        marker:null,
        polygon:null
      }
    },
    mounted() {
      this.map = new BMap.Map("map");
      this.map.enableScrollWheelZoom();
      this.point = new BMap.Point(113.297391, 23.099386);
      this.map.centerAndZoom(this.point, 19);
      this.marker = new BMap.Marker(this.point);  // 创建标注
      this.map.addOverlay(this.marker);               // 将标注添加到地图中
      this.marker.setAnimation(BMAP_ANIMATION_BOUNCE); //跳动的动画
      /!*多边形*!/
      this.polygon = new BMap.Polygon([
        new BMap.Point(113.297405, 23.100084),
        new BMap.Point(113.298272, 23.099498),
        new BMap.Point(113.297634, 23.098916),
        new BMap.Point(113.296884, 23.09929)
      ], {strokeColor: "blue", strokeWeight: 2, strokeOpacity: 0.5});  //创建多边形
      //设置多边形的填充颜色
      this.polygon.setFillColor("red");
      this.map.addOverlay(this.polygon);
    },
    methods: {
      hidePolygon:function () {
        this.polygon.hide();
      },
      showPolygon:function () {
        this.polygon.show();
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .map {
    height: 500px;
    width: 1000px;
  }
</style>
