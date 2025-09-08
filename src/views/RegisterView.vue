<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import { register } from '@/utils/api';
const router = useRouter();

// 表單資料
const email = ref('');
const nickname = ref('');
const password = ref('');
const confirmPassword = ref('');

const handleRegister = async () => {
  // 新增：檢查密碼是否一致
  if (password.value !== confirmPassword.value) {
    alert('兩次輸入的密碼不一致，請重新輸入。');
    return; // 終止函式執行
  }

  // 新增：基本的密碼長度驗證 (可選)
  if (password.value.length < 6) {
    alert('密碼長度需至少為 6 個字元。');
    return;
  }
  try {
    await register(email.value, password.value, nickname.value);
    alert('註冊成功');
    // 註冊成功後頁面轉到login頁面
    router.push('/login');
  } catch (error) {
    alert(error.response.data.message);
  }
};
</script>

<template>
  <div id="signUpPage" class="bg-yellow">
    <div class="conatiner signUpPage vhContainer">
      <div class="side">
        <a href="#"
          ><img
            class="logoImg"
            src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/logo.png"
            alt=""
        /></a>
        <img
          class="d-m-n"
          src="https://raw.githubusercontent.com/hexschool/2022-web-layout-training/main/todolist/img.png"
          alt="workImg"
        />
      </div>
      <div>
        <form class="formControls" action="index.html">
          <h2 class="formControls_txt">註冊帳號</h2>
          <label class="formControls_label" for="email">Email</label>
          <input
            class="formControls_input"
            type="text"
            id="email"
            name="email"
            placeholder="請輸入 email"
            v-model="email"
            required
          />
          <label class="formControls_label" for="name">您的暱稱</label>
          <input
            class="formControls_input"
            type="text"
            name="name"
            id="name"
            placeholder="請輸入您的暱稱"
            v-model="nickname"
          />
          <label class="formControls_label" for="pwd">密碼</label>
          <input
            class="formControls_input"
            type="password"
            name="pwd"
            id="pwd"
            placeholder="請輸入密碼"
            v-model="password"
            required
          />
          <label class="formControls_label" for="pwd">再次輸入密碼</label>
          <input
            class="formControls_input"
            type="password"
            name="pwd"
            id="pwd1"
            placeholder="請再次輸入密碼"
            v-model="confirmPassword"
            required
          />
          <input
            class="formControls_btnSubmit"
            type="button"
            @click="handleRegister"
            value="註冊帳號"
          />
          <RouterLink class="formControls_btnLink" to="/login">登入</RouterLink>
        </form>
      </div>
    </div>
  </div>
</template>
