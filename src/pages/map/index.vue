<!--  -->
<template>
  <view>
    <button type="primary" @tap="openMap">打开地图</button>
    <button type="primary" @tap="selectMap">选择地图</button>
  </view>
</template>

<script>
export default {
  data () {
    return {
    }
  },

  components: {},

  computed: {},

  onLoad () {
  },

  methods: {
    openMap () {
      wx.getLocation({
        type: 'gcj02', //返回可以用于wx.openLocation的经纬度
        success (res) {
          console.log('res', res)
          const latitude = res.latitude
          const longitude = res.longitude
          wx.openLocation({
            latitude,
            longitude,
            scale: 18
          })
        }
      })
    },
    selectMap () {
      wx.chooseLocation({
        success: function (res) {
          console.log(res);
        }
      })
    }
  }
}

</script>
<style lang='scss' scoped>
#myMap {
  width: 100%;
  min-height: 10vh;
}
</style>