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
          placeholder="Enter your username"
        />
        <p v-if="errors.username" class="error">{{ errors.username }}</p>
      </div>

      <div class="form-group">
        <label for="email">Email</label>
        <input
          id="email"
          v-model="form.email"
          type="email"
          placeholder="Enter your email"
        />
        <p v-if="errors.email" class="error">{{ errors.email }}</p>
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input
          id="password"
          v-model="form.password"
          type="password"
          placeholder="Enter your password"
        />
        <p v-if="errors.password" class="error">{{ errors.password }}</p>
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

// Form data
const form = reactive({
  username: '',
  email: '',
  password: ''
})

// Error messages
const errors = reactive({
  username: '',
  email: '',
  password: ''
})

// Validation and submission
function handleRegister() {
  // Reset previous errors
  errors.username = ''
  errors.email = ''
  errors.password = ''

  let isValid = true

  // Username validation
  if (!form.username.trim()) {
    errors.username = 'Username is required.'
    isValid = false
  }

  // Email validation
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!form.email.trim()) {
    errors.email = 'Email is required.'
    isValid = false
  } else if (!emailPattern.test(form.email)) {
    errors.email = 'Please enter a valid email address.'
    isValid = false
  }

  // Password validation
  if (!form.password.trim()) {
    errors.password = 'Password is required.'
    isValid = false
  } else if (form.password.length < 6) {
    errors.password = 'Password must be at least 6 characters long.'
    isValid = false
  }

  if (!isValid) return

  // ✅ If all good:
  console.log('Registering user:', form)
  alert(`Welcome, ${form.username}! Registration successful.`)

  // Reset form
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
.error {
  color: #e74c3c;
  font-size: 13px;
  margin-top: 3px;
}
.login-link {
  text-align: center;
  margin-top: 15px;
}
</style>
