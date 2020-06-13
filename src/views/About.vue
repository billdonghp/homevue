<template>
  <div class="about">

    <el-container>
      <el-header style="text-align: right; font-size: 12px">
        <el-dropdown @command="handleCommand">
          <i
            class="el-icon-setting"
            style="margin-right: 15px"
          ></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="see">查看</el-dropdown-item>
            <el-dropdown-item command="new">新增</el-dropdown-item>
            <el-dropdown-item command="delete">删除</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
        <span>{{username}}</span>
      </el-header>
      <el-main>
        <el-table :data="tableData">
          <el-table-column
            prop="id"
            label="客户ID"
            width="80"
          >
          </el-table-column>
          <el-table-column
            prop="createdat"
            label="日期"
            width="140"
          >
          </el-table-column>
          <el-table-column
            prop="name"
            label="姓名"
            width="120"
          >
          </el-table-column>
          <el-table-column
            prop="mobilephone"
            label="手机号"
            width="120"
          >
          </el-table-column>
          <el-table-column
            prop="address"
            label="地址"
            width="200"
          >
          </el-table-column>
          <el-table-column
            prop="remark"
            label="备注"
            width="200"
          >
          </el-table-column>
          <el-table-column
            label="操作"
            width="80px"
          >
            <template slot-scope="scope">
              <el-button @click="handleDelete(scope.$index, scope.row)">删除</el-button>
            </template>
          </el-table-column>
        </el-table>
      </el-main>
    </el-container>

  </div>
</template>
<style>
.el-header {
  background-color: #409eff;
  color: #333;
  line-height: 60px;
}
.el-aside {
  color: #333;
}
</style>
<script>
export default {
  data () {
    return {
      tableData: [],
      username: window.localStorage.name
    }
  },
  methods: {
    handleCommand (command) {
      if (command === 'see') {
        this.getTableDate()
      } else if (command === 'new') {
        this.$router.push('customer')
      } else {
        this.$notify({
          title: command,
          message: '这是一条不会自动关闭的消息',
          duration: 0
        })
      }
    },
    handleDelete (index, row) {
      this.$axios.delete('/customer/' + row.id).then(res => {
        this.$message({
          message: `${row.name} 删除成功`,
          type: 'success'
        })
        this.tableData.splice(index, 1)
      }).catch(res => {

      })
    },
    getTableDate () {
      this.$axios.get('/customer').then((res) => {
        this.tableData = res.data
      }).catch(function () {

      })
    }
  },
  mounted () {
    this.getTableDate()
  }
}
</script>
