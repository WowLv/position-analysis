<template>
  <div class="location-rank-container">
    <el-collapse v-model="activeNames" class="location-table">
      <el-collapse-item name="1">
         <template slot="title"><span class="title"><i class="el-icon-medal"></i>地区排行榜</span></template>
        <div class="location-rank-main">
           <el-table
            :data="locationData"
            style="width: 100%">
            <el-table-column
              prop="name"
              label="省份"
              width="280">
            </el-table-column>
            <el-table-column
              prop="value"
              label="数量"
              width="280">
            </el-table-column>
          </el-table>
        </div>
      </el-collapse-item>
    </el-collapse>
    <column-bar-sub class="top" :column-bar-data="locationData" title="地区排行榜"></column-bar-sub>
  </div>
</template>

<script>
import { getAllProvince } from '@/api/map'
import { TopFiveDate } from '@/utils/sortData'
import columnBarSub from '@/components/charts/column-bar-sub'
export default {
  components: {
    columnBarSub
  },
  data() {
    return {
      activeNames: ['1'],
      locationData: []
    }
  },
  mounted() {
    this.getTop()
  },
  methods: {
    async getTop() {
      const { data } = await getAllProvince()
      this.locationData = TopFiveDate(data)
    }
  }
}
</script>

<style lang="scss" scoped>
.location-rank-container {
  width: 100%;
  height: 100%;
   display: flex;
  .location-table {
    flex: 1;
    .title {
      font-size: 24px;
      margin-left: 20px;
    }
    .location-rank-main {
      margin: 0 20px;
    }
  }
  .top {
    flex: 1;
    height: 385px;
    width: 100%;
  }
}

</style>
