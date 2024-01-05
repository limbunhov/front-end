<template>
  <div class="main-login">
      <div class="container" id="login">
          <div class="cart_form">
              <h2>Login Form</h2>
              <form @submit.prevent="handleLogin">
                  <label>Email address:</label>
                  <i class="fa-regular fa-envelope"></i>
                  <input type="email" id="loginEmail" v-model="loginData.email"
                      placeholder="Email..." required>
                  <label for="loginPassword">Password:</label>
                      <i class="fa-solid fa-lock"></i>
                      
                          <input type="password" id="loginPassword" v-model="loginData.password"
                              placeholder="Password..." required>

                  <div class="z-1 d-flex flex-column justify-content-center align-items-center">
                      <button type="submit" class="btn btn-primary">Login</button>
                      <span>Not a member? <a @click="toggleForm">Register</a></span>
                  </div>
              </form>
          </div>
      </div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      isLoggedIn: false,
      loginData: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    async handleLogin() {
      try {
        const response = await axios.post('http://localhost:3000/login', this.loginData);

        if (response && response.data) {
          console.log('Login successful', response.data);
          alert('Login successful!');

          // Store the token and user ID in localStorage
          localStorage.setItem('token', response.data.token);
          localStorage.setItem('userId', response.data.userId);

          // Fetch the role using getRole function
          const userRole = await this.getRole(response.data.userId);
          console.log(userRole);
          if (userRole === 'admin') {
            this.$router.push('/adminpage'); // typo: should be '/admin-page'
          } else {
            this.$router.push('/');
          }
        } else {
          console.error('Invalid response format:', response);
          alert('Login failed. Please try again.');
        }
      } catch (error) {
        console.error('Login failed', error.response ? error.response.data : error.message);
        alert('Login failed. Please try again.');
      }
    },

    async getRole(userId) {
        try {
            const response = await axios.get(`http://localhost:3000/role/${userId}`);
            const userRole = response.data.role;
            console.log(userRole);
            return userRole;
        } catch (error) {
            console.error('Error fetching user role:', error);
            throw error; // Rethrow the error to be caught in the higher level
        }
    },
    mounted() {
      const isLoggedIn = localStorage.getItem('token');
      if (isLoggedIn) {
        this.$router.push('/');
      }
    },

    toggleForm() {
      this.isRegister = !this.isRegister;
      this.$router.push('/acount/register');
    },
  },
};
</script>
<style scoped></style>