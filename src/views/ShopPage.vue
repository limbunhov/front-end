<template>
  <section>
    <div class="filter_p">
      <div class="Searching">
        <input type="text" v-model="searchProduct" @input="applySearch" placeholder="Search products...">
        <span @click="applySearch"><i class="fa-solid fa-magnifying-glass"></i></span>
      </div>
    </div>
    <div class="sort_by">
      <div class="sort">
        <label>Sort by:</label>
        <select v-model="selectedSortOption" @change="applySort">
          <option value="default">Default</option>
          <option value="price-asc">Price (Low to High)</option>
          <option value="price-desc">Price (High to Low)</option>
          <option value="year-asc">Year (Old to New)</option>
          <option value="year-desc">Year (New to Old)</option>
        </select>
      </div>
    </div>
  </section>
  <section>
    <div style="margin-bottom: 18rem;">
      <div>
        <div class="name_brand">
          <p>New Arrive</p>
        </div>
        <div class="cart_items">
          <div v-for="product in filteredProducts" :key="product._id" class="cart">
            <div class="item_pic">
              <img :src="`${product.image}`" alt="Product Image" />
              <div class="social">
                <i class="fa-regular fa-heart" @click="toggleFavorite(product._id)"></i>
                <i class="fa-regular fa-eye"></i>
              </div>
            </div>
            <div class="detail">
              <h1>{{ product.name }}</h1>
              <p>&#10004;{{ product.title.t1 }}</p>
              <p>&#10004; {{ product.title.t2 }}</p>
              <p>&#10004;{{ product.title.t3 }}</p>
              <p>&#10004; {{ product.title.t4 }}</p>
              <p>&#10004; {{ product.title.t5 }}</p>
            </div>
            <div class="price_pro">
              <h1>$ {{ product.price }}</h1>
              <span @click="addToCart(product)"><i class="fa-solid fa-cart-shopping"></i></span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import axios from 'axios';
import * as jwtDecode from 'jwt-decode';


export default {
  data() {
    return {
      products: [],
      loading: true,
      searchProduct: '',
      selectedSortOption: 'default',
      selectedFilters: [],
      cartItemCount: 0,
      favoriteProducts: [],
    };
  },
  created() {
    this.fetchProducts();
  },
  computed: {
    filteredProducts() {
      let filtered = this.products.filter((product) => {
      const nameMatch = product.name && product.name.toLowerCase().includes(this.searchProduct.toLowerCase());
      const titleMatches = product.title && (
        ((product.title.t && product.title.t.toLowerCase().includes(this.searchProduct.toLowerCase())) || '') ||
        (product.title.t1 && product.title.t1.toLowerCase().includes(this.searchProduct.toLowerCase())) ||
        (product.title.t2 && product.title.t2.toLowerCase().includes(this.searchProduct.toLowerCase())) ||
        (product.title.t3 && product.title.t3.toLowerCase().includes(this.searchProduct.toLowerCase())) ||
        (product.title.t4 && product.title.t4.toLowerCase().includes(this.searchProduct.toLowerCase())) ||
        (product.title.t5 && product.title.t5.toLowerCase().includes(this.searchProduct.toLowerCase()))
      );
      return nameMatch || titleMatches;
    });

      if (this.selectedSortOption === 'price-asc') {
        filtered = filtered.sort((a, b) => a.price - b.price);
      } else if (this.selectedSortOption === 'price-desc') {
        filtered = filtered.sort((a, b) => b.price - a.price);
      } else if (this.selectedSortOption === 'year-asc') {
        filtered = filtered.sort((a, b) => (a.year || 0) - (b.year || 0));
      } else if (this.selectedSortOption === 'year-desc') {
        filtered = filtered.sort((a, b) => (b.year || 0) - (a.year || 0));
      }

      if (this.selectedFilters.length > 0) {
        filtered = filtered.filter((product) =>
          this.selectedFilters.some((filter) => product.attributes.includes(filter))
        );
      }

      return filtered;
    },
  },
  methods: {
    async fetchProducts() {
      try {
        // Assume you have a Node.js server running with Express and Mongoose
        const response = await axios.get('http://localhost:3000/products', {
          params: {
            search: this.searchProduct,
            sort: this.selectedSortOption === 'default' ? '' : this.selectedSortOption.toLowerCase(),
          },
        });

        this.products = response.data.map(product => ({ ...product, quantity: 0 }));
        this.loading = false;
      } catch (error) {
        console.error('Error fetching products:', error);
        this.loading = false;
      }
    },
    async applySearch() {
      this.loading = true;
      try {
        await this.fetchProducts();
      } catch (error) {
        console.error('Error fetching products:', error);
      } finally {
        this.loading = false;
      }
    },
    
    
    async addToCart(product) {
      const token = localStorage.getItem('token');
      const userId = localStorage.getItem('userId');
      console.log('Token:', token);
      console.log('UserId:', userId);
      const quantity = 1; // Define the quantity variable here or adjust as needed

      try {
        // Make a POST request to add the product to the user's cart
        const response = await axios.post('http://localhost:3000/add-to-cart', {
          userId: userId,
          productId: product._id,
          quantity: quantity, // Use the defined quantity variable
        });

        console.log('Added to cart:', response.data);
        // Optionally, you can update the local cart state or take other actions
      } catch (error) {
        console.error('Error adding to cart:', error);
      }
    },

    // Fetch cart items when the component is created
    async fetchCartItems() {
      const userId = 'your-user-id'; // Replace with the actual user ID

      try {
        const response = await axios.get(`http://localhost:3000/cart/${userId}`);
        this.cart = response.data;
      } catch (error) {
        console.error('Error fetching cart items:', error);
      }
    },

    // New method for sorting
    applySort() {
      this.loading = true;
      try {
        this.fetchProducts();
      } catch (error) {
        console.error('Error fetching products:', error);
      } finally {
        this.loading = false;
      }
    },

    async toggleFavorite(productId) {
      try {
        const userId = localStorage.getItem('userId'); // You should replace this with the actual user ID
        // const productId = product._id;
        console.log(userId);
        console.log(productId);

        console.log('Request Payload:', {
          userId: userId,
          productId: productId,
        });

        const isFavorite = this.isProductFavorite(productId);

        if (isFavorite) {
          // await axios.delete(`http://localhost:3000/favorites/${userId}/remove/${productId}`);
        } else {
          const response = await axios.post(`http://localhost:3000/add/favorites`, {
            userId: userId,
            productId: productId,
          });

          // console.log('Added to favorite:', response.data);
          // If it's not a favorite, add it
          // await axios.post(`http://localhost:3000/favorites/${userId}/add/${productId}`);
        }

        // You can update your local state or perform any other actions here
      } catch (error) {
        console.error('Error toggling favorite:', error);
      }
    },

    isProductFavorite(productId) {
      // Replace this logic with your actual check
      return this.favoriteProducts.includes(productId);
    },
  },
};
</script>
