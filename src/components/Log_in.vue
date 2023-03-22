<template>
  <div>
    <h1>Login Form</h1>
    <form @submit.prevent="login">
      <div class="form-group">
        <label for="username">Username</label>
        <input type="text" class="form-control" id="username" v-model="username" :class="{ 'is-invalid': usernameError }" />
        <div class="invalid-feedback">{{ usernameError }}</div>
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" class="form-control" id="password" v-model="password" :class="{ 'is-invalid': passwordError }" />
        <div class="invalid-feedback">{{ passwordError }}</div>
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
const API_URL = "https://educateddelectablepascal.cykistanis.repl.co/";

export default {
  data() {
    return {
      username: '',
      password: '',
      usernameError: '',
      passwordError: '',
    };
  },
  methods: {
    async login() {
      this.usernameError = '';
      this.passwordError = '';

      // // Validate username
      // if (!this.username) {
      //   this.usernameError = 'Username is required';
      // } else if (this.username.length < 3) {
      //   this.usernameError = 'Username must be at least 3 characters long';
      // }

      // // Validate password
      // if (!this.password) {
      //   this.passwordError = 'Password is required';
      // } else if (this.password.length < 8) {
      //   this.passwordError = 'Password must be at least 8 characters long';
      // }

      // // If there are errors, don't submit the form
      // if (this.usernameError || this.passwordError) {
      //   return;
      // }

      // Make API request
      try {
        const response = await axios.post(API_URL + "test_stationery/login", {
          username: this.username,
          password: this.password
        });
        console.log('Login successful');
      } catch (error) {
        console.error(error);
        alert('Login failed');
      }
    },
  },
};
</script>
