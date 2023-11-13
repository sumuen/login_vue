<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="p-6 max-w-sm w-full bg-white rounded-lg border border-gray-200 shadow-md">
      <h2 class="mb-6 text-2xl font-bold text-center text-gray-700">登录</h2>
      <form @submit.prevent="login">
        <div class="mb-4">
          <label for="username" class="block mb-2 text-sm font-medium text-gray-900">用户名</label>
          <input type="text" id="username" v-model="username"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
            required>
        </div>
        <div class="mb-4">
          <label for="password" class="block mb-2 text-sm font-medium text-gray-900">密码</label>
          <input type="password" id="password" v-model="password"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
            required>
        </div>
        <div class="mb-4 flex items-center">
          <input type="checkbox" id="agreement" v-model="agreed" class="mr-2">
          <label for="agreement" class="text-sm text-gray-600">我已阅读并同意
            <a href="https://www.baidu.com" class="text-blue-500 hover:text-blue-600" target="_blank">协议</a>
          </label>
        </div>
        <button type="submit" :disabled="!agreed"
          class="w-full text-white bg-blue-500 hover:bg-blue-600 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center disabled:bg-blue-300">登录</button>

      </form>
      <div class="mt-6">
        <table class="min-w-full border-collapse block md:table">
          <thead class="block md:table-header-group">
            <tr class="border md:table-row">
              <th class="block md:table-cell">用户名</th>
              <th class="block md:table-cell">密码</th>
            </tr>
          </thead>
          <tbody class="block md:table-row-group">
            <tr class="border md:table-row" v-for="(account, index) in accounts" :key="index">
              <td class="block md:table-cell">{{ account.username }}</td>
              <td class="block md:table-cell">{{ account.password }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    return {
      username: '',
      password: '',
      agreed: false,
      accounts: []  // 添加此行
    };
  },
  methods: {
    login() {
      // 读取 localStorage 中的账号信息
      const storedAccounts = JSON.parse(localStorage.getItem('accounts')) || [];
      storedAccounts.push({ username: this.username, password: this.password });

      // 更新 localStorage
      localStorage.setItem('accounts', JSON.stringify(storedAccounts));

      // 更新组件的账号列表
      this.accounts = storedAccounts;

      console.log("登录请求：", this.username, this.password);
    }
  }
};
</script>
