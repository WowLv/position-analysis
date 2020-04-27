<template>
  <div class="date-rank-container">
    <el-collapse v-model="activeNames" class="date-table">
      <el-collapse-item name="1">
         <template slot="title"><span class="title"><i class="el-icon-medal"></i>日期排行榜</span></template>
        <div class="date-rank-main">
           <el-table
            :data="updateData"
            style="width: 100%">
            <el-table-column
              prop="name"
              label="日期"
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
    <column-bar-sub class="top" :column-bar-data="updateData" title="日期排行榜"></column-bar-sub>
  </div>
</template>

<script>
import { getAllUpdate } from '@/api/map'
import { TopFiveDate } from '@/utils/sortData'
import columnBarSub from '@/components/charts/column-bar-sub'
export default {
  components: {
    columnBarSub
  },
  data() {
    return {
      activeNames: ['1'],
      updateData: [],
      title: '时间排行榜'
    }
  },
  mounted() {
    this.getTop()
  },
  methods: {
    async getTop() {
      const { data } = await getAllUpdate()
      this.updateData = TopFiveDate(data)
    }
  }
}
</script>

<style lang="scss" scoped>
.date-rank-container {
  width: 100%;
  height: 100%;
  display: flex;
  .date-table {
    flex: 1;
    .title {
      font-size: 24px;
      margin-left: 20px;
    }
    .date-rank-main {
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
