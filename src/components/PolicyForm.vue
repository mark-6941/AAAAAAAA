<template>
  <div class="policy-form-container">
    <h2>填寫保單基本資料</h2>

    <!-- 使用 Element Plus 表單開始 -->
    <el-form :model="policyholder" @submit.prevent="submitPolicyData" label-width="120px">
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
        <el-button type="primary" native-type="submit">送出</el-button>
      </el-form-item>
    </el-form>
    <!-- Element Plus 表單結束 -->

    <div v-if="successMessage" class="message success">{{ successMessage }}</div>
    <div v-if="errorMessage" class="message error">{{ errorMessage }}</div>
  </div>
</template>

<script>
import axios from 'axios';

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
    async submitPolicyData() {
      // 重設訊息
      this.successMessage = '';
      this.errorMessage = '';

      try {
        // 這行是重點！將 API 位址指向您用 JSON Server 啟動的虛擬後端
        const response = await axios.post(' http://localhost:3000/policies', this.policyholder);
        this.successMessage = '保單資料已成功送出！保單編號: ' + response.data.id;
        console.log('Response from server:', response.data);

        // 清空表單
        this.policyholder = { name: '', idNumber: '', birthDate: '' };

      } catch (error) {
        this.errorMessage = '送出保單資料失敗，請確認後再試。';
        console.error('Error submitting policy data:', error);
      }
    }
  }
};
</script>

<style scoped>
/* 使用與 Element Plus 範例相同的樣式以保持美觀 */
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
