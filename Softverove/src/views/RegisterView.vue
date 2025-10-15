<template>
  <div class="register-page">
    <h1>Create Account</h1>

    <form @submit.prevent="handleRegister">
      <div class="form-group">
        <label for="username">Username</label>
        <input
          id="username"
          v-model="form.username"
          type="text"
          required
          placeholder="Enter your username"
        />
      </div>

      <div class="form-group">
        <label for="email">Email</label>
        <input
          id="email"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter your email"
        />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input
          id="password"
          v-model="form.password"
          type="password"
          required
          placeholder="Enter your password"
        />
      </div>

      <button type="submit">Register</button>
    </form>

    <p class="login-link">
      Already have an account?
      <router-link to="/login">Login</router-link>
    </p>
  </div>
</template>

<script setup>
import { reactive } from 'vue'

// reactive object to hold form data
const form = reactive({
  username: '',
  email: '',
  password: ''
})

function handleRegister() {
  if (!form.username || !form.email || !form.password) {
    alert('Please fill in all fields')
    return
  }

  console.log('Registering user:', form)

  // ✅ later you’ll replace this with a POST request to Laravel
  alert(`Welcome, ${form.username}! Registration successful.`)

  // reset form
  form.username = ''
  form.email = ''
  form.password = ''
}
</script>

<style scoped>
.register-page {
  max-width: 400px;
  margin: 80px auto;
  padding: 20px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
.form-group {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}
label {
  margin-bottom: 5px;
  font-weight: bold;
}
input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 14px;
}
button {
  width: 100%;
  background: #42b883;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
}
button:hover {
  background: #369f73;
}
.login-link {
  text-align: center;
  margin-top: 15px;
}
</style>
