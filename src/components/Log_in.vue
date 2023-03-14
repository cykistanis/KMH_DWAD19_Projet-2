<template>
    <div>
      <h1>Login Form</h1>
      <form>
        <div class="form-group">
          <label for="username">Username</label>
          <input type="text" class="form-control" id="username" v-model="username" />
        </div>
        <div class="form-group">
          <label for="password">Password</label>
          <input type="password" class="form-control" id="password" v-model="password" />
        </div>
        <button type="submit" class="btn btn-primary" @click.prevent="login()">Login</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        username: '',
        password: '',
      };
    },
    methods: {
      async login() {
        try {
          const response = await axios.post('/api/authenticate', {
            username: this.username,
            password: this.password,
          });
  
          console.log(response.data); // This should contain the authentication token
        } catch (error) {
          console.log(error);
        }
      },
    },
  };
  </script>