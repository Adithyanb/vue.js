<template>
    <div class="student-dashboard-container">
      <header>
        <h1>DataHive</h1>
      </header>
      <div class="content-container">
        <div class="chat-container">
          <h2>Chatbot</h2>
          <div class="chat-messages">
            <!-- Chatbot messages will be displayed here -->
          </div>
          <input type="text" v-model="chatQuery" placeholder="Ask a question">
          <button @click="sendChatQuery" class="btn">Submit</button>
        </div>
      </div>
      <footer>
        <span>{{ userName }}</span>
        <button class="btn">Sign Out</button>
      </footer>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  
  export default {
    name: 'StudentDashboard',
    data() {
      return {
        chatQuery: '',
        userName: 'Jane Doe'
      }
    },
    methods: {
      async sendChatQuery() {
        try {
          const response = await axios.post('/api/chat', { query: this.chatQuery })
          // Update the chat messages container with the response
          this.chatQuery = ''
        } catch (error) {
          alert('Error sending chat query: ' + error.message)
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .student-dashboard-container {
    display: flex;
    flex-direction: column;
    height: 100vh;
    background-color: #333;
    color: white;
  }
  
  header, footer {
    background-color: #222;
    padding: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  h1, h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  
  .content-container {
    display: flex;
    flex-grow: 1;
  }
  
  .chat-container {
    flex-basis: 100%;
    background-color: #555;
    padding: 2rem;
  }
  
  .chat-messages {
    height: 400px;
    overflow-y: auto;
    margin-bottom: 1rem;
  }
  
  input {
    width: 100%;
    height: 50px;
    font-size: 1.2rem;
    padding: 0 1rem;
    border-radius: 25px;
    border: none;
    margin-bottom: 1rem;
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