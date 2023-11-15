<template>
    <div class="login-container">
      <form @submit.prevent="onSubmit" class="login-form">
        <h2>Login</h2>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="loginData.email">
        </div>
        <div class="password-field">
          <label for="password">Password:</label>
          <vue-password-strength-meter type="password" id="password" v-model="loginData.password"></vue-password-strength-meter>
        </div>
        <button type="submit">Login</button>
      </form>
    </div>
  </template>
  
  <script lang="js">
  import VuePasswordStrengthMeter from 'vue-password-strength-meter';
  import axios from 'axios';
  export default {
    components: {
      VuePasswordStrengthMeter
    },
    data() {
      return {
        loginData: {
          email: '',
          password: ''
        }
      };
    },
    methods: {
    onSubmit() {
      if (!this.loginData.email || !this.loginData.password) {
        alert('Email and password are required');
        return;
      }

      const formData = new URLSearchParams();
      formData.append('email', this.loginData.email);
      formData.append('password', this.loginData.password);

      axios.post('https://api-demo.forgingblock.io/signin', formData, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        //   'Origin': 'http://localhost:8080/' 
        }
      })
      .then(response => {
        // Handle success
        console.log('Login successful', response);
        // You might want to handle the received cookie here
      })
      .catch(error => {
        // Handle error
        console.error('Login error', error);
      });
    }
  }
  };
  </script>
  
  <style scoped>
  .login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .login-form {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    width: 100%
  }
  
  .login-form input[type="email"],
  .login-form input[type="password"] {
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .password-field{
    display: flex;

  }
  .vue-password-strength-meter {
    max-width: 100%;
    background-color: none;

    /* margin-bottom: 20px; */
  }
  .Password{
    max-width: 100%;
    margin-left: 0;
    }
  </style>
  