<!--  -->
<template>
  <view>
    <map class='map' id='myMap' :longitude="longitude" :latitude="latitude"
      show-location="true" :markers="markers" bindmarkertap="bindMakertap" bindcontroltap='controlTap' 
      bindregionchange='regionChange'
      bindtap='bindMapTap'
    >
    </map>
  </view>
</template>

<script>
export default {
  data () {
    return {
      longitude: 120,
      latitude: 30,
      markers: [],
      polyline: ''
    }
  },

  components: {},

  computed: {},

  mounted () {},

  methods: {}
}

</script>
<style lang='scss' scoped>
.map {
  width: 100%;
  height: 50vh;
}
</style>