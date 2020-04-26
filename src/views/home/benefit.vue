<template>
  <div class="heat-map-container">
    <heat-map class="heat-map" :heat-map-data="heatMapData" />
</div>
</template>

<script>
import { getPositionHeatmap } from '@/api/position'
import heatMap from '@/components/charts/heat-map'

export default {
  components: {
    heatMap
  },
  data() {
    return {
      heatMapData: []
    }
  },

  mounted() {
    // this.initBenefit()
    this.getHeatmapData()
  },
  methods: {
    async getHeatmapData() {
      const { data } = await getPositionHeatmap()
      this.heatMapData = data
    }
  }
}
</script>

<style lang="scss" scoped>
.heat-map-container {
  width: 100%;
  height: 100%;
  // position: relative;
  .heat-map {
      height: 400px;
      background: #fff;
    }
}

</style>
