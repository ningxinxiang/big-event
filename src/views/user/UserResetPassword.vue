<script setup>
import { ref } from 'vue';
import { ElMessage } from 'element-plus';
// import { updatePwd } from './api/user.js';

const userInfo = ref({
  id: 0,
  username: '东哥',
  oldpassword: '',
  password: '',
  repassword: '',
});

const rules = {
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    { pattern: /^\S{2,10}$/, message: '密码必须是2-10位的非空字符串', trigger: 'blur' }
  ],
  repassword: [
    { required: true, message: '请再次输入密码', trigger: 'blur' },
    { validator: (rule, value, callback) => {
      if (value !== userInfo.value.password) {
        callback(new Error('两次输入的密码不一致'));
      } else {
        callback();
      }
    }, message: '两次输入的密码不一致', trigger: 'blur' }
  ],
  oldpassword: [
    { required: true, message: '请输入原密码', trigger: 'blur' }
  ]
};



// const updatepassword = async () => {
//   try {
    
//     let info = new FormData();
//     info.append('oldpassword', userInfo.value.oldpassword);
//     info.append('password', userInfo.value.password);
//     info.append('repassword', userInfo.value.repassword);
//     // let result = await updatePwd(info);
//     if (result.data.code === 0) {
//       ElMessage.success('修改成功');
//     } else {
//       ElMessage.error(result.data.message || '修改失败');
//     }
//   } catch (error) {
//     ElMessage.error('请求失败：' + error.message);
//   }
// };
</script>
<template>
    <el-card class="page-container">
        <template #header>
            <div class="header">
                <span @click="clearDate">重置密码</span>
            </div>
        </template>
        <el-row>
            <el-col :span="12">
                <el-form :model="userInfo" :rules="rules" label-width="100px" size="large">
                    <el-form-item label="登录名称">
                        <el-input v-model="userInfo.username" disabled></el-input>
                    </el-form-item>
                    <el-form-item label="原密码" prop="oldpassword">
                      <el-input v-model="userInfo.oldpassword"></el-input>
                  </el-form-item>
                    <el-form-item label="新密码" prop="password">
                        <el-input v-model="userInfo.password"></el-input>
                    </el-form-item>
                    <el-form-item label="再次确认密码" prop="repassword">
                        <el-input v-model="userInfo.repassword"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="updatepassword">提交修改</el-button>
                    </el-form-item>
                </el-form>
            </el-col>
        </el-row>
    </el-card>
</template>