<template>
    <div class="container" id="signup">
      <div class="cart_form">
        <h2>Register Now</h2>
        <form @submit.prevent="saveData">
          <label for="fullName">Full Name:</label>
          <i class="fa-solid fa-user"></i>
          <input type="text" id="fullName" v-model="registerData.fullName" placeholder="Full Name..." required>
  
          <label for="emailReg">Email address:</label>
          <i class="fa-regular fa-envelope"></i>
          <input type="email" id="emailReg" v-model="registerData.email" placeholder="Email..." required>
  
          <label for="passwordReg">Password:</label>
          <i class="fa-solid fa-lock"></i>
          <input type="password" id="passwordReg" v-model="registerData.password" placeholder="Password..." required>
  
          <label for="confirmPassword">Confirm Password:</label>
          <i class="fa-solid fa-lock"></i>
          <input type="password" id="confirmPassword" v-model="registerData.confirmPassword" placeholder="Confirm Password..." required>
  
          <div class="z-1 d-flex flex-column justify-content-center align-items-center">
                <button type="submit" :disabled="loading">Register</button>
                <span v-if="loading">Registering...</span>
                <span>Or</span>
                <div class="google">
                    <div>
                        <img src="../assets/image/google.png" alt="" width="20px">
                    </div>
                    <a href="#">Register with Google</a>
                </div>
                <span class="text-secondary">Already have an account?</span>
                <p class="li" @click="islogin()">Log in</p>
            </div>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        registerData: {
          fullName: '',
          email: '',
          password: '',
          confirmPassword: '',
        },
        loading: false,
      };
    },
    methods: {
        async saveData() {
            try {
                this.loading = true;
                const response = await axios.post('http://localhost:3000/register', this.registerData);

                console.log('Data saved:', response.data);
            } catch (error) {
                console.error('Error saving data:', error);
            } finally {
                this.loading = false;
            }
        },
        islogin() {
            this.$router.push('/acount/login');
        }
    },
  };
  </script>
  