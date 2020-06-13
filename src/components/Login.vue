<template>
  <div class="login">
    <el-row>
      <el-col
        :xs="{ span: 24, offset: 0 }"
        :lg="{ span: 8, offset: 8 }"
        :xl="{ span: 8, offset: 8 }"
      >
        <el-form
          ref="form"
          :model="form"
          label-width="80px"
          label-position="left"
          size="mini"
        >
          <el-form-item label="用户名">
            <el-input
              placeholder="请输入用户"
              v-model="form.name"
            ></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input
              v-model="form.pwd"
              show-password
              placeholder="请输入密码"
            ></el-input>
          </el-form-item>
          <el-form-item>
            <el-switch
              v-model="form.isSave"
              active-text="保存"
            ></el-switch>
          </el-form-item>
          <el-form-item>
            <el-button
              type="primary"
              @click="onSubmit()"
            >注册</el-button>
            <el-button
              type="primary"
              @click="reset()"
            >重置</el-button>
          </el-form-item>
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
        name: window.localStorage.getItem('name')
          ? window.localStorage.getItem('name')
          : '',
        pwd: '',
        isSave: window.localStorage.getItem('name') !== null
      }
    }
  },
  methods: {
    onSubmit () {
      if (this.form.isSave === true) {
        if (this.form.name != null) {
          window.localStorage.setItem('name', this.form.name)
        }
      } else {
        window.localStorage.clear()
      }
      console.log(this.form.name)
    },
    reset () {
      this.form.name = ''
      this.form.pwd = ''
    },
    userregister () {

    }
  }
}
</script>
