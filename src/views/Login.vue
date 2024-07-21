<template>
  <div class="container">
    <div class="form-container">
      <h1>Login</h1>
      <form @submit.prevent="login">
        <label for="email">Email:</label>
        <input type="email" v-model="email" required>
        <label for="password">Password:</label>
        <input type="password" v-model="password" required>
        <button type="submit">Login</button>
      </form>
      <router-link to="/register">Don't have an account? Register</router-link>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post('/api/login', {
          email: this.email,
          password: this.password
        });
        alert(response.data);
        localStorage.setItem('auth-token', 'dummy-token');  // 保存一个简单的 token
        this.$router.push('/');
      } catch (error) {
        alert('Error: ' + error.response.data);
      }
    }
  }
};
</script>
