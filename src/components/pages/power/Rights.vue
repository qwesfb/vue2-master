<template>
<div class="right">
<el-card>
    <el-row class="top">
        <el-table :data="tableData" border style="width: 100%"  stripe>
             <el-table-column type="index"  label="#" width="80">
            </el-table-column>
            <el-table-column prop="authName"  label="权限名称" width="550">
            </el-table-column>
            <el-table-column   prop="level" label="权限等级" >
                <template slot-scope="scope">
                    <el-tag v-if="scope.row.level==='0'">一级</el-tag>
                    <el-tag type="success" v-else-if="scope.row.level==='1'">二级</el-tag>
                    <el-tag type="warning" v-else="scope.row.level==='2'">三级</el-tag>
                </template>
            </el-table-column>
        </el-table>
    </el-row>
</el-card>

</div>
</template>

<script>
export default {
  data () {
    return {
      tableData: []
    }
  },
  created () {
    this.getrights()
  },
  methods: {
    async getrights () {
      const { data: res } = await this.$http.get('rights/list')
      if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
      this.tableData = res.data
      // console.log(this.tableData);
    }
  }
}
</script>
