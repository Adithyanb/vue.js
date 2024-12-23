<template>
    <div class="login-container">
      <h1>Login</h1>
      <form @submit.prevent="submitLogin">
        <input type="email" v-model="email" placeholder="Email" required>
        <input type="password" v-model="password" placeholder="Password" required>
        <input type="text" v-model="specialKey" placeholder="Special Key" required>
        <button type="submit" class="btn">Login</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    name: 'Login',
    data() {
      return {
        email: '',
        password: '',
        specialKey: ''
      }
    },
    methods: {
      async submitLogin() {
        try {
          const response = await axios.post('/api/login', {
            email: this.email,
            password: this.password,
            specialKey: this.specialKey
          })
          // Handle successful login, e.g., redirect to dashboard
        } catch (error) {
          alert('Error logging in: ' + error.message)
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .login-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #333;
    color: white;
  }
  
  h1 {
    font-size: 3rem;
    margin-bottom: 2rem;
  }
  
  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    width: 400px;
  }
  
  input {
    height: 50px;
    font-size: 1.2rem;
    padding: 0 1rem;
    border-radius: 25px;
    border: none;
  }
  
  .btn {
    height: 50px;
    font-size: 1.2rem;
    font-weight: bold;
    border-radius: 25px;
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .btn:hover {
    background-color: #45a049;
  }
  </style>