<template>
    <div class="teacher-dashboard-container">
      <header>
        <h1>DataHive</h1>
      </header>
      <div class="content-container">
        <div class="left-sidebar">
          <h2>File and Text Upload</h2>
          <input type="file" @change="uploadFile">
          <textarea v-model="textToUpload" placeholder="Enter text to upload"></textarea>
          <button @click="uploadText" class="btn">Upload Text</button>
          <h2>Uploaded History</h2>
          <ul>
            <li v-for="item in uploadHistory" :key="item.id">
              {{ item.name }} - {{ item.type }}
            </li>
          </ul>
        </div>
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
    name: 'TeacherDashboard',
    data() {
      return {
        uploadHistory: [],
        textToUpload: '',
        chatQuery: '',
        userName: 'John Doe'
      }
    },
    methods: {
      async uploadFile(event) {
        const file = event.target.files[0]
        try {
          await axios.post('/api/upload-file', file)
          this.getUploadHistory()
        } catch (error) {
          alert('Error uploading file: ' + error.message)
        }
      },
      async uploadText() {
        try {
          await axios.post('/api/upload-text', { text: this.textToUpload })
          this.textToUpload = ''
          this.getUploadHistory()
        } catch (error) {
          alert('Error uploading text: ' + error.message)
        }
      },
      async getUploadHistory() {
        try {
          const response = await axios.get('/api/upload-history')
          this.uploadHistory = response.data
        } catch (error) {
          alert('Error fetching upload history: ' + error.message)
        }
      },
      async sendChatQuery() {
        try {
          const response = await axios.post('/api/chat', { query: this.chatQuery })
          // Update the chat messages container with the response
          this.chatQuery = ''
        } catch (error) {
          alert('Error sending chat query: ' + error.message)
        }
      }
    },
    mounted() {
      this.getUploadHistory()
    }
  }
  </script>
  
  <style scoped>
  .teacher-dashboard-container {
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
  
  .left-sidebar {
    flex-basis: 30%;
    background-color: #444;
    padding: 2rem;
  }
  
  .chat-container {
    flex-basis: 70%;
    background-color: #555;
    padding: 2rem;
  }
  
  .chat-messages {
    height: 400px;
    overflow-y: auto;
    margin-bottom: 1rem;
  }
  
  input, textarea {
    width: 100%;
    height: 50px;
    font-size: 1.2rem;
    padding: 0 1rem;
    border-radius: 25px;
    border: none;
    margin-bottom: 1rem;
  }
  
  textarea {
    height: 100px;
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