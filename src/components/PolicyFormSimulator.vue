<template>
  <div class="policy-form-container">
    <h2>保單基本資料填寫 (模擬測試版)</h2>
    <el-form :model="policyholder" @submit.prevent="simulateSubmit" label-width="120px">
      <el-form-item label="姓名">
        <el-input v-model="policyholder.name" placeholder="請輸入姓名" required></el-input>
      </el-form-item>

      <el-form-item label="身分證字號">
        <el-input v-model="policyholder.idNumber" placeholder="請輸入身分證字號" required></el-input>
      </el-form-item>

      <el-form-item label="出生日期">
        <el-date-picker v-model="policyholder.birthDate" type="date" placeholder="請選擇出生日期" value-format="YYYY-MM-DD" required></el-date-picker>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" native-type="submit">送出 (模擬)</el-button>
      </el-form-item>
    </el-form>

    <div v-if="successMessage" class="message success">{{ successMessage }}</div>
    <div v-if="errorMessage" class="message error">{{ errorMessage }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      policyholder: {
        name: '',
        idNumber: '',
        birthDate: ''
      },
      successMessage: '',
      errorMessage: ''
    };
  },
  methods: {
    simulateSubmit() {
      // 重設訊息
      this.successMessage = '';
      this.errorMessage = '';

      console.log('正在模擬提交表單資料:', this.policyholder);

      // 使用 setTimeout 模擬後端處理的延遲，這段邏輯與您提供的範例相同
      setTimeout(() => {
        // 模擬成功回應
        this.successMessage = '模擬成功！保單資料已提交。';
        console.log('模擬成功，模擬的資料為:', this.policyholder);
        // 清空表單
        this.policyholder = { name: '', idNumber: '', birthDate: '' };
      }, 1000); // 1秒後顯示成功訊息
    }
  }
};
</script>

<style scoped>
/* 使用與 PolicyForm.vue 相同的樣式以保持一致性 */
.policy-form-container {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  background-color: #fff;
}
h2 {
  text-align: center;
  color: #333;
}
.message {
  margin-top: 20px;
  padding: 10px;
  border-radius: 4px;
  text-align: center;
}
.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}
.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}
</style>