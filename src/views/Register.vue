<template>
  <div class="container">
    <div class="form-container">
      <h1>Register</h1>
      <form @submit.prevent="register">
        <label for="email">Email:</label>
        <input type="email" v-model="email" required>
        <label for="password">Password:</label>
        <input type="password" v-model="password" required>
        <button type="submit">Register</button>
      </form>
      <router-link to="/login">Already have an account? Login</router-link>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Register',
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async register() {
      try {
        const response = await axios.post('/api/register', {
          email: this.email,
          password: this.password
        });
        alert(response.data);
        this.$router.push('/login');
      } catch (error) {
        alert('Error: ' + error.response.data);
      }
    }
  }
};
</script>
