<template>
    <div class="sign-up-container">
      <h1>Sign Up</h1>
      <form @submit.prevent="submitSignUp">
        <input type="text" v-model="username" placeholder="Username" required>
        <input type="email" v-model="email" placeholder="Email" required>
        <input type="password" v-model="password" placeholder="Password" required>
        <input type="password" v-model="confirmPassword" placeholder="Confirm Password" required>
        <input type="text" v-model="specialKey" placeholder="Special Key" required>
        <button type="submit" class="btn">Sign Up</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    name: 'SignUp',
    data() {
      return {
        username: '',
        email: '',
        password: '',
        confirmPassword: '',
        specialKey: ''
      }
    },
    methods: {
      async submitSignUp() {
        if (this.password !== this.confirmPassword) {
          alert('Passwords do not match')
          return
        }
  
        try {
          await axios.post('/api/sign-up', {
            username: this.username,
            email: this.email,
            password: this.password,
            specialKey: this.specialKey
          })
          // Redirect to login page or show success message
        } catch (error) {
          alert('Error signing up: ' + error.message)
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .sign-up-container {
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