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
      <button type="submit" class="btn btn-primary" @click.prevent="login">Login</button>
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
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post(API_URL + "test_stationery/login", {
          username: this.username,
          password: this.password
        });

console.log('Login successful');
} catch (error) {
console.log('Login failed');
}
},
},
};
</script>
