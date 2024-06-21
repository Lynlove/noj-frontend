<template>
  <div id="userLoginView">
    <h2>用户注册</h2>
    <a-space>
      <h2>
        <routerLink class="router-link" to="/user/login">登录</routerLink>
      </h2>
      <h2>
        <routerLink class="router-link" to="/user/register">注册</routerLink>
      </h2>
    </a-space>
    <a-form
      style="width: 480px; margin: 0 auto"
      label-align="left"
      auto-label-width
      :model="form"
      @submit="handleSubmit"
    >
      <a-form-item
        :rules="[
          { required: true, message: '账号不能为空' },
          { minLength: 4, message: '账号⻓度不能低于四位' },
        ]"
        field="userAccount"
        label="账号"
      >
        <a-input v-model="form.userAccount" placeholder="请输入账号" />
      </a-form-item>
      <a-form-item
        :rules="[{ required: true, message: '用户名不能为空' }]"
        field="userName"
        label="用户名"
      >
        <a-input v-model="form.userName" placeholder="请输入用户名" />
      </a-form-item>
      <a-form-item
        :rules="[
          { required: true, message: '密码不能为空' },
          { minLength: 8, message: '密码⻓度不能低于⼋位' },
        ]"
        field="userPassword"
        tooltip="密码不少于 8 位"
        label="密码"
      >
        <a-input-password
          v-model="form.userPassword"
          placeholder="请输入密码"
        />
      </a-form-item>
      <a-form-item
        :rules="[
          { required: true, message: '密码不能为空' },
          { minLength: 8, message: '密码⻓度不能低于⼋位' },
        ]"
        field="checkPassword"
        tooltip="密码不少于 8 位"
        label="确认密码"
      >
        <a-input-password
          v-model="form.checkPassword"
          placeholder="请输入密码"
        />
      </a-form-item>
      <a-form-item>
        <a-button
          type="primary"
          html-type="submit"
          style="width: 120px; margin: 0 auto"
          >注册
        </a-button>
      </a-form-item>
    </a-form>
  </div>
</template>
<script setup lang="ts">
import { reactive } from "vue";
import { UserControllerService } from "../../generated";
import message from "@arco-design/web-vue/es/message";
import { useRouter } from "vue-router";
import { useStore } from "vuex";

/**
 *
 表单信息 */
const form = reactive({
  userAccount: "",
  userName: "",
  userPassword: "",
  checkPassword: "",
});
const router = useRouter();
const store = useStore();

/**
 *
 提交表单 * @param data
 */
const handleSubmit = async () => {
  if (form.userAccount.length < 4 || form.userPassword.length < 6) {
    return;
  }
  if (
    form.checkPassword.length !== form.userPassword.length ||
    form.checkPassword !== form.userPassword
  ) {
    message.error("两次输⼊密码不⼀致");
    return;
  }
  const res = await UserControllerService.userRegisterUsingPost(form);
  //登录成功，跳转到主⻚
  if (res.code === 0) {
    message.success("注册成功,自动登录");
    await UserControllerService.userLoginUsingPost({
      userAccount: form.userAccount,
      userPassword: form.userPassword,
    });
    await store.dispatch("user/getLoginUser");
    await router.push({
      path: "/",
      replace: true,
    });
  } else {
    message.error(res.message);
  }
};
</script>
<style>
.router-link {
  text-decoration: none;
}
</style>
