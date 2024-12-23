/* eslint-disable */ 
<template>
  <div id="app">
    <header>
      <h1>DataHive</h1>
    </header>
    <UserButtons />
    <router-view></router-view>
  </div>
</template>

<script>
import UserButtons from '@/components/UserButtons.vue' 

export default {
  name: 'App',
  components: {
    UserButtons 
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #333;
  color: white;
  height: 100vh;
  display: flex;
  flex-direction: column;
}

header {
  background-color: #222;
  padding: 1rem;
}

h1 {
  font-size: 3rem;
  margin-bottom: 2rem;
}
</style>
