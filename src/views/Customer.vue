<template>
  <div class="customer">
    <el-row>
      <el-col
        :xs="{ span: 24, offset: 0 }"
        :lg="{ span: 8, offset: 8 }"
        :xl="{ span: 8, offset: 8 }"
      >
        <el-form
          :ref="form"
          :model="form"
          label-width="60px"
          label-position="left"
        >
          <el-form-item label="姓名">
            <el-input
              v-model="form.name"
              placeholder="请输入姓名"
            ></el-input>
          </el-form-item>
          <el-form-item label="手机号">
            <el-input
              v-model="form.mobilephone"
              placeholder="请输入手机号"
            ></el-input>
          </el-form-item>
          <el-form-item label="地址">
            <el-input
              v-model="form.address"
              placeholder="请输入地址"
            ></el-input>
          </el-form-item>
          <el-form-item label="日期">
            <el-col :span="14">
              <el-date-picker
                v-model="form.createdat"
                placeholder="请选择日期"
                size='large'
              ></el-date-picker>
            </el-col>
          </el-form-item>
          <el-form-item label="备注">
            <el-input
              type="textarea"
              :rows="2"
              v-model="form.remark"
              placeholder="请输入备注"
            ></el-input>
          </el-form-item>
          <el-button
            type="primary"
            @click="onSubmit"
          >保存</el-button>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  data () {
    return {
      form: {
        name: '',
        mobilephone: '',
        address: '',
        remark: '',
        createdat: '',
        updatedat: '2020-06-06',
        status: '1'
      }
    }
  },
  methods: {
    onSubmit () {
      if (this.form.name !== '') {
        this.$axios.post('/customer/', this.form).then(() => {
          this.$message({
            message: `${this.form.name} 保存成功`,
            type: 'success'
          })
          this.$router.push('about')
        }).catch(() => {
          this.$message({
            message: `${this.form.name} 保存失败`,
            type: 'error'
          })
        })
      } else {
        this.$message.warning('用户名不能为空')
      }
    },
    open () {
      this.$message({
        message: '恭喜你，这是一条成功消息',
        type: 'success'
      })
    }
  },

  computed: {
    setRemark () {
      return `客户家庭地址: ${this.form.address} `
    }
  }
}
</script>
