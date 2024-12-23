/* eslint-disable */ 
<template>
  <div class="buttons-container">
    <button class="btn btn-teachers">Teachers</button>
    <button class="btn btn-students">Students</button>
  </div>
</template>

<script>
export default {
  name: 'UserButtons' 
}
</script>

<style scoped>
.buttons-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  margin-top: 2rem;
}

.btn {
  width: 200px;
  height: 60px;
  font-size: 1.5rem;
  font-weight: bold;
  border-radius: 30px;
  background-color: #333;
  color: white;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #4e504e;
}

.btn-teachers {
  order: 2;
}

.btn-students {
  order: 1;
}
</style>
