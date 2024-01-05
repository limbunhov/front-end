<template>
  <div class="navbar navbar-light narbar-expand-lg">
    <div>
      <div @click="toggleMenuBar()" class="menu">
        <i class="fa-solid fa-bars"></i>
        <span>Categories</span>
      </div>
      <menubar v-if="isOpen" />
    </div>
    <div class="catagary">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/Shop">Shop </RouterLink>
      <RouterLink to="/about">About </RouterLink>
      <RouterLink to="/adminpage">DeskBoard</RouterLink>
      <!-- <RouterLink to="/Contact">Contact Us</RouterLink> -->
      <RouterLink to="/crudproduct">CrudProduct</RouterLink>
    </div>
    <div class="information">
      <RouterLink to="/favorite">
        <i class="fa-solid fa-heart"></i>
      </RouterLink>
      <RouterLink to="/card">
        <div class="cart_count">
          <i class="fa-solid fa-cart-shopping"></i>
          <span>{{ cartItemCount }}</span>
        </div>
      </RouterLink>
      <!-- Conditional rendering based on user login state -->
      <i @click="acount_profile()" class="fa-solid fa-user"></i>
      <div v-if="Account">
        <div v-if="!isLoggedIn">
          <div class="card_member">
            <div class="d-flex justify-content-center align-items-center gap-1">
              <RouterLink to="/acount/login" @click="acount_profile" class="btn bg-info">Log in</RouterLink>
              <h5>OR</h5>
              <RouterLink to="/acount/register" @click="acount_profile" class="btn bg-success">Register</RouterLink>
            </div>
          </div>
        </div>
        <div v-else>
          <div class="card_member">
            <div class="d-flex justify-content-center align-items-center gap-1">
              <RouterLink to="/profile"  @click="acount_profile" class="btn bg-info">View Profile</RouterLink>
              <h5>OR</h5>
              <button class="btn bg-danger" @click="logout">Logout</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { RouterLink, RouterView } from 'vue-router';
import menubar from '../components/menubar.vue'
import login_form from '../components/login&register/login_form.vue';
import register_form from '../components/login&register/register_form.vue';
import Admin from '../components/AdminPage/Admin.vue';
import crud_product from '../components/AdminPage/Crud_product.vue';
import ShopPage from '../views/ShopPage.vue';
export default {
  components: { menubar, login_form, register_form, Admin, crud_product, ShopPage },
  data() {
    return {
      isOpen: false,
      Account: false,
      isLoggedIn: true,
      cartItemCount: 1
    };
  },
  methods: {
    countProduct(){
      this.cartItemCount = count;
    },
    
    toggleMenuBar() {
      this.isOpen = !this.isOpen;
      console.log("you clicked me ");
    },
    acount_profile() {
      this.Account = !this.Account;
    },
    logout() {
      console.log("Loged out");
      localStorage.removeItem('token');
      localStorage.removeItem('userId');
      this.Account = !this.Account;
      this.isLoggedIn = false;
      // this.$router.push('/login');
      this.$router.push('/acount/register');
    },
  },
};
</script>